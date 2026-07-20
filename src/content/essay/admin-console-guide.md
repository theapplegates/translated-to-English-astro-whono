---
title: Admin Console Quick Guide
description: An introduction to the astro-whono local Admin Console entry points and what each page does.
badge: guide
date: 2026-04-24
tags: [ "Admin Console", "guide" ]
draft: false
---
<cloudinary-picture
  src="assets/images/The-Gulfstream-G800.20250416"
  alt="TODO: describe this image"
  width="3600"
  height="2400"
  devices="1200|40|original,992|60|16:9,768|70|4:3,0|100|1:1"
  breakpoints="50, 432, 647, 858, 1000"
  picture-class="responsive-picture"
/>



<cloudinary-picture
  src="assets/images/slava-auchynnikau-Z4g5S4sksPQ-unsplash"
  alt="TODO: describe this image"
  width="4000"
  height="2667"
  sizes="(min-width: 768px) 720px, 100vw"
  breakpoints="50, 431, 638, 746, 968, 984, 1000"
  picture-class="responsive-picture"
/>


<cloudinary-picture
  src="assets/images/alim-unsplash"
  alt="TODO: describe this image"
  width="4018"
  height="3014"
  sizes="(min-width: 768px) 720px, 100vw"
  breakpoints="50, 402, 604, 715, 786, 873, 879, 1000"
  picture-class="responsive-picture"
/>

<cloudinary-picture
  src="assets/images/the-metropolitan-museum-of-art-zvD1-cNLluI-unsplash"
  alt="TODO: describe this image"
  width="2846"
  height="3536"
  sizes="(min-width: 768px) 720px, 100vw"
  breakpoints="50, 319, 439, 519, 524, 690, 703, 727, 777, 825, 855, 864, 901, 938, 982, 988, 1000"
  picture-class="responsive-picture"
/>

The Admin Console at `/admin/` is the local backend entry point, used after forking, cloning, or self-hosting to maintain site configuration and content.

It is not a standalone CMS. Saving writes back to the configuration or content files inside the repository, so it pairs well with Git: you can review diffs before and after changes, and roll back as normal project files when needed.

:::note[Local tools]
The Admin Console's editing features are only available in the development environment.<br>
Production keeps at most a read-only site overview page; `/api/admin/*` serves only the local backend and is not a public API.
:::

## Quick entry

Start the project locally:

```bash
npm install
npm run dev
```

The dev server runs at `http://localhost:4321/` by default; if you changed the port, replace `4321` with your actual port.

| Entry | Page | Main purpose |
| :---: | :---: | :--- |
| `/admin/` | Site Overview | View the site overview, content structure, and recent articles |
| `/admin/theme/` | Theme Console | Edit site info, sidebar, homepage, and inner-page copy |
| `/admin/content/` | Content Console | Article management and visual writing |
| `/admin/images/` | Images Console | Browse image resources and copy usable paths |
| `/admin/checks/` | Checks Console | View structured diagnostics and run pre-release checks |
| `/admin/data/` | Data Console | Import and export theme settings for migration and backup |

## Main pages

### 📈 Site Overview

[Site Overview](/admin/) is the backend home, showing content counts, recent updates, and admin entry points (the entries are visible only in the development environment).

This page is optional and can be shown to visitors, controlled by the "Admin Overview" toggle inside the Theme Console.

### 🛠️ Theme Console

The Theme Console manages theme-level configuration, making it easy to adjust basic site settings after forking or cloning.

See the [Theme Console configuration guide](/archive/theme-console-guide/) for details.

### 📝 Content Console

The Content Console is the entry point for content management and visual writing, where you can review and maintain the site's written content in one place.

See the [Content Console user guide](/archive/content-console-guide/) for details.

### 🖼️ Images Console

The Images Console lets you browse image resources, inspect image info, and copy paths for use in configuration or content fields.

It is currently a resource browser: it does not compress, delete, or replace files. When you need to change an image, put it in the agreed project directory first, then return to the relevant page to select or fill in the path.

### ✅ Checks Console

The Checks Console runs pre-release checks, organizing content, configuration, image references, and agreed-upon risks into diagnostic results.

It does not modify files directly. When it finds an issue, go back to Theme, Content, or the source code to address it.

### 📤 Data Console

The Data Console handles importing or exporting theme settings. Export is for migration or backup; import runs a pre-check first and writes only after confirmation.

It works with the theme configuration data managed by the Theme Console, not with article content.

---

Those are the Admin Console's main entries and features. If you have more ideas or suggestions, please open an Issue.
