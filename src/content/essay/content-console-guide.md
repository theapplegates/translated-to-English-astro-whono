---
title: Content Console User Guide
description: A guide to the astro-whono local Content Console — browsing, searching, editing, previewing, downloading, and deleting content.
badge: guide
date: 2026-06-13
tags: [ "Content Console", "guide" ]
draft: false
---

astro-whono ships with a local Content Console for managing site content in a development environment.

The Content Console lives at `/admin/content/`. It covers four content categories — essay, Whisper, Notes, and About — letting you browse, find, edit, and preview them, and supports creating drafts, downloading source files, and deleting. It is handy when you'd rather not hand-edit frontmatter directly.

:::note[Development environment]
`/admin/content/` and its editor pages only work in the development environment. Visiting them in production shows only a local-development notice; content data and the editor do not load. `/api/admin/content/*` serves only the local backend and is not a public API.
:::

## Local startup and entry

When developing locally, start the project with:

```bash
npm install
npm run dev
```

By default the dev server runs at `http://localhost:4321/`. After it starts, open:

```text
http://localhost:4321/admin/content/
```

If you changed the dev port, replace `4321` with your actual port.

The Content Console reads the source files under `src/content/**` directly, with no database or external services. Creating, saving, and deleting content files writes into the repository, so you can track and roll back changes through Git.

## Content types and capabilities

The Content Console manages four content types, but their capabilities differ:

| Content | Path | New | Edit | Delete | List filter |
| :--- | :--- | :---: | :---: | :---: | :---: |
| Essay | `src/content/essay/` | yes | yes | yes | yes |
| Whisper | `src/content/bits/` | yes | yes | yes | yes |
| Notes | `src/content/memo/index.md` | — | yes | — | — |
| About | `src/content/about/index.md` | — | yes | — | — |

Essays and Whispers are multi-entry collections: you can create drafts, edit, and delete entries one by one, and the list offers filtering and pagination. Notes and About are fixed single-page content; only the existing text can be edited, with no new or delete.

## Browse, filter, and search

Opening `/admin/content/` shows an overview that groups Essay, Whisper, and Notes content by default. The top toolbar provides:

- Search: find across content by title, tag, or slug
- Scope: switch between "All content" and a single category
- State: All / Published only / Drafts only
- Sort: Latest update / Title A–Z
- Years: filter by content year

State, sort, year filtering, and pagination apply only to essays and Whispers; Notes and About are fixed single pages and do not expose these filters. In the list, drafts are marked `[draft]` and essays excluded from the archive are marked `[archive off]`.

Each item has an "Edit" button, plus a "More" menu with edit-info, view-on-site, download, and delete actions.

## New and edit

### Essay

In the essay group, click "New article". After filling in basic info such as the title, a draft is created and you jump to the editor.

The essay editor provides:

- A CodeMirror-based text area with multiple syntax-highlight themes and line-number options
- Edit / preview layout switching, with server-side rendered preview
- A frontmatter panel: publish date, updated date, tags, draft, and archive fields
- Two auxiliary sidebars: outline and Markdown syntax
- A toolbar: common Markdown, math formulas, emoji, images, and galleries
- Body image upload: saved to the current content's attachment directory and inserted as Markdown

### Whisper

In the Whisper group, click "New activity". After choosing a publish time a draft is created and you jump to the editor.

The Whisper editor is a standalone workbench for editing text, basic info, and images (`images` rows). It supports image upload and a live card preview that matches the cards in the `/bits/` list exactly.

### Notes and About

Notes and About are fixed single-page content; the editor only handles text:

- Notes: edit the `src/content/memo/index.md` text, with support for inline images, page preview, and an in-text table of contents
- About: edit the `src/content/about/index.md` text. Friend links and FAQ in the preview render with the public page styles; the contact-link slot is controlled by `::contact-links`

The titles and subtitles of the Notes and About pages are not maintained here — adjust them in the Theme Console.

## Batch operations

After selecting items in the list, use "Batch operations" to:

- Publish / set to draft: batch-toggle the `draft` state
- Download: pack the selected content's source files into a zip
- Delete: delete the selected items in bulk, moving source files to the trash (confirmed first)

Batch operations act on the currently checked items. Use filters or search to narrow the scope, then process in batches.

## Download and delete

- Download: from an item's "More" menu, choose "Download source file" to get its Markdown document
- Delete: from an item's "More" menu; the source file is moved to the trash rather than erased outright, and is confirmed first

Download and delete act on the source file itself. Delete is supported only for essays and Whispers; Notes and About cannot be deleted.

## Content fields and writing conventions

The Content Console is for entering and maintaining content. Specific frontmatter fields, image-path rules, and body writing conventions (callouts, figures, galleries, formulas, etc.) are still governed by the "Content and writing" section of the repo README, so they are not repeated here.

**New content is a draft by default.** Essay and Whisper drafts are visible during local development and are automatically filtered out of production builds, RSS, and public lists. Notes are single-page content and should not be marked as draft.

---

## A note at the end

:::info[Why build a local backend?]
The Content Console is the most complex, time-consuming part of the whole backend. Since everything is written locally and you already need the dev server, you could just edit the Markdown directly — so why build this backend?

- astro-whono's target users may not be familiar with front-end work. Remembering frontmatter fields, directory structure, and writing conventions when editing source files directly is a lot; the backend gathers these into forms and buttons to lower the barrier.
- When writing, the final layout matters most. The editor's built-in server preview shows text, cards, and About pages close to how they'll appear before you save, so you don't have to keep switching to the browser.
- Common content formats (callouts, images, galleries, formulas, emoji, etc.) can be inserted straight from the toolbar, sparing you hand-written markup and docs.
- Fixed single pages like Notes and About used to require editing source files; now you can edit the text in place in the backend and preview it, which is more convenient.

The Content Console is not meant to replace the command line or your editor. It exists so people without a coding background can comfortably maintain their own content. The ideal, of course, would be a real CMS — but that is a different scope of work and is not in the current plan.
:::

### 🔜 Current progress and next steps

The Content Console's originally-envisioned features are now mostly done. The admin backend will focus on maintenance and detail polish going forward, with no new features planned. If you have ideas or suggestions while using it, they are welcome.

:::tip[Next steps]
A comments feature is planned, currently leaning toward Waline. Wiring it into essays is fairly straightforward; Whispers are short, feed-style pages and will need a redesigned comment layout for that kind of page. So while the comment module is on the roadmap, it may take some time before it ships.
:::

---

The above covers the Content Console's content-management entries and common operations. If you run into content anomalies, save issues, or have feature ideas, please open an Issue.
