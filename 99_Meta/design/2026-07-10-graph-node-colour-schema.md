---
type: meta
title: Graph Node Colour Schema
status: approved
created: 2026-07-10
topic:
- topic/meta
wiki_role: meta
---

# Graph Node Colour Schema

Colour schema for graph-view nodes in **wiki-agents**. Colour marks the function
a note serves, not its rank. The schema groups nodes by top-level folder and
draws from a validated categorical palette.

Applied in `.obsidian/graph.json` under `colorGroups`. A backup of the prior
configuration sits at `.obsidian/graph.json.bak`.

---

## 1. Groups

| Group | Folders | Role | Hue | Hex | rgb integer |
|---|---|---|---|---|---|
| Maps | `50_MOCs` | Navigation hubs | Blue | `#2a78d6` | 2783446 |
| Concepts | `30_Concepts` | The ideas | Aqua | `#1baf7a` | 1814394 |
| Sources | `10_Sources` | External material | Yellow | `#eda100` | 15573248 |
| People | `20_People` | Thinkers, authors | Green | `#008300` | 33536 |
| Guides | `40_Guides` | How-to notes | Violet | `#4a3aa7` | 4864679 |
| In progress | `60_Drafts`, `70_Research` | Unfinished work | Red | `#e34948` | 14895432 |
| Meta | `99_Meta` | Vault machinery | Magenta | `#e87ba4` | 15236004 |
| Entry | `00_Home`, `00_Inbox` | Start points | Orange | `#eb6834` | 15427636 |

## 2. Rules

- Colour follows the folder, never the node's link count.
- The palette holds eight slots. A ninth group folds into an existing one rather
  than adding a hue.
- Blue serves Maps. The hue with the strongest separation marks the hubs.
- Red serves in-progress work. Drafts and Research read as "needs work".
- Templates and Attachments carry no colour. The graph filter `-path:90_Templates`
  hides templates; `showAttachments: false` hides attachments.

## 3. Validation

The palette passed the data-viz categorical checks on a light surface:

- Lightness band: pass, all eight inside L 0.43–0.77.
- Chroma floor: pass, all eight at or above 0.1.
- Colourblind separation: pass, worst adjacent pair ΔE 24.2 against a ≥12 target.
- Contrast: aqua, yellow, and magenta sit below 3:1 on a light surface. Node
  labels supply the relief, so meaning never rests on colour alone.

## 4. Obsidian configuration

```json
"search": "-path:90_Templates",
"colorGroups": [
  { "query": "path:50_MOCs", "color": { "a": 1, "rgb": 2783446 } },
  { "query": "path:30_Concepts", "color": { "a": 1, "rgb": 1814394 } },
  { "query": "path:10_Sources", "color": { "a": 1, "rgb": 15573248 } },
  { "query": "path:20_People", "color": { "a": 1, "rgb": 33536 } },
  { "query": "path:40_Guides", "color": { "a": 1, "rgb": 4864679 } },
  { "query": "path:60_Drafts OR path:70_Research", "color": { "a": 1, "rgb": 14895432 } },
  { "query": "path:99_Meta", "color": { "a": 1, "rgb": 15236004 } },
  { "query": "path:00_Home OR path:00_Inbox", "color": { "a": 1, "rgb": 15427636 } }
]
```
