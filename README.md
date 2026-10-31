# radion-nest: branch feature/section-templating

This feature branch augments [Radion](https://github.com/micahkepe/radion) with section templates.

The `content` page has been modified to demonstrate the new capabilities of section templating. Refer to the `base` branch for just the template modifications.

## Quick Start

```bash
zola serve --open
```

In addition to the Home, Categories and Tags tabs (which are left unchanged), there is now a new Sections tab for navigating the nested structure of the website.  
Click around and explore, or go through the Markdown files and directory structure of `content`!

## What's New
- Section templates, with automated and configurable generation of Subsection and Pages listings.
  - Section pages may use and render content in the body.
  - All direct subsections (unless `hidden`) are listed without pagination.
  - Pages listing may be configured to display all accessible pages (direct pages + pages from transparent subsections), direct pages only, or none.
    - *Note:* Pagination is supported only for listing of all accessible pages.
  - The home page is unchanged; pagination occurs *through* transparent sections.
- Adaptation of table of contents for section pages, includin Subsection and Pages listings; addition of `extra.summary` field as substitute for `page.summary` generated from `<!-- more -->` HTML comment delimiter.
- Usage of the following front-matter variables for sections:
  - `extra.summary`
  - `extra.show_pages`
  - `extra.sections_header`
  - `extra.pages_header`
- Usage and reservation of the following fragment identifiers for sections:
  - `#__radion-sections`
  - `#__radion-pages`

## What's Changed
- The title for the home `_index.md` page reads the `title` front matter variable, then `title` from `config.toml`, if `config.extra.radion_name` is unset.
- Table of contents for pages will display at the start of the body when opted into via `extra.toc = true`, even if a summary is not delimited via the `<!-- more -->` tag.

## Acknowledgements

This repository and branch are derivative works of [Radion](https://github.com/micahkepe/radion).