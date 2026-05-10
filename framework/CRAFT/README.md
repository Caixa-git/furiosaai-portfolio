# CRAFT Framework v1.0 — Code Review, Audit, Fix, and Triage

> **Single-agent autonomous delivery pipeline.**  
> 1 message → auto-execute → report. Zero unnecessary interrupts.  
> Paper-grounded at every layer. 19+ academic papers, ~35,000+ collective citations.

## Naming Basis (Academic)

| Criterion | Source | Score |
|:----------|--------|:-----:|
| Conciseness | Deissenboeck & Pizka (2005) IEEE TSE | 5 chars |
| Meaningfulness | Deissenboeck & Pizka (2005) | 'craft' = skilled making |
| Comprehensibility | Lawrie et al. (2006) IEEE ICPC | Real word, not opaque |
| Mental model | Spinellis (2012) IEEE Software | 'Craft your code' |
| Uniqueness | N/A | No major SE framework named CRAFT |

## Core Value

> 최소 사용자 개입, 최대 학술적 검증.

## Architecture (9 Layers)

```
Layer 0: User Interface
  단일 메시지 "CS-NN: title" → 모든 것 시작
  ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Layer 1: Task Size Detection
  🟢 Small (direct)     → no Plan Review, no dispatch
  🟡 Medium (1-2 tasks) → Code Review only
  🟠 Medium-Complex     → Plan Review + Code Review
  🔴 Large              → decompose to Medium

Layer 2: Plan Review (CRITICALITY)
  CRITICALITY = S × I × U × (1 + D)
    S: Severity (1-3)
    I: Irreversibility (1-3)
    U: User Impact (1-3)
    D: Discovery Bonus (0 = plan, +0.5 = dev, +1 = review, +2 = prod)
  ≥18 → 🔴 Must fix  9-17 → 🟡 Can proceed  <9 → 💭 Note only
  Max 3 rounds. 3rd fail → force proceed with ≥18 fixes only.

Layer 3: Code Review (Dispatch Isolation)
  → Independent subagent session (bias prevention)
  → Bacchelli & Bird (2013) independent reviewer
  → Coverage metrics in summary

Layer 4: 🔒 Security Scan
  → python3 scripts/security_scan.py --block
  → Meli et al. (2019) TruffleHog + OWASP patterns
  → Scans: GitHub tokens, AWS keys, private keys, PII, .env, etc.
  → 🔴 CRITICAL = push blocked. 🟡 WARNING = report only.

Layer 5: Git Workflow (Feature Branch)
  git checkout -b cs-NN/kebab-name
  → develop → commit → push → PR
  → merge --no-ff to main → delete branch
  → Humble & Farley (2010) Continuous Delivery

Layer 6: Definition of DoD
  ✅ Plan Review pass   ✅ Security scan pass   ✅ Code Review pass
  ✅ All commits pushed ✅ main merged           ✅ Pages deployed
  🟡 Tests written      💭 Docs updated

Layer 7: Technical Debt Registry
  CRIT < 18 findings → TECH_DEBT.md auto-appended
  Sheikhaei & Tian (2023), Fowler (2009)

Layer 8: User Intervention Protocol
  4 conditions ONLY block the user:
    1. CRITICALITY ≥ 18
    2. 3 Plan Reviews all failed
    3. No GitHub repo configured
    4. Data loss risk
  Everything else → report only. Never interrupt.
  Sheridan (1978) LOA 6-7, Amershi et al. (2019) G12/G17

Layer 9: Self-Critique Protocol (Meta-Review)
  Every paper-based proposal auto-validated with FIRE filter:
    F — Findings replicated? (Open Science 2015)
    I — Is context matched? (Yarkoni 2022)
    R — Rival explanations? (Ioannidis 2005)
    E — Evidence convergence? (Munafò 2017)
  → HIGH / MEDIUM / TENTATIVE confidence labels
```

## Key Papers

| # | Paper | Citations | Layer |
|:-:|-------|:---------:|:-----:|
| 1 | Humble & Farley (2010) Continuous Delivery | 5,000+ | Git, DoD |
| 2 | Bacchelli & Bird (2013) Code Review | 2,000+ | Code Review |
| 3 | Boehm (1991) Spiral Model / TRW | 30,000+ | Plan Review |
| 4 | McConnell (2006) Code Complete | 10,000+ | Size, DoD |
| 5 | Meli et al. (2019) TruffleHog | 500+ | Security |
| 6 | OWASP Top 10 (2021) | — | Security |
| 7 | Fowler (2009) Technical Debt | 5,000+ | Tech Debt |
| 8 | Sheridan (1978) Levels of Automation | 5,000+ | Intervention |
| 9 | Amershi et al. (2019) Human-AI Guidelines | 1,000+ | Intervention |
| 10 | Wang & Wang (2026) Observability Gap | — | Notifications |
| 11 | Ioannidis (2005) Why Most Findings Are False | 30,000+ | Self-Critique |
| 12 | Open Science Collab (2015) Reproducibility | 10,000+ | Self-Critique |
| 13 | Munafò et al. (2017) Reproducible Science | 2,000+ | Self-Critique |
| 14 | Fanelli (2010) Publication Pressure | 2,000+ | Self-Critique |
| 15 | Yarkoni (2022) Generalizability Crisis | 800+ | Self-Critique |
| 16 | Kitchenham et al. (2002) SE Guidelines | 1,000+ | Self-Critique |
| 17 | Sheikhaei & Tian (2023) Automated SATD | 50+ | Tech Debt |
| 18 | Deissenboeck & Pizka (2005) Naming | 200+ | Naming |
| 19 | Lawrie et al. (2006) Identifier Naming | 500+ | Naming |
| 20 | Spinellis (2012) Naming is a Choice | 100+ | Naming |

## Quick Start

```bash
# 1. User sends:
CS-01: Add search debounce

# 2. CRAFT auto-executes:
#    ✓ Size detection → Small (direct)
#    ✓ Dev + commit + push
#    ✓ Security scan → clean
#    ✓ Code Review → dispatch
#    ✓ Merge + deploy

# 3. Response:
✅ CS-01 완료. (45s)
   📊 debounce 300ms → 200ms
   🔄 Code Review clean
   🚀 main @ a1b2c3d
```

## Known Gaps

CRAFT covers **Implementation → Deploy** only. For full product lifecycle, see [POWER CRAFT](../POWER-CRAFT/README.md):
- **P**roduct Discovery — What to build?
- **O**perations — How to run?
- **W**atch — How to test?
- **E**valuation — Does it work?
- **R**eliability — Is it stable?
