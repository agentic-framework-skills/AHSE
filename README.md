# AHSE

**AUTONOMOUS HARDWARE & SOFTWARE PRODUCT SYNTHESIS ENGINE** — an agent-agnostic skill that,
from a single `INIT`, autonomously synthesizes a complete hardware/software product blueprint
(Design Thinking → 5W2H → Vision/Mission → HW/SW architecture → Lean MVP → simulation → final blueprint).

The skill is a self-contained system prompt in [`AHSE/SKILL.md`](AHSE/SKILL.md). It can be
loaded by any agent that supports system prompts — and ships first-class integration with the
[`skills`](https://github.com/vercel-labs/skills) CLI (`npx skills`).

---

## What it does

`AHSE` is a closed-loop, deterministic state machine. You trigger it with a single input —
**`INIT`** — and it executes **without any further user interaction**, running the full stage
pipeline (`STAGE-100` → `STAGE-700`) to a terminal code:

| Terminal code | Meaning |
|---|---|
| `STAGE-999: SUCCESS_DELIVERY` | The product passes Design Thinking, 5W2H, Vision/Mission, and Lean simulation, resulting in a production-ready HW/SW blueprint. |
| `BURNOUT-000: VIABILITY_COLLAPSE` | A fatal constraint (violation of physical laws, unresolvable BOM/unit economics, unresolvable power/compute ratio, or market irrelevance) that cannot be solved even after three simulated Lean pivots. |

The operator supplies the **product concept as conversation context**; the engine then produces
a single, flowing structured document: executive summary, full hardware BOM, software stack
diagram (ASCII/Markdown), 5W2H summary, and a deployment roadmap.

---

## Requirements

- Any agent capable of loading a system prompt (or the `skills` CLI).
- The product concept supplied by the operator as context.

---

## Installation

### One-shot (no install)

```bash
npx skills use agentic-framework-skills/AHSE
```

### Add to a project or agent

```bash
# Project-level
npx skills add agentic-framework-skills/AHSE
# Global / across agents
npx skills add agentic-framework-skills/AHSE -g --all
```

### Or load directly

Drop the contents of [`AHSE/SKILL.md`](AHSE/SKILL.md) as the system prompt for your agent.

---

## Usage

```
INIT                # lock inputs and synthesize the full blueprint (STAGE-100 → STAGE-700)
```

After `INIT`, the skill emits each stage in order (`STAGE-100`, `STAGE-200`, …, `STAGE-700`)
and terminates with either `STAGE-999: SUCCESS_DELIVERY` or
`BURNOUT-000: VIABILITY_COLLAPSE`.

---

## Stages produced after `INIT`

| Stage | Output |
|---|---|
| `STAGE-100` | Latent human need, target user persona & context, root problem statement. |
| `STAGE-200` | 5W2H Strategic Matrix (What, Why, Where, When, Who, How, How Much — cost/power/BOM). |
| `STAGE-300` | Vision statement + Mission statement. |
| `STAGE-400` | Hardware architecture (enclosure, MCU/SoC, sensors, power, connectivity, BOM) + software architecture (firmware, edge AI, cloud/API, UI/UX) + HW/SW integration boundary. |
| `STAGE-500` | 3 riskiest assumptions + MVP spec isolating the smallest viable HW + SW baseline. |
| `STAGE-600` | Build-Measure-Learn simulation; `PERSEVERE` / `PIVOT` (up to 3×) → `BURNOUT-000`. |
| `STAGE-700` | Final blueprint: executive summary, full HW BOM, software stack diagram, 5W2H summary, deployment roadmap. |

---

## Synthesis constraints

- **Deep rigor**: real, physically plausible component selections (ESP32-S3, nRF52840, STM32,
  Cortex-M4, LiDAR, IMU) and modern software stacks (FreeRTOS, Rust, WebSockets, Protobuf,
  PyTorch Edge) — no generic placeholders.
- **Lean simulation**: the MVP is stress-tested against physical, supply-chain, and value
  constraints; up to **3 pivots** before a hard stop.
- **Fatal stop**: any unresolvable physical/economic paradox immediately yields
  `BURNOUT-000: VIABILITY_COLLAPSE`.

---

## Author

Developed by **Jean Machuca** — [GitHub @jeanmachuca](https://github.com/jeanmachuca) ·
[Sponsor on GitHub Sponsors](https://github.com/sponsors/jeanmachuca).

---

## License

Distributed under the **MIT License** — the skill itself is MIT; the product blueprints it
generates are provided without warranty to you for any use.

---

## Repository layout

```text
AHSE/               # skill folder
  SKILL.md          # the system prompt (do not edit unless evolving the skill)
README.md           # this file (you are here)
LICENSE             # MIT
```

### Contributing

Develop in a topic branch: `git checkout -b feature/<topic> development` (or `fix/<topic>`,
`bugfix/<topic>`), then open a pull request into `development`. After review, promote to `main`
via a release PR and tag on `main`:
`git tag -a vMAJOR.MINOR.PATCH -m "…" && git push origin vMAJOR.MINOR.PATCH`. Prefer plain
`git pull` — **no rebasing**.
