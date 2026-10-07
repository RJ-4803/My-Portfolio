# Renujaan Ravichandran · Portfolio

A one-page portfolio site. Plain HTML, CSS and JavaScript with no build step.

## Folder layout

```
Portfolio/
├── index.html          The whole site: markup, styles and script in one file
├── assets/             Everything the live site loads
│   ├── img/            profile.jpg, project-resqlink.png, project-sgpa.png
│   └── icons/          favicon-32.png, favicon-192.png, apple-touch-icon.png
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
| `<body>` | Sections in page order: hero, what I do + projects, about, skills, achievements, contact |
| `<script>` | Smooth scrolling, pinned sections, letter effects, parallax layers, pointer tilt |

Colours and fonts are CSS variables at the top of `<style>`; changing them there updates the whole site.
The frosted-glass tints are the `--g-*` variables at the top of the GLASS block.

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
