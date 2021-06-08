---
layout: default
title: Navigation Structure
nav_order: 5
---

# Navigation Structure
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Main navigation

The main navigation for your UI Theme Doc (Just the Docs) site is on the left side of the page at large screens and on the top (behind a tap) on small screens. The main navigation can be structured to accommodate a multi-level menu system (pages with children and grandchildren).

By default, links to all pages appear in the main navigation at the top level, ordered alphabetically by page title. By adding fields to the YAML front matter of individual pages, you can [change their order](#ordering-pages), [exclude pages](#excluding-pages), and [display pages as children ](#pages-with-children) to any depth.

Additional navigation features include [auxiliary links](#auxiliary-links) at the top of the page, and in-page navigation with an automatically-generated [table of contents](#in-page-navigation-with-table-of-contents).

If your site has pages with the same title, you need to avoid confusion when you reference that title on other pages. For the construction of the navigation display to work (and to avoid potential confusion when browsing) your page titles need to satisfy the following requirements:

* Top-level pages cannot have the same title.
* Children of the same parent cannot have the same title.
* A child cannot have the same title as its parent or any of its ancestors.

You can disambiguate references to parent titles in [several ways](#title-disambiguation). If two potential parents have the same title, but different grandparents, you can use the grandparent titles to identify the intended parent. For deeper navigation structures, you can also use the titles of more remote ancestors. And if you want the same navigation structure in different parts of the website, you can add section identifiers (which are not displayed).


---

## Ordering pages

To specify a page order, you can use the `nav_order` parameter in your pages' YAML front matter.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Customization
nav_order: 4
---
```

The parameter values determine the order of the top-level pages, and of child pages with the same parent. You can reuse the same parameter values (e.g., integers starting from 1) for the child pages of different parents.

The parameter values can be numbers (integers, floats) and/or strings. When you omit `nav_order` parameters, they default to the titles of the pages, which are ordered alphabetically. Pages with numerical `nav_order` parameters always come before those with strings or default `nav_order` parameters. If you want to make the page order independent of the page titles, you can set explicit `nav_order` parameters on all pages.

By default, all Capital letters come before all lowercase letters; you can add `nav_sort: case_insensitive` in the configuration file to ignore the case. Enclosing strings in quotation marks is optional.

[^case-insensitive]: *Note for users of previous versions:* `nav_sort: case_insensitive` previously affected the ordering of numerical `nav_order` parameters: e.g., `10` came before `2`. Also, all pages with explicit `nav_order` parameters previously came before all pages with default parameters. Both were potentially confusing, and they have now been eliminated. 

---

## Excluding pages

For specific pages that you do not wish to include in the main navigation, e.g. a 404 page or a landing page, use the `nav_exclude: true` parameter in the YAML front matter for that page.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: 404
nav_exclude: true
---
```

The `nav_exclude` parameter does not affect the [auto-generating list of child pages](#auto-generating-table-of-contents), which you can use to access pages excluded from the main navigation.

Pages with no `title` are automatically excluded from the navigation. 

---

## Pages with children

Sometimes you will want to create a page with many children (a section). First, it is recommended that you keep pages that are related in a directory together... For example, in these docs, we keep all of the written documentation in the `./docs` directory and each of the sections in subdirectories like `./docs/ui-components` and `./docs/utilities`. This gives us an organization like:

```
+-- ..
|-- (Jekyll files)
|
|-- docs
|   |-- ui-components
|   |   |-- index.md  (parent page)
|   |   |-- buttons.md
|   |   |-- code.md
|   |   |-- labels.md
|   |   |-- tables.md
|   |   +-- typography.md
|   |
|   |-- utilities
|   |   |-- index.md      (parent page)
|   |   |-- color.md
|   |   |-- layout.md
|   |   |-- responsive-modifiers.md
|   |   +-- typography.md
|   |
|   |-- (other md files, pages with no children)
|   +-- ..
|
|-- (Jekyll files)
+-- ..
```

On the parent pages, add this YAML front matter parameter:
-  `has_children: true` (tells us that this is a parent page)

#### Example
{: .no_toc }

```yaml
---
layout: default
title: UI Components
nav_order: 2
has_children: true
---
```

Here we're setting up the UI Components landing page that is available at `/docs/ui-components`, which has children and is ordered second in the main nav.

### Child pages
{: .text-gamma }

On child pages, simply set the `parent:` YAML front matter to whatever the parent's page title is and set a nav order (this number is now scoped within the section).

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
---
```

The Buttons page appears as a child of UI Components and appears second in the UI Components section.

### Auto-generating Table of Contents

By default, all parent pages will automatically have a Table of Contents at the bottom, listing their child pages. To disable this automatic Table of Contents, set `has_toc: false` in the parent page's YAML front matter.

#### Example
{: .no_toc }

```yaml
---
layout: default
title: UI Components
nav_order: 2
has_children: true
has_toc: false
---
```

### Children with children
{: .text-gamma }

Child pages can themselves have children, recursively, to any number of levels. 

#### Example
{: .no_toc }

```yaml
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
---
```

```yaml
---
layout: default
title: Buttons Child Page
parent: Buttons
nav_order: 1
---
```

This would create the following navigation structure:

```
+-- ..
|
|-- UI Components
|   |-- ..
|   |
|   |-- Buttons
|   |   |-- Button Child Page
|   |
|   |-- ..
|
+-- ..
```

---

### Title disambiguation
{: .text-gamma }

If no two pages on your website have the same `title`, you only need to set the `parent` titles to fix the hierarchy. You can also have the same `title` on pages that have no children, provided that they have different parent pages.

If two parents have the same `title`, but different grandparents, you can set their `grand_parent` titles to distinguish between their parents. The `grand_parent` title needs to be the same as the `parent` of the `parent`.


#### Example
{: .no_toc }

```yaml
---
layout: default
title: Buttons Child Page
parent: Buttons
grand_parent: UI Components
nav_order: 1
---
```

You can use the following techniques for disambiguating titles in deeper navigation structures (or simply instead of `grand_parent`): 

Ancestors
: The `ancestor` field of a page is similar to `grand_parent`: it refers to a page that can be reached by a succession  of `parent` titles.  

Sections
: You can choose a unique section identifier (a number or string), and add it as the `section_id` field of a page. Then use the same identifier for the `in_section` field of all its descendant pages. If you use a new `section_id` field inside a section, you create a sub-section.

In contrast to `ancestor` values, section identifiers are independent of page titles. However, you need to be careful not to set the same `section_id` value more than once.

---

## Auxiliary Links

To add auxiliary links to your site (in the upper right on all pages), add it to the `aux_links` [configuration option]({{ site.baseurl }}{% link docs/configuration.md %}#aux-links) in your site's `_config.yml` file.


#### Example
{: .no_toc }

```yaml
# Aux links for the upper right navigation
aux_links:
  "UI Theme Doc on GitHub":
    - "//github.com/gigamaster/ui-theme-doc"
```

---

## In-page navigation with Table of Contents

To generate a Table of Contents on your docs pages, you can use the `{:toc}` method from Kramdown, immediately after an `<ol>` in Markdown. This will automatically generate an ordered list of anchor links to various sections of the page based on headings and heading levels. There may be occasions where you're using a heading and you don't want it to show up in the TOC, so to skip a particular heading use the `{: .no_toc }` CSS class.

#### Example
{: .no_toc }

```markdown
# Navigation Structure
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
```

This example skips the page name heading (`#`) from the TOC, as well as the heading for the Table of Contents itself (`##`) because it is redundant, followed by the table of contents itself. To get an unordered list, replace  `1. TOC` above by `- TOC`.

### Collapsible Table of Contents

The Table of Contents can be made collapsible using the `<details>` and `<summary>` elements , as in the following example. The attribute `open` (expands the Table of Contents by default) and the styling with `{: .text-delta }` are optional.

```markdown
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
```

The result is shown at [the top of this page](#navigation-structure) (`{:toc}` can be used only once on each page).

