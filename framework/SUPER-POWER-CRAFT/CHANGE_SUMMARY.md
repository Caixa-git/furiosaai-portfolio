# SUPER POWER CRAFT v2.0 — 변경 요약

## 개요

SUPER POWER CRAFT v1.0 (Launch Ready 프레임워크) → v2.0 (Sales Test Readiness 프레임워크)

## 주요 변경 사항

| 항목 | v1.0 (이전) | v2.0 (변경) |
|------|:-----------|:------------|
| **핵심 정의** | 제품 출시 가능 여부 판정 | Sales Test Readiness 점검 — "고객에게 영업 테스트를 해볼 만한 상태" |
| **판정 표현** | Launch Ready / Pre-Launch / Not Ready | Sales Test Ready / Needs Polish / Not Ready |
| **Gate 이름** | Launch Readiness Gate | Sales Test Readiness Gate |
| **점수 이름** | Launch Score | Sales Test Score |
| **Decision 파일** | LAUNCH_DECISION.md | SALES_TEST_DECISION.md |
| **README Status** | Launch Status | Sales Test Status |
| **3 Cycle 근거** | 논문 기반 최적값 | **운영 상한** — 비용/토큰 방지 |
| **AI 평가 위상** | 판정 주체 | **사전 점검** — 실제 검증은 고객 반응 |
| **Launch Score 의미** | 출시 예측 점수 | **의사결정 보조 체크리스트** |
| **App Store 분리** | 혼재 | **STORE POWER CRAFT로 완전 분리** |
| **논문 인용** | 과도 | 실무 체크리스트 중심 (배경 참고만) |
| **"할 수 없는 일"** | 없음 | 명시적 리스트 추가 |
| **실제 검증 지표** | 없음 | DM 답장률, 전환율 등 구체적 예시 |

## 유지된 항목 (변경 없음)

- Cycle 01/02/03 구조
- Product Value Gate (6항목, 5/6 통과)
- Sales Readiness Gate (6항목, 5/6 통과)
- Scope Control (P0≤3, P1≤3, P2 기록)
- Stop Conditions 10개
- BLOCKER_REPORT.md 형식
- outputs/INDEX 확장 규칙
- 채팅 짧은 보고 형식
- CRAFT / POWER CRAFT 역할 유지

## 영향

- 기존 v1.0 문서와의 하위 호환성: ❌ **호환되지 않음** (판정명, Gate명, Decision 파일명 변경)
- POWER CRAFT에 미치는 영향: ❌ 없음 (유지)
- STORE POWER CRAFT와의 관계: ✅ 분리됨
