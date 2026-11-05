# Cerebrum Canvas

Interactive 3D prototype of the Cerebrum visualization for Kinetic (VisiQuate).

Open `index.html` in a browser. Single file, no build step, no external assets beyond Google Fonts.

What it contains:
- 7,452 neurons in four lobes (Grounding, Governance, Agent, Executable) on a sample catalog shaped like the live one
- Orbit / pan / zoom camera, click a lobe to open it, Esc to go back, R to reset
- Three layers of cross-lobe paths (trunk bundles, kind-to-kind tracts, individual fibers) with continuous impulses
- Pulsing regions, ingress packets with entry sparks, nebula aura with event-driven emanations
- Original synthesized ambient score with per-impulse grains (Web Audio, on by default after first gesture)
- Real-time growth model: 4 neurons and 9 synapses per week, compounding 0.4% per week from 2026-10-29
- Scenes: Resting state, A thought, Diagnostic cascade, The gate, Neurogenesis, A year of growth

## drill/

A separate build that keeps the demo above as the entry layer and adds a drill-through to the real catalog.
Open `drill/index.html`. Click a lobe, then scroll in, press Enter or double-click to open the data layer:
a Family → Kind → Data product Sankey, kind chips, a filterable node table and neighbours. Esc returns to the brain.

Engineers wire real data with one call, in this shape:

```js
window.Cerebrum.setData({
  nodes:     [{id, name, kind, family, plane, product, scope:'client'|'global', status:'governed'|'draft', updated:'YYYY-MM-DD'}],
  kindEdges: [{a: kindName, b: kindName, n}],
  products:  [{key, name}]
});
```

`window.Cerebrum.openLobe(i)` opens a lobe programmatically (0 Grounding, 1 Governance, 2 Agent, 3 Executable).

### Loader (drill build)

`window.Cerebrum.loader.show(title, subtitle)` and `.hide()` show a close-up neuron animation (dendrites and axon growing,
impulses travelling, the view pulling back, synapses forming with other neurons). Use it while the catalog is loading or
a request is slow; the drill build shows it on first paint and while a lobe's data is being read.

### Sankey impulses (drill build)

Each ribbon has a centerline cubic; an impulse is an SVG `<circle class="imp">` with `offset-path: path("…")` and a CSS
`offset-distance` animation from 0% to 100%, removed on `animationend`. About one every 1 to 2 seconds, weighted by ribbon
width, limited to the selected kind when one is chosen. `window.Cerebrum.sankeyPulse.fire(kindName?)` fires one on demand,
so an archetype run can light the ribbons it actually touched. Disabled under `prefers-reduced-motion`.

## Light theme

Both builds are dark-first and switch to a light palette when Kinetic sets `data-theme="light"` on the root element,
when the OS prefers light and no `data-theme` is set, or with `?theme=light` on the URL for review. Only colors, gradients,
blend modes and the aura change; layout and behavior are identical. Light has its own palette: Grounding teal #0E9A8D, Governance amber #E09A0A,
Agent magenta #C2379B, Executable cobalt #2F5FD6: crisp hard-edged dots, ring-style firing, pastel aura in multiply, subtle slate impulses.

### Light preview and token sheet

`drill/light/index.html` shows the drill build in the light theme (it loads `../index.html?theme=light`, so there is
one source of truth). On GitHub Pages: `/Cerebrum/drill/light/`. Every dark and light color, opacity and blend rule is
listed in `docs/cerebrum-theme-tokens.xlsx`.
