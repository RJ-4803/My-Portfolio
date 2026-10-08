# Renujaan Ravichandran · Portfolio

A one-page portfolio site. Plain HTML, CSS and JavaScript with no build step.

## Folder layout

```
Portfolio/
├── index.html          The whole site: markup, styles and script in one file
├── assets/             Everything the live site loads
│   ├── img/            profile.jpg, project-resqlink.png, project-sgpa.png,
│   │                   og-card.jpg (the picture shown when the link is shared)
│   ├── icons/          favicon-32.png, favicon-192.png, apple-touch-icon.png
│   └── documents/      The CV (PDF) opened by the two "View CV" buttons
├── Images/             Original, full-size source images (not used by the live site)
│   ├── profile/        portrait-formal.png
│   ├── favicon/        portrait-outdoor.jpg
│   └── projects/       resqlink-dashboard.png, sgpa-calculator.png
├── archive/            Earlier versions, kept for reference
└── README.md
```

To publish the site you only need `index.html` and the `assets/` folder.

## Preview locally

From this folder:

```bash
python -m http.server 8765
```

Then open http://localhost:8765. Opening `index.html` directly also works, but use
the local server when checking images and scroll effects.

## Publish to GitHub Pages

Upload `index.html` and `assets/` to the root of the `RJ-4803/My-Portfolio` repository.
GitHub Pages then serves it at https://rj-4803.github.io/My-Portfolio/.

## Editing

`index.html` has three parts, each divided by comment headers:

| Part | What it holds |
| --- | --- |
| `<style>` | Design tokens (colours, fonts, spacing) first, then one block per section of the page |
| `<head>` | Title, description, canonical URL, link-preview tags and structured data |
| `<body>` | Sections in page order: hero, what I do + projects (featured card, then two smaller ones), competition results, beyond the classroom, skills, about, contact |
| `<script>` | Menu button, copy email, smooth scrolling, pinned sections, letter effects, parallax layers, pointer tilt |

Colours and fonts are CSS variables at the top of `<style>`; changing them there updates the whole site.
The frosted-glass tints are the `--g-*` variables at the top of the GLASS block.

### Things to keep in sync

- **The site address appears in `<head>` several times** (canonical URL, `og:url`, `og:image`,
  `twitter:image`, structured data). If the site moves, update all of them.
- **Each project card states team or solo, and your role.** Keep that accurate when adding projects.
- **Highlighted skills** (the `core` class in the Skills section) are the ones the listed projects use.
  Update them when the project list changes.
- **The CV file name** is linked from the menu, the hero and the contact card.
- **The link-preview picture** (`assets/img/og-card.jpg`, 1200×630) repeats the name, the title and
  the stack. Remake it if any of those change.

### Slots waiting for real information

Search `index.html` for these comment labels. Each marks a place where a true detail would
strengthen the page; they are left empty rather than filled with guesses.

| Label | Where | What to add |
| --- | --- | --- |
| `CURRENTLY` | Hero | One line on what you are learning or building now |
| `RESULT` | ResQLink card | A real outcome: where it was presented, who used it |
| `LIVE DEMO` | ResQLink card | A "Live demo" button once the deployment is back online |
| `PROJECT LINK` | Competition results | One line if a listed project was built at one of the hackathons |
| `CURRENTLY LEARNING` | About facts | A fifth fact, already written and commented out |

## Adding or replacing an image

1. Put the original in `Images/` (for example `Images/projects/tickethub-dashboard.png`).
2. Save a web-sized copy in `assets/img/` (project screenshots are named `project-<name>.png`).
3. Point the matching `<img src="assets/img/...">` in `index.html` at it.

The TicketHub card currently uses a drawn illustration because it has no screenshot yet.

## Notes

- **One file on purpose.** Keeping styles and script inside `index.html` means the page still
  renders when the file is opened or previewed on its own, without its neighbours.
- **Smooth scrolling** uses [Lenis](https://github.com/darkroomengineering/lenis), loaded from a CDN.
  Without a connection the page falls back to normal scrolling.
- **Reduced motion.** Visitors who ask their system to reduce motion get a static page with no
  pinning or scroll effects.
- **Small screens.** Below 900px the links sit behind a menu button. Without JavaScript the button
  is hidden and the links show as one scrollable row.
- **In-page links** stop below the fixed header because of `scroll-padding-top` on `<html>`.
  Lenis reads the same value, so the script adds no offset of its own.
