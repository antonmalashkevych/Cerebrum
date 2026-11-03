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
