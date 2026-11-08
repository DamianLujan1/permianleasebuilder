# Permian Lease Builder

**Well Pad, Flow Lines & Tank Battery**: a browser-based 3D oilfield construction game set in the Permian Basin.

You take tickets off a job board. Each job ties a lease's wells into one central tank battery (CTB), or has you run that battery. Production flows **well pad → test site → CTB**:

1. **Test site.** You set it on open ground outside the battery fence, out by the pads. It's a 6-slot test manifold with 3-way valves, a 3-phase test separator and a meter run on a gravel pad, and it costs $98,000.
2. **Flow lines.** You dig from each wellhead flag stake to a tile beside the test site, then Lay Pipe. The first ~90 ft off each wellhead (14 tiles) is welded steel. A transition coupling follows, and flexpipe runs the rest of the way into the manifold.
3. **Bulk line.** You dig from another tile beside the test site to a tile beside the CTB header and Lay Pipe again, which strings flexpipe the whole way. A header takes up to 4 incoming lines, one per test site.
4. **Battery.** You backfill, set and connect the vessels (separators, heater treater, tanks, VRU, LACT, gas sales meter or flare), and commission the battery for operations.

A well counts as tied in only when its line ends at a test site that has its own bulk line to the CTB. If a pad ditch touches the bulk-line ditch, the wells would bypass the test site. The checklist flags that, and Lay Pipe refuses to string a bypass. Saves made before test sites existed keep their old direct tie-ins. The work has to stay inside the job's budget and route around obstacles such as caliche pits, power poles, pipeline right-of-way and lease roads.

## Running it

The whole game is one self-contained `index.html`. three.js is bundled inline, so it needs no build step, dependencies or network requests.

- **Locally:** open `index.html` in a browser, or serve the folder (`python3 -m http.server`).
- **Hosting:** any static host works. On Vercel, use framework preset "Other", no build command and the repo root as the output directory.

## Controls

| Input | Action |
| --- | --- |
| `1`–`7` | Tools: Camera, Dig Ditch, Lay Pipe, Backfill, Build Battery, Connect Lines, Delete |
| Left-drag | Use the current tool (orbit in Camera mode) |
| Right-drag | Orbit |
| Middle-drag / Shift+Right-drag / `WASD` | Pan |
| Wheel | Zoom |
| `Q` / `E` | Rotate camera |
| `R` | Rotate equipment |
| `Esc` | Cancel |
| `Ctrl+Z` | Undo |
| `Space` | Pause operations |
| `H` | Help |
| `P` | Photo mode |
| `T` | Hide toolbar |

## Provenance

`index.html` was pulled from the Vercel project `oilfield-battery-builder`, production deployment `dpl_DXmSSds7NRkLmyBh5CHqFHSVNDh2` (the latest of 12 deployments). As imported, the file was byte-identical to the deployed source: SHA-1 `09440a78d78ffc14e991ea7c6dd010d71c34046d`, matching Vercel's content hash for that file. The deployment held this one file only, with all of its JavaScript minified, and no unminified source was part of it.

## Code layout

Everything lives in one `<script>`: an esbuild bundle of three.js, its OrbitControls, and the game. The three.js part stays minified. The game logic starts at `function Mr(n, t)` (tile terrain lookup) and is pretty-printed so it can be edited and reviewed. Local variable names are still the short ones the minifier picked. That reformat changed no behavior: running `esbuild --minify-whitespace` on the old and new scripts gives identical output.
