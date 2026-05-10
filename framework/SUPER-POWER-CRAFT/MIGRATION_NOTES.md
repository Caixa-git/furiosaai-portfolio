# MIGRATION NOTES — SUPER POWER CRAFT v1.0 → v2.0

## 마이그레이션 필요 사항

v1.0에서 v2.0으로의 변경으로 인해 아래 항목에 영향을 받는다:

### 변경된 파일명

| v1.0 | v2.0 |
|:-----|:-----|
| `outputs/cycle-03/LAUNCH_DECISION.md` | `outputs/cycle-03/SALES_TEST_DECISION.md` |
| `outputs/cycle-03/LAUNCH_READINESS_GATE.md` | `outputs/cycle-03/SALES_TEST_READINESS_GATE.md` |
| `outputs/cycle-03/LAUNCH_SCORE.md` | `outputs/cycle-03/SALES_TEST_SCORE.md` |

### 변경된 표현 (문서 전반)

- "Launch Ready" → "Sales Test Ready"
- "Pre-Launch" → "Needs Polish"
- "Launch Status" → "Sales Test Status"
- "Launch Score" → "Sales Test Score"
- "Launch 최종 보고" → "Sales Test 최종 보고"

### README 변경 필요 섹션

- `## Launch Status` → `## Sales Test Status`

### outputs/INDEX.md 변경 필요

- Launch Readiness Artifacts → Sales Test Readiness Artifacts
- Launch Readiness gate 열 → Sales Test Readiness gate 열

## 마이그레이션 방법

기존 프로젝트가 없으므로(SUPER POWER CRAFT는 설계 단계) 실제 마이그레이션은 발생하지 않는다.
향후 적용 시 v2.0 명칭을 기준으로 사용한다.
