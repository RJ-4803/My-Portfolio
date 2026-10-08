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
│   ├── documents/      The CV (PDF) opened by the two "View CV" buttons
│   └── video/          Optional. The hero's background clip goes here (see "Background video")
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
| `<script>` | Menu button, copy email, optional video, smooth scrolling, pinned sections, letter effects, parallax layers, pointer tilt |

### Design tokens

Everything visual is a CSS variable in the TOKENS block at the top of `<style>`; changing one
there updates the whole site.

| Group | Variables |
| --- | --- |
| Surfaces | `--bg`, `--bg-2`, `--surface`, `--surface-2` |
| Text | `--text`, `--text-2`, `--muted` |
| Borders | `--line`, `--line-2` |
| Accents | `--accent` (electric blue: interaction and data), `--accent-2` (teal: active states), `--accent-glow`, `--grad` |
| Technical background | `--grid-o` and `--grid-cell` (the grid), `--trace-o` (wires), `--node-o` (nodes) |
| Video | `--vid-o` (its opacity), `--vid-overlay` (the dark layer over it) |
| Glass | `--blur`, plus the `--g-*` tints in the GLASS block |
| Motion | `--dur-1` to `--dur-3`, `--dur-signal`, `--dur-amb`, `--ease` |

Colours are also stored as channels (`--accent-rgb`, `--accent-2-rgb`, `--bg-rgb`, `--surface-rgb`,
`--edge-rgb`, `--grid-rgb`) so any opacity can be mixed from them: `rgb(var(--accent-rgb) / 0.2)`.
To change the accent colour, change the channel values.

### The background system

The backgrounds are drawn with CSS and inline SVG; there is no canvas and no image.
One idea runs through them: the path of a request through the stack.

| Piece | Class | Where |
| --- | --- | --- |
| Engineering grid | `.grid` (and `.sec::before`) | Every scene; fades toward the text |
| Circuit traces with signals | `.net` (inline SVG) | Hero, wide screens only |
| Request path: client → api → data | `.bus`, `.hub`, `.wire` | Foot of the hero; ends in the Scroll cue |
| Rings | `.rings` | Behind the portrait and behind the contact card |
| Lanes | `.wire.lane` | Achievements band and contact |
| Checkpoint path | `.results` | Achievements; draws as you scroll (`--draw`) |
| Skills wire | `.flow` | Frontend → Backend → Databases |

Each trace in the hero SVG appears twice: once as a line and once with class `sig`, which is
the signal that travels along it. To add a trace, add both.

### Background video (optional)

The hero can play a clip behind the drawn background. It is off until you give it a file:

1. Put the clip at `assets/video/tech-background.mp4` and a still frame from it at
   `assets/video/tech-background.jpg`.
2. In `index.html`, find `class="vid"` and set
   `data-src="assets/video/tech-background.mp4"` and `data-poster="assets/video/tech-background.jpg"`.

The clip plays only on screens 900px or wider, with motion allowed, no data-saver, and at least
4 GB of device memory. Phones and everyone else get the still frame. It loads after the page
has finished loading, pauses when the hero is off screen or the tab is in the background, and
if the file is missing the drawn background simply stays.

What to look for in a clip:

| | |
| --- | --- |
| Subject | Abstract technology: flowing data, fibre light, a circuit board in close-up, a slow network visualisation. No people, keyboards, screens of code, text or logos |
| Look | Dark background, low contrast, blue or teal highlights, slow movement |
| Shape and size | 16:9, 1920×1080 (1280×720 is enough, since it sits behind an overlay) |
| Length | 8 to 20 seconds, cut so the last frame matches the first (a seamless loop) |
| Format | MP4, H.264, no audio track, 24 or 30 fps |
| File size | 2 to 4 MB; do not go above 6 MB |
| Rights | A clip you made or are licensed to use |

If the clip looks too strong or too faint, change `--vid-o` and `--vid-overlay`.

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
  pinning, scroll effects, signals or video. The grid, traces and rings stay, so the design is intact.
- **Touch screens.** Project cards have no hover there, so each one switches on while it crosses
  the middle of the screen.
- **Small screens.** Below 900px the links sit behind a menu button. Without JavaScript the button
  is hidden and the links show as one scrollable row.
- **In-page links** stop below the fixed header because of `scroll-padding-top` on `<html>`.
  Lenis reads the same value, so the script adds no offset of its own.
