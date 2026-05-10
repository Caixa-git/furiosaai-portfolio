# POWER CRAFT Framework — Design Spec v1.0

> CRAFT Core (9 layers) + Product Discovery · Operations · Watch · Evaluation · Reliability
>
> **Total papers:** 31+  
> **Collective citations:** ~50,000+  
> **Full product lifecycle:** Discovery → Build → Test → Deploy → Run → Evaluate

## Architecture

```
Pre-Build:
  P — Product Discovery  ─── Ries(2011) Lean Startup · Kano(1984) · Torres(2021)
       ↓ CS-NN task queue

Build:
  CRAFT Core (9 layers)  ─── 20 papers
       ↓ delivered code

Intra-Build:
  W — Watch (Testing)    ─── Fraser(2011) EvoSuite · Schäfer(2023) LLM tests
       ↓ tested code

Post-Deploy:
  O — Operations         ─── Beyer(2016) SRE · Forsgren(2018) DORA · Majors(2021)
       ↓ monitoring data

Cross-Cutting:
  E — Evaluation         ─── Bland(2019) experiment validation
  R — Reliability        ─── Basiri(2016) chaos engineering
```

## New Layers Detail

### 1. Product Discovery (P)
- **What:** User problem → structured CS-NN task queue
- **When:** Before any CRAFT execution
- **Trigger:** Vague user request
- **Process:** Kano decomposition → hypothesis design → CS-NN queue
- **Papers:** Ries, Maurya, Kano, Torres, Bland, Gothelf (6 papers, ~30,000+ citations)
- **FIRE:** HIGH
- **User block:** ⚠️ Yes (needs problem input)

### 2. Watch/Testing (W)
- **What:** Auto-generate and execute tests for all new code
- **When:** After Code Review (L3), before Security (L4)
- **Trigger:** Every CS-NN completion
- **Process:** LLM test gen → execute → coverage gate → ≥70% pass
- **Papers:** Fraser, Schäfer, Beck, Jia, Zhu (5 papers, ~15,000+ citations)
- **FIRE:** HIGH
- **User block:** ✅ Auto (failures = 🔴 blocker, warnings = 🟡 report)

### 3. Operations (O)
- **What:** Monitor deployed service, detect anomalies, auto-create recovery tasks
- **When:** After deploy, continuously
- **Trigger:** Health check failure / metric anomaly
- **Process:** Health check → anomaly detection → incident → CS-HOTFIX
- **Papers:** Beyer, Majors, Forsgren, Sridharan, Basiri (5 papers, ~9,000+ citations)
- **FIRE:** HIGH
- **User block:** ⚠️ Yes (only critical incidents)

## CRAFT Core (9 layers, unchanged)

| # | Layer | Function | Auto? |
|:-:|-------|----------|:-----:|
| 0 | User Interface | CS-NN → execution | Interrupt |
| 1 | Task Size Detection | Small/Medium/Complex/Large | ✅ |
| 2 | Plan Review | CRITICALITY(S×I×U×(1+D)) | ✅ |
| 3 | Code Review | Dispatch isolation | ✅ |
| 4 | Security Scan | Secret detection | ✅ |
| 5 | Git Workflow | Feature branch → merge | ✅ |
| 6 | Definition of DoD | 4✅ + 2🟡/💭 checklist | ✅ |
| 7 | Tech Debt Registry | AUTO_DEBT.md logging | ✅ |
| 8 | User Intervention | 4 conditions only | ✅ |
| 9 | Self-Critique | FIRE filter on proposals | ✅ |

## Comparison: CRAFT vs POWER CRAFT

| Dimension | CRAFT v1.0 | POWER CRAFT v1.0 |
|-----------|:----------:|:-----------------:|
| **SDLC Coverage** | Implementation → Deploy | **Discovery → Run** |
| **Papers** | 20 | 31+ |
| **Layers** | 9 | **12** (9+3) |
| **Auto layers** | 8/9 | **11/12** |
| **User interrupts** | 4 conditions | **5** (+ Discovery input) |
| **Testing** | Manual Code Review | **Auto test gen + execution** |
| **Operations** | ❌ None | **SRE monitoring + DORA** |
| **Product awareness** | ❌ None | **Kano + Lean Startup** |

## Known Limitations

1. **Discovery is human-dependent** — user must supply problem statement
2. **Testing needs runtime** — Node/Python test runner must be available
3. **Operations is monitoring-only** — no auto-scaling, no auto-remediation
4. **Cross-cutting E+R are design intent** — not yet implemented as code
5. **FIRE self-critique has R gap** — all 3 layers lack contradictory papers due to search restrictions

## Path to Implementation

```
v1.0 → Design spec (THIS DOCUMENT)
v1.1 → Scripted test gen (Python/Node agent)
v1.2 → Health check cron + incident auto-task
v1.3 → DORA metric tracking
v1.4 → Kano-based decomposition prompt
v1.5 → Full POWER CRAFT named release
```
