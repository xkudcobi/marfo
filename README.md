# MARFO

MARFO tools index. A single page linking to live demos of my browser based
tools, self hosted instead of Linktree.

Static site, no hosting tied to it yet

## Structure

Two files, no build step, no dependencies. GitHub Pages serves them straight
from `main`.

| File | Purpose |
| --- | --- |
| `index.html` | The whole page. Markup, CSS and the one script, in one file. |
| `logo.svg` | The mark: white square, black circle. Favicon, apple touch icon, OG image. |
| `tools/` | The tools themselves, one folder each, served from this same site. |

## Bundled tools

Every card links to a folder under `tools/`, so the whole thing ships as one
static site. Each tool is a self contained page, no build step.

| Folder | Card |
| --- | --- |
| `tools/kinetik/` | 01 Kinetic Type Animator |
| `tools/molten/` | 02 Liquid Font Generator |
| `tools/halo/` | 03 Melt and Halo Type |
| `tools/tessera/` | 04 Mosaic Tile Generator |
| `tools/lattice/` | 05 Pattern Generator |
| `tools/ember/` | 06 Thermal Poster Maker |
| `tools/stepper/` | 07 Step Sequencer |
| `tools/pulsar/` | 08 VJ Audio Visualizer |

## Design system

Modelled on a hardware quick start sheet: a light grey field with soft
rounded cells, everything set in uppercase mono, one red accent dot.

| Token | Value | Use |
| --- | --- | --- |
| `--bg` | `#e3e3e3` | Page field, visible as the gap between cells |
| `--cell` | `#f0f0f0` | Cell fill |
| `--ink` | `#2e2e2e` | Headings, names, numbers |
| `--ink-soft` | `#585858` | Body copy |
| `--ink-faint` | `#9b9b9b` | Counts, footer, resting state of `OPEN` |
| `--ink-deep` | `#0a0a0a` | A tool cell under the cursor, and the circles |
| `--on-ink` | `#ffffff` | Type on a turned over cell |
| `--on-ink-soft` | `#b8b8b8` | Body copy on a turned over cell |
| `--on-ink-hair` | `#3d3d3d` | The `OPEN` rule on a turned over cell |
| `--red` | `#d71921` | Accent dot on hover |
| `--r` | `22px` | Cell radius |
| `--gap` | `10px` | Grid gap and page padding |

Type is [Doto](https://fonts.google.com/specimen/Doto) for titles, numbers and
section letters, and [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono)
for everything else. Body copy is uppercase with open tracking.

House style: no em dashes anywhere in the copy. Break the sentence or use a
comma.

## Hover

The eight tool cells turn over to `--ink-deep` on hover and focus, type to
white, over `.55s`. The lift runs faster at `.25s` so the card still feels
responsive while the colour is still travelling. The red dot fades in at
`.35s`. Category bars do not turn over: nothing there is clickable.

## Categories

| Key | Category | Tools |
| --- | --- | --- |
| A | Type | 01 to 03 |
| B | Print & Pattern | 04 to 06 |
| C | Sound & Visual | 07, 08 |

Numbering runs `01` to `08` straight through, across categories. Adding a tool
mid sheet therefore renumbers every card after it, and the two meta
descriptions in `<head>` spell the total out in words.

## Adding a tool

Copy a `.tool` cell into the right category `.row`, then bump the numbers that
follow it and the `count` on that category bar.

```html
<a class="cell tool" href="https://EXAMPLE.COM" target="_blank" rel="noopener">
  <div class="cell-top"><span class="dot idx">00</span><span class="cue"></span></div>
  <div class="name">WHAT IT DOES</div>
  <div class="cell-body">
    <div class="meta">
      <span class="code">CODENAME</span>
      <span class="desc">ONE OR TWO LINES, UPPERCASE, NO EM DASH.</span>
    </div>
    <div class="go">OPEN<svg viewBox="0 0 12 12" aria-hidden="true"><path d="M3.5 8.5 8.5 3.5M4.5 3.5H8.5V7.5" fill="none" stroke="currentColor" stroke-width="1.4"/></svg></div>
  </div>
</a>
```

`.name` is the function, `.code` is the project name. A visitor scans for what
a thing does before they care what it is called.

## Adding a category

Add a bar, then a row under it:

```html
<div class="bar">
  <span class="dot">G</span>
  <h2>CATEGORY NAME</h2>
  <span class="count">/ 2</span>
</div>
<div class="row">
  ...tool cells...
</div>
```

`.row` is `auto-fit, minmax(288px, 1fr)`, so two cells fill half the width each
and three fill a third each. No empty slots to plan around.

## Linking a new tool

Drop the tool's folder under `tools/` and point the card at `tools/NAME/`.
Relative asset paths only, no root absolute `/js/...` paths, so the site works
from any subfolder.
