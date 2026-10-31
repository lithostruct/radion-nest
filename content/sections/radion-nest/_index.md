+++
title = "Radion-Nest"
description = "Posts relating to extending Radion with section and navigation support."

transparent = true
sort_by = "date"
weight = 1

[extra]
toc = true
summary = '''
This section catalogues and tests the addition of sections to Radion.  
As a matter of fact, <i>this text too</i> is a test![^0]

This section page uses `extra.show_pages = "all"`. It should display all its accessible pages.

[^0]:
    Foreshadowing is a narrative device in which suggestions or warnings about things to come are dropped or planted.
'''
+++


# What's New?

One major thing really.  
Introducing:

## Section Templates

You may now write and configure `_index.md` files to configure how sections display!

The front-matter variables supported are as such:
```toml
# To ensure pages in this section can be pagniated by the home page.
# Subsections can choose whether to be set as transparent.
# If it is set to `false`, this section and its contents will not be included in the home page.
transparent = true

[extra]

# Enables table-of-content generation. Default value set to `false`.
# This functions similarly to table-of-content generation for pages,
# with the addition of automatically-generated headers where applicable.
toc = true | false

# Pages can be split into the summary and main body via <!-- more -->, but not so with sections.
# This variable allows for the insertion of a string as a "summary",
# which follows Radion's theming and will display before the table of contents.
# Renders as Markdown.
summary = string as markdown

# Defines how pages are shown. Default value set to `"all"`.
# Section pagination via `paginate_by` is only compatible with this value set to `"all"`.
# `"all"`: All accessible pages shown.
#    This includes pages from transparent subsections and their descendants.
# `"direct_only"`: Only display direct pages in this section.
# `"none"`: Do not show a `Pages` listing. Pages within this section may still be included in 
#    home page pagination, depending on the value of `transparent`.
show_pages = "all" | "direct_only" | "none"

# The header name of the Sections listing. Default value set to `"Sections"`.
sections_header = string
# The header name of the Pages listing. Default value set to `"Pages"`.
pages_header = string
```
Caveats[^1] do[^2] apply.[^3] [^4]

## Table of Contents Support

Section pages can be pages in their own right. That's why you can also opt into Table of Contents generation via the front matter variable `extra.toc = true`.

This functions identically to Radion's Table of Contents generation for pages, with the addition of automatically generated `Section` and `Pages` headings where applicable.

# Minor Tweaks

This template should be similar to base Radion, such that one can switch from one to the other if section capabilities are not used.
However, there are a couple of details that have been modified:
- The home `_index.md` page now reads the `title` front matter variable, then `title` from `config.toml`, if `config.extra.radion_name` is unset.  
  You can think of the latter as an override now, rather than the default way to set the title of the home page.
- Table of contents for pages will display at the start of the body, opted into via `extra.toc = true`, even if a summary is not demarcated via the `<!-- more -->` tag.

[^1]:
    `extra.summary` internally uses Zola's `markdown` filter within a dedicated section of the section template. This means that it has access to all of the CommonMark specification, but cannot interact with the rest of the document. Notice how the first *1st* footnote in the summary comes before the table of contents?

    Any augmentation to Zola's Markdown rendering eg. LaTeX support in the case of Radion will also be usable within the summary section.

[^2]:
    A table of contents is only generated if the corresponding `section.toc` is populated, despite the fact that every section can be populated with both `Sections` and `Pages` headers. This holds even if `extra.toc` is set to `true`.

[^3]:
    The `pages` statistic displayed for each subsection only accounts for the total number of pages directly and from transparent sections. This will be the common case anyways, but pages can be accessible via section navigation and yet are seen as invisible from an enclosing section. All subsections will be listed unless explicitly `hidden` via front matter configuration.

[^4]:
    Giscus comments are disabled by default in sections. This may be overriden by setting `extra.comments = true` in the section front-matter.