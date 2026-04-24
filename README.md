# Architecture Workshops

> Interactive tooling for exploring, scoring, and prioritising modernisation across complex aviation software ecosystems.

**Live →** https://michalbojkogdansk.github.io/architecture-workshops/

---

## What this is

A browser-based planning tool for aviation software architects working on modernisation programmes. It maps a system's modules across architectural layers, scores each one across multiple strategic dimensions, and lets you dynamically filter and prioritise based on what matters most to your current initiative.

Built as a standalone static site — no server, no build step, no framework. Just open the URL.

---

## Views

| View | What it shows |
|---|---|
| **Architecture** | All modules across their architectural layers, colour-coded by any selected dimension |
| **Dependency graph** | D3 force-directed network of the strongest inter-module dependencies |
| **Priority matrix** | 2D scatter: complexity vs revenue impact, bubble size and colour by selected dimension |

---

## Dimensions

Each module is scored 1–5 across six strategic dimensions:

| Dimension | Question it answers |
|---|---|
| **Revenue impact** | How critical is this to the product's commercial value? |
| **Modernisation complexity** | How hard is it to change — technically and regulatorily? |
| **Incrementality** | How easily can work be split into very small, safe deliveries? |
| **Regulation level** | How tightly constrained by certification standards? |
| **Customer impact** | How directly will customers feel any change here? |
| **AI SDLC applicability** | Where can AI tooling (Copilot, LLM testing, code gen) genuinely accelerate delivery? |

### Computed scores

```
ROI score    = (revenue_impact × incrementality) / mod_complexity
AI win score = (ai_sdlc × incrementality) / mod_complexity
```

---

## Quick filter presets

| Preset | Logic |
|---|---|
| **Highest ROI** | Revenue ≥ 4, Incrementality ≥ 4 |
| **AI SDLC quick wins** | AI score ≥ 4, Incrementality ≥ 4 — lowest-risk places to introduce AI-assisted development |
| **Low customer risk** | Minimal customer-facing exposure — good for building team confidence with new tooling |
| **High regulation** | Surfaces the heavily certified modules — plan these last or in isolation |

---

## Adapting to a different system

1. Edit `data/modules.js` — replace module entries with your system's components
2. To add a new scoring dimension, add a field to each module object, then add one entry to the `DIMS` array in `index.html`

```js
// data/modules.js
{ id: "my_module", ..., team_ownership: 2, build_vs_buy: 4 }

// index.html — DIMS array
{ id: 'team_ownership', label: 'Team ownership clarity', color: '#e879f9' }
```

The UI — all three views, filters, detail panel — adapts automatically.

---

## GitHub Pages setup

Already configured. Any push to `main` updates the live site within ~30 seconds.

To use this template for a different system:
1. Fork the repo
2. Replace `data/modules.js` with your architecture data
3. Enable Pages under Settings → Pages → Source: `main` / root

---

## Roadmap ideas

- [ ] Export filtered view as CSV / JSON
- [ ] Gantt-style roadmap ordered by dependency topology
- [ ] Team assignment per module
- [ ] Score history tracking (before vs after modernisation)
- [ ] Jira / Linear integration for converting modules to epics
