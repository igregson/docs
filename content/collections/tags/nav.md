---
overview: >
  The nav tags are designed to help your
  users navigate through your hierarchy of
  pages. They work together to allow you
  to easily traverse your content upways
  and downways, sideways, slantways,
  longways, backways, squareways,
  frontways, and any other ways that you
  can think of.
title: Nav
id: ed746608-87f9-448f-bf57-051da132fef7
is_parent_tag: true
parameters:
  -
    name: from
    type: string
    description: "The starting point for your navigation. If unspecified, it'll use the current URI."
  -
    name: max_depth
    type: 'integer *1*'
    description: >
      The maximum number of subdirectory
      levels to traverse, letting you build a
      multi-level nav.
  -
    name: show_unpublished
    type: 'boolean *false*'
    description: "Unpublished content is, by it's very nature, unpublished. That is, unless you show it by turning on this parameter."
  -
    name: include_entries
    type: 'boolean *false*'
    description: >
      Whether entries mounted under a page
      should be included as part of the
      navigation.
  -
    name: sort
    type: string
    description: >
      The field by which the pages will be
      sorted. For example, specify `title` to
      sort alphabetically by the title field.
  -
    name: include_home
    type: 'boolean *false*'
    description: >
      You can choose to turn off the home page
      in the tree, opting to start the crumbs
      from the first level nav item.
  -
    name: exclude
    type: 'string|array'
    description: >
      A single URL, or a list of multiple pipe-separated URLs, to be excluded.
  -
    name: filter
    type: wizardry
    description: >
      Filter the tree by using a special conditions syntax, the same as the [Collections tag](/docs/tags/collection). View the [available conditions](/docs/conditions).
variables:
  -
    name: is_published
    type: boolean
    description: Whether or not the page is published.
  -
    name: is_page
    type: boolean
    description: >
      Whether or not the page is in fact a
      page. If you are using the `entries`
      parameter to show entries, a "page" may
      potentially be an entry.
  -
    name: is_entry
    type: boolean
    description: >
      The inverse of `is_page`. Outputs
      whether the "page" is an entry.
  -
    name: has_entries
    type: boolean
    description: >
      Whether the current page has entries
      mounted to it.
  -
    name: children
    type: array
    description: >
      An array of child pages. Use this as a
      tag pair to iterate over any child
      pages.
  -
    name: parent
    type: array
    description: "An array containing the current page's parent. Use this as a tag pair to output variables from the parent's page data."
  -
    name: is_parent
    type: boolean
    description: >
      Whether the current page is a parent of
      the URL being viewed. Useful for
      outputting active states.
  -
    name: is_current
    type: boolean
    description: >
      Whether the current page is the URL
      being viewed. Also useful for outputting
      active states.
  -
    name: page data
    type: mixed
    description: >
      Each page being iterated has access to
      all the variables inside that page. This
      includes things like `title`, `content`,
      etc.
  -
    name: '*recursive children*'
    type: wizardry
    description: >
      Recursively output the entire contents
      of the `nav` tag pair. More information
      about this is below.
---
## Recursion {#recursion}

It's possible to use recursive tags for semi-automatically creating deeply-nested lists of links as your navigations. A sample set-up looks something like this:

```
<ul>
   {{ nav from="/{segment_1}" }}
      <li>
         <a href="{{ url }}"{{ if is_current || is_parent }} class="on"{{ /if }}>{{ title }}</a>
         {{ if is_current || is_parent }}
            {{ if children }}
               <ul>{{ *recursive children* }}</ul>
            {{ /if }}
         {{ /if }}
      </li>
   {{ /nav }}
</ul>
```

The `{{ *recursive children* }}` tag will repeat the contents of the entire `{{ nav }}` tag using child elements if they exist. This means that as long as there are children to display, and we’re still on either the current or parent page of those children, the nav tag will traverse deeper.

It’s an admittedly weird concept, and might take some fiddling with to truly understand, but is very powerful when fully understood. Take the time. Learn to wield it. A powerful Jedi will you be.