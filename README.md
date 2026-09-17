# MARFO

Eight browser based tools for type, pattern, poster and sound work, behind a
retro desktop home screen. Nothing to install, no accounts, no server.

Live at https://xkudcobi.github.io/marfo/ via GitHub Pages, served straight
from `main`. Static files only, no build step.

## Structure

| Path | Purpose |
| --- | --- |
| `index.html` | The hub. Markup, CSS and the one script, in one file. |
| `404.html` | Not found page in the same window style. Pages serves it for any missing path. |
| `logo.svg` | The mark: white square, black circle. Favicon and apple touch icon of the hub. |
| `og.png` | 1200 x 630 share image for link previews. |
| `tools/` | The tools themselves, one folder each. Each is self contained. |
| `tools/NAME/icon.svg` | The tool's desktop icon, also used as that tool's favicon. |

## Tools

| Folder | Name | What it does |
| --- | --- | --- |
| `tools/kinetik/` | KINETIK | Kinetic type animator. `flash.html` is a second, stroboscopic engine on p5. |
| `tools/molten/` | MOLTEN | Liquid font generator, exports OTF. `poster.html` sets the font on a poster. |
| `tools/halo/` | HALO | Melt and halo type. |
| `tools/tessera/` | TESSERA | Mosaic tile generator. |
| `tools/lattice/` | LATTICE | Pattern generator. |
| `tools/ember/` | EMBER | Thermal poster maker, WebGL fluid feedback. |
| `tools/stepper/` | STEPPER | MIDI step sequencer and sampler. |
| `tools/pulsar/` | PULSAR | VJ audio visualizer. `chladni.html` and `sander.html` are sub modes it opens in an iframe. |

Icons in the hub link to `tools/NAME/` and open in a new tab. Relative paths
only, no root absolute `/js/...` paths, so the site works from any subfolder.

## The hub

A phone home screen at narrow widths: status bar, a 2 x 4 icon grid, page
dots, a dock. From 600px the phone gets a bezel; from 900px the bezel goes
and the grid becomes a full screen 4 x 2 desktop.

Dock:

- **ABOUT** opens a Win9x style window with the tool list.
- **LANG** toggles Turkish and English. The chip in the status bar does the
  same. The choice is stored under the `marfo-lang` localStorage key and a
  Turkish browser defaults to Turkish.
- **RANDOM** opens one of the eight tools.

Keyboard: arrow keys, Home and End move between icons, Escape closes the
About window, Tab stays inside it while it is open.

### Design tokens

| Token | Value | Use |
| --- | --- | --- |
| `--desk` | `#008080` | Desktop field |
| `--dock` | `#3b9393` | Dock strip |
| `--face` | `#c0c0c0` | Window and button faces |
| `--light` / `--soft` / `--shadow` / `--dark` | `#fff` `#dfdfdf` `#808080` `#000` | The bevel rings |
| `--navy` / `--navy2` | `#000080` `#1084d0` | Title bar gradient, selection |
| `--ui` | Arimo | All interface type |
| `--px` | Silkscreen | The MARFO wordmark |

Icons are hand drawn 60 x 60 SVGs with `shape-rendering: crispEdges`, black
1 to 2px strokes and flat Win9x palette fills.

House style for copy: no em dashes. Break the sentence or use a comma.

## Translation

Any element with `data-tr="..."` carries its Turkish text in the attribute
and its English text as content. The script swaps them. When adding copy to
the hub, add both.

## Adding a tool

1. Drop the tool's folder under `tools/NAME/`.
2. Draw a 60 x 60 icon and save it as `tools/NAME/icon.svg`. Link it from the
   tool's `<head>` as `<link rel="icon" href="icon.svg" type="image/svg+xml">`.
3. Copy an `<a class="icon">` block in `index.html`, paste the icon's inner
   SVG, set `href`, `data-name` and the label.
4. Add a `<dt>` / `<dd>` pair to the About window, with a `data-tr` on the
   `<dd>`.
5. Update the two meta descriptions in `<head>`, the About copy and the
   `8 tools` status cell, which all spell the total out.
6. Regenerate `og.png` if the grid changes.

## Local preview

Any static server works, for example `npx serve .` or Python's
`http.server`. Open `http://localhost:PORT/`. The tools that use the camera or
microphone need `localhost` or HTTPS.
