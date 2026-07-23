# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal portfolio site for Hein Htut Zaw (Henry), served as static files from GitHub Pages at `heinhtutzaw19.github.io`.
Built on the "Massively" HTML5 UP template. There is no build step, no framework, and no test suite - editing HTML/CSS and pushing to `main` deploys the live site.

## Developing

- Preview locally by opening `index.html` in a browser, or run any static server (e.g. `python3 -m http.server`) from the repo root so relative asset paths resolve.
- Deploy by committing to `main` and pushing; GitHub Pages serves the root directly.

## Editing CSS

`assets/css/main.css` is compiled from the Sass sources in `assets/sass/` (`main.scss` imports `base/`, `components/`, `layout/`, `libs/`). Edit the `.scss` files and recompile rather than hand-editing the built CSS. `noscript.css` compiles from `noscript.scss`.

## Structure that isn't obvious from the file tree

- **Two pages only:** `index.html` (projects) and `about.html`. Both share the same nav, header, and footer markup - a change to nav/footer must be duplicated across both files.
- **Projects are hardcoded HTML**, not data-driven. Each project is an `<article>` inside the single `.posts` section (`#projects`) in `index.html`. Adding a project means copying an existing `<article>` block, dropping an image into `images/`, setting the tech-stack `<span class="tags">` chips, and adding a `data-category` attribute (see below).
- **Category filtering.** A `.filters` bar above the projects holds buttons with `data-filter` values (`all`, `data`, `software`, `ai`, `robotics`). Each `<article>` carries a `data-category` attribute with one or more space-separated categories (e.g. `data-category="software ai"`). The inline `<script>` at the bottom of `index.html` toggles each article's `hidden` attribute on button click - plain vanilla JS, no jQuery. Adding a new category means adding a filter button and tagging the relevant articles; a project with no matching filter simply never shows under that button. There is no pagination or router - all projects live in one list.
- The template JS in `assets/js/` (jQuery + `main.js`, `util.js`, breakpoints, etc.) is vendored template code handling the intro animation, responsive nav, and scroll effects. Leave it alone unless changing template behavior.

## Conventions

- Project tech-stack chips use inline `style="background-color: #99ccff;"` on `<span class="tags">`. Match that when adding tags. These are separate from `data-category` (the filter dimension).
- The filter bar's styling lives in a scoped `<style>` block in `index.html`'s `<head>`, not in the Sass sources.
- Resume lives at `assets/docs/resume.pdf`.
