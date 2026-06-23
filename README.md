# glass-demo

An interactive **liquid-glass lens** that follows your cursor (or touch) and refracts the wallpaper behind it. Pick the lens shape — **circle / triangle / rectangle** — from the tab at the top, and scroll to pan the wallpaper up and down.

[**Live demo**](https://tt-u.github.io/glass-demo/) · single file, no build, no dependencies.

## How the glass works

For each shape a small **displacement map** is generated on a canvas from the shape's **SDF** (signed distance field):

- inside the shape the background is sampled slightly **toward the centre** → gentle magnification;
- near the edge an extra push along the SDF **gradient (outward normal)** → the refractive glassy rim.

That map drives an SVG **`feDisplacementMap`** filter, applied as the element's **`backdrop-filter`**, so it warps whatever is rendered behind it. The element is `clip-path`-ed to the shape and gets a soft SVG outline as the rim. One code path, any shape — just swap the SDF function.

The lens is pinned to its own GPU layer (`translate3d` + `will-change`) and snaps to integer pixels when idle, to avoid `backdrop-filter` re-rasterization flicker.

## Run locally

```bash
# any static server, e.g.
python3 -m http.server 8000
# then open http://localhost:8000
```

## Credit

Wallpaper photo by **Alex Ning** on [Pexels](https://www.pexels.com/) (Pexels License).

🤖 Built with [Claude Code](https://claude.com/claude-code)
