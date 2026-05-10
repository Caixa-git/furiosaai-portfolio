# SUPER POWER CRAFT Framework v2.0

> Sales Test Readiness — 작은 제품 아이디어를 최대 3 Cycle 안에 정리해, 실제 고객에게 영업 테스트를 해볼 만한 상태인지 점검하는 프레임워크

---

## 1. 정의

SUPER POWER CRAFT는 **제품 성공을 예측하는 프레임워크가 아니다.**

```
작은 제품 아이디어를 최대 3 Cycle 안에 정리해,
실제 고객에게 영업 테스트를 해볼 만한 상태인지 점검하는
Sales Test Readiness 프레임워크다.
```

### SUPER POWER CRAFT가 할 수 있는 일

- 웹 데모 또는 포트폴리오를 고객에게 보여줄 수 있게 정리
- 첫 화면 가치 제안 점검
- 타겟 고객 명확화
- 무료 샘플/무료 진단 제안 준비
- 유료 패키지 가격 정리
- 영업 DM/전화 문구 준비
- 위험 기능 제거
- 사용자 다음 액션 제안

### SUPER POWER CRAFT가 할 수 없는 일

- 제품 성공 예측
- 시장 적합성 확정
- 실제 구매 의사 보장
- 앱스토어 심사 통과 보장
- 고객 반응 없는 PMF 판정

**AI의 Gate 평가는 사용자에게 보여주기 전 사전 점검이다.** 실제 검증은 고객 반응으로만 가능하다.

실제 검증 지표 예시:
- DM 답장률
- 무료 샘플 요청 수
- 실제 상담 전환 수
- 결제 의사
- 첫 유료 고객
- 반복 구매 또는 월 관리 전환

---

## 2. 역할 분리

```
CRAFT:
  작은 작업을 빠르게 끝내는 최소 실행 프레임워크

POWER CRAFT:
  GitHub / Live Demo / QA / 문서까지 갖춘 포트폴리오 개발 프레임워크

SUPER POWER CRAFT:
  최대 3 Cycle 안에 제품을 영업 테스트 가능한 상태로 정리하는
  Sales Test Readiness 프레임워크

STORE POWER CRAFT: (별도 프레임워크)
  App Store / Google Play 제출 준비를 위한 Store Submission Readiness 프레임워크
```

---

## 3. 지원 모드

| 모드 | Cycle | 용도 |
|------|:-----:|------|
| 기본 모드 | 1 | POWER CRAFT와 동일 — 단순 개발 |
| Launch Ready 모드 | 최대 3 | Sales Test Readiness 판정 |

기본 모드는 POWER CRAFT와 동일하게 작동한다. (GitHub Feature Branch, Persona dispatch, Final Sync Gate, Security Scan 등 전부 유지)

Launch Ready 모드는 사용자가 명시적으로 요청할 때만 작동한다:

```
이 프로젝트는 SUPER POWER CRAFT로 진행해줘.
최대 3 Cycle 안에 Sales Test Ready 상태인지 판정해줘.
```

---

## 4. Cycle 구조

### Cycle 01 — MVP Build

| 항목 | 내용 |
|------|------|
| **목표** | 실행 가능한 최소 제품을 만든다 |
| **중점** | 핵심 기능 구현, 기본 UI, 샘플 데이터, README, Live Demo, QA |
| **완료 기준** | 사용자가 직접 눌러볼 수 있고, 핵심 기능이 최소 1개 이상 정상 동작한다 |
| **적용 Gate** | Final Sync Gate, Persona Usage Gate |
| **자동 진행 조건** | MVP 실행 가능 → Cycle 02. MVP 실행 불가 → hotfix 1회, 실패 시 BLOCKER_REPORT.md |

### Cycle 02 — Product Fit Polish

| 항목 | 내용 |
|------|------|
| **목표** | 비개발자 또는 실제 사장님이 30초 안에 제품 가치를 이해하게 만든다 |
| **중점** | 첫 화면 가치 제안, 결과물 품질, Before/After, 가격 패키지 초안, 무료 제안, 불필요한 기능 제거 |
| **완료 기준** | 이 제품이 누구에게 어떤 결과를 주는지 명확하다 |
| **적용 Gate** | Final Sync Gate, Persona Usage Gate, Product Value Gate, Sales Readiness Gate |
| **자동 진행 조건** | Gate 통과 → Cycle 03. Gate 부분 실패 → Cycle 02b hotfix 1회. 제품 가치 불명확 → BLOCKER_REPORT.md |

### Cycle 03 — Sales Test Ready

| 항목 | 내용 |
|------|------|
| **목표** | 실제로 링크를 보내고 반응을 볼 수 있는 상태로 정리한다 |
| **중점** | Live Demo 안정성, README 허브, DEMO_SCENARIO, PORTFOLIO_SUMMARY, 영업용 문구, 가격 패키지, 무료 진단/샘플 제안, SALES_TEST_DECISION.md 작성 |
| **완료 기준** | 외부 고객에게 보여줄 수 있고, 사용자가 실제 영업 테스트를 시작할 수 있다 |
| **주의** | Cycle 03에서는 대형 신규 기능을 추가하지 않는다. 출시 준비, 문서, QA, 영업 문구, 가격 패키지, Live Demo 안정화에 집중한다 |
| **적용 Gate** | Final Sync Gate, Persona Usage Gate, Product Value Gate, Sales Readiness Gate, Naruhodo Legal Review Gate, Sales Test Readiness Gate, Sales Test Score, SALES_TEST_DECISION.md |

---

## 5. Gate

### Product Value Gate

권장 위치: `outputs/cycle-02/PRODUCT_VALUE_GATE.md`, `outputs/cycle-03/PRODUCT_VALUE_GATE.md`

| 항목 | 결과 | 근거 |
|------|:----:|------|
| 첫 화면에서 무엇을 해주는 제품인지 보이는가 | 통과/부분/실패 | |
| 타겟 사용자가 명확한가 | 통과/부분/실패 | |
| 해결하는 문제가 명확한가 | 통과/부분/실패 | |
| 결과물이 사용자가 바로 쓸 수 있는가 | 통과/부분/실패 | |
| 기능 설명보다 결과/효과 중심인가 | 통과/부분/실패 | |
| 돈 낼 이유가 보이는가 | 통과/부분/실패 | |

**통과 기준:** 6개 중 5개 이상 통과

> 이 기준은 과학적 기준이 아니라 실무 점검 기준이다.

### Sales Readiness Gate

권장 위치: `outputs/cycle-02/SALES_READINESS_GATE.md`, `outputs/cycle-03/SALES_READINESS_GATE.md`

| 항목 | 결과 | 근거 |
|------|:----:|------|
| 무료 샘플/무료 진단 제안이 있는가 | 통과/부분/실패 | |
| 유료 패키지 가격이 명확한가 | 통과/부분/실패 | |
| 사장님에게 보낼 DM/전화 문구가 있는가 | 통과/부분/실패 | |
| Before/After 또는 개선 예시가 있는가 | 통과/부분/실패 | |
| 첫 고객에게 제안할 최소 상품이 정의되어 있는가 | 통과/부분/실패 | |
| 유지보수 부담이 과도하지 않은가 | 통과/부분/실패 | |

**통과 기준:** 6개 중 5개 이상 통과

### Naruhodo Legal Review Gate

권장 위치: `outputs/cycle-03/NARUHODO_LEGAL_REVIEW_GATE.md`

> ⚖️ 법적 리스크가 감지되면 `hermes-naruhodo` 스킬을 통해 자동 검토.
> 스킬이 로드되지 않은 환경 → `GATE_SKELETON.md` 참조하여 수동 점검.
> 전체 게이트 문서: `Caixa-git/hermes-naruhodo` (private), SKILL.md Section 3(호출 기준), Section 18(프레임워크 참조).

| # | 항목 | 결과 | 근거 |
|:-:|:-----|:----:|:------|
| 1 | 실제 고객 데이터 사용 여부 | 통과/검토필요 | |
| 2 | 개인정보/민감정보 포함 여부 | 통과/검토필요 | |
| 3 | API 키/토큰/비밀키 노출 여부 | 통과/검토필요 | |
| 4 | 오픈소스 라이선스 고지 필요 여부 | 통과/검토필요 | |
| 5 | 이미지/폰트/아이콘 출처 확인 필요성 | 통과/검토필요 | |
| 6 | AI 생성물 사용 범위 확인 | 통과/검토필요 | |
| 7 | 서비스명/상표 충돌 가능성 | 통과/검토필요 | |
| 8 | 저작권 등록 권고 여부 | 통과/검토필요 | |
| 9 | 계약서/약관/개인정보처리방침 필요 여부 | 통과/검토필요 | |
| 10 | 판매/납품/유료 서비스 리스크 | 통과/검토필요 | |
| 11 | 앱스토어/플레이스토어 제출 리스크 | 통과/검토필요 | |

**통과 기준:** 11개 전부 "통과". 하나라도 "검토필요"면 Naruhodo 스킬 호출.

**실행 규칙:**
```text
- naruhodo-legal-review Hermes 스킬 로드 확인
- 로드됨 → skill_view('naruhodo-legal-review') 후 자동 검토
- 로드 안 됨 → 사용자에게 "법적 리스크 검토가 필요합니다" 알림 + GATE_SKELETON.md 참조 요청
- 검토 완료 후 Gate 통과/보류 기록
```

### Sales Test Readiness Gate

기존 Launch Readiness Gate에서 변경. 권장 위치: `outputs/cycle-03/SALES_TEST_READINESS_GATE.md`

| 항목 | 결과 | 근거 |
|:-----|:----:|:------|
| GitHub Repo public | 통과/실패 | |
| Live Demo 정상 접근 | 통과/실패 | |
| Live Demo에서 핵심 기능 실제 동작 | 통과/실패 | |
| README 최신화 | 통과/실패 | |
| outputs/INDEX 최신화 | 통과/실패 | |
| 태그 최신화 | 통과/실패 | |
| 민감정보 없음 | 통과/실패 | |
| 위험 기능 없음 | 통과/실패 | |
| DEMO_SCENARIO 있음 | 통과/실패 | |
| PORTFOLIO_SUMMARY 있음 | 통과/실패 | |
| 가격 패키지 있음 | 통과/실패 | |
| 영업 문구 있음 | 통과/실패 | |
| 사용자 다음 액션 명확함 | 통과/실패 | |

**판정 기준:**

| 통과 개수 | 판정 |
|:---------:|:-----|
| 11개 이상 | Sales Test Ready |
| 8~10개 | Needs Polish |
| 7개 이하 | Not Ready |

> 이 판정은 영업 테스트 준비 상태를 의미한다. 실제 판매 성공을 의미하지 않는다.

---

## 6. Sales Test Score

기존 Launch Score에서 변경. 권장 위치: `outputs/cycle-03/SALES_TEST_SCORE.md`

| 항목 | 점수 | 근거 |
|:-----|:---:|:------|
| 문제 명확성 | 0~10 | |
| 타겟 명확성 | 0~10 | |
| 첫 화면 설득력 | 0~10 | |
| 기능 동작 안정성 | 0~10 | |
| 결과물 품질 | 0~10 | |
| 가격 제안 명확성 | 0~10 | |
| 영업 문구 준비 | 0~10 | |
| 유지보수 부담 낮음 | 0~10 | |
| 리스크 낮음 | 0~10 | |
| Live Demo 완성도 | 0~10 | |

**판정:**

| 점수 | 판정 |
|:---:|:-----|
| 80점 이상 | Sales Test Ready 후보 |
| 60~79점 | Needs Polish |
| 59점 이하 | Not Ready |

> Sales Test Score는 성공 예측 점수가 아니라 의사결정 보조 체크리스트다. 점수가 높아도 실제 판매 성공을 보장하지 않는다. 점수가 낮아도 특정 고객에게 팔릴 수 있다.

---

## 7. Sales Test Decision

기존 LAUNCH_DECISION.md에서 변경. 권장 위치: `outputs/cycle-03/SALES_TEST_DECISION.md`

```md
# Sales Test Decision

## 1. 최종 판정

- Sales Test Ready / Needs Polish / Not Ready

## 2. 판정 이유

## 3. 실제로 팔 수 있는 상품명

## 4. 타겟 고객

## 5. 첫 제안 가격

## 6. 무료 제안 문구

## 7. 유료 전환 문구

## 8. Live Demo 링크

## 9. GitHub Repo 링크

## 10. 검토자가 먼저 볼 파일

## 11. 영업 테스트 전 남은 작업

## 12. 개발 종료 여부

- 종료 / 1회 보완 / 방향 재검토

## 13. 사용자 다음 액션

예:
- 인스타/네이버 플레이스 운영 가게 30곳 리스트업
- 무료 진단 DM 20건 발송
- 반응률 기록
- 유료 전환 시도

## 14. Next Path

- Sales Outreach
- Web Landing Page
- Store Submission Track
- Not Recommended Yet
```

---

## 8. 3 Cycle 제한의 의미

```
3 Cycle은 이론적 최적값이 아니다.
AI가 무한 개선에 빠지지 않도록 막는 운영 상한이다.
```

목적:
- 비용 폭주 방지
- 토큰 소비 방지
- 기능 추가 욕심 방지
- "개발만 계속하고 영업을 안 하는 상태" 방지

---

## 9. App Store / Play Store와의 분리

SUPER POWER CRAFT는 **앱스토어 제출 준비를 다루지 않는다.**

앱스토어 출시가 목표라면 별도 프레임워크인 **STORE POWER CRAFT**를 사용한다.

SUPER POWER CRAFT의 마지막 산출물에는 `Next Path` 항목에 `Store Submission Track`을 포함할 수 있으며,
Store Submission Track이 필요하면 `STORE POWER CRAFT로 전환`을 권장한다.

---

## 10. Scope Control

- 각 Cycle은 최대 3개의 주요 개선 목표만 수행한다
- P0는 최대 3개, P1은 최대 3개, P2는 기록만 하고 구현하지 않는다
- Cycle 02 이후에는 판매 가능성, 문구, UX, 데모 흐름, 안정성을 우선한다
- Cycle 03에서는 새로운 대형 기능을 추가하지 않는다
- 이미 완료된 항목을 다음 Cycle 목표로 반복하지 않는다

---

## 11. Stop Conditions

아래 중 하나라도 해당하면 다음 Cycle로 자동 진행하지 않는다:

1. Live Demo가 정상 동작하지 않는다
2. GitHub / README / outputs 상태가 불일치한다
3. 핵심 기능이 동작하지 않는다
4. 민감정보 또는 위험한 자동화가 포함되었다
5. 제품 가치가 불명확하다
6. 유지보수 부담이 과도하다
7. 사용자에게 팔 상품이 정의되지 않았다
8. Cycle 목표가 이미 완료된 작업을 반복하고 있다
9. 다음 Cycle에서 해결할 수 없는 외부 권한/API 문제가 막고 있다
10. 자동으로 계속 개선하는 것이 오히려 제품 방향을 흐릴 가능성이 있다

중단 시 `outputs/cycle-XX/BLOCKER_REPORT.md`를 작성하고 사용자 판단을 기다린다.

---

## 12. README 확장

README에는 최종적으로 아래 섹션을 추가할 수 있다:

```md
## Sales Test Status

- Sales Test Ready / Needs Polish / Not Ready

## Sales Package

## Target Customer

## First Offer Price

## Free Sample Offer

## Live Demo

## Sales Test Decision

## Next User Action
```

Cycle 01에서는 `Not evaluated yet`으로 표시할 수 있다.

---

## 13. outputs/INDEX.md 확장

```md
## Sales Test Readiness Artifacts

| Cycle | Product Value | Sales Readiness | Sales Test Readiness | Sales Test Score | Sales Test Decision |
|:-----:|:-------------:|:---------------:|:--------------------:|:----------------:|:-------------------:|
| cycle-01 | - | - | - | - | - |
| cycle-02 | PRODUCT_VALUE_GATE.md | SALES_READINESS_GATE.md | - | - | - |
| cycle-03 | PRODUCT_VALUE_GATE.md | SALES_READINESS_GATE.md | SALES_TEST_READINESS_GATE.md | SALES_TEST_SCORE.md | SALES_TEST_DECISION.md |
```

---

## 14. 보고 형식

### 채팅 짧은 보고 (공통 규칙)

채팅 보고는 아래 형식을 사용한다. 긴 내용은 md 파일에만 작성한다.

```md
## 짧은 보고

- 상태:
- 완료 내용:
- 수정한 파일:

## 다음 액션

- 권장 결정: (완료 처리 / 진행 / 보류 / 중단 / 1회 보완 / 사용자 승인 필요)
- 이유:
- 지금 사용자에게 필요한 행동: (없음 / 승인 / 보류 / 거절 / 계정 제공 / 토큰 제공 / 비용 승인 / 파일 제공 / 테스트 대상 선택)
- 나중에 필요한 조건:
- 에이전트가 다음에 자동으로 처리할 일:
```

상세 규칙은 [AGENT_OPERATION_RULES.md](../AGENT_OPERATION_RULES.md) 참고.

### Cycle 03 종료 보고

Cycle 03 종료 시 채팅 보고는 아래 항목을 추가로 포함한다:

```md
## Sales Test 최종 보고 (Cycle 03)

- 상태: ✅ 완료 / ⏳ 진행 중 / ❌ 실패
- 판정: Sales Test Ready / Needs Polish / Not Ready
- Sales Test Score: 0~100
- GitHub Repo: url
- Live Demo: url
- SALES_TEST_DECISION.md: outputs/cycle-03/SALES_TEST_DECISION.md
```

긴 보고는 md 파일에만 작성한다.

---

## 15. BLOCKER_REPORT.md

권장 위치: `outputs/cycle-XX/BLOCKER_REPORT.md`

```md
# Blocker Report

## 1. 중단된 Cycle
## 2. 중단 사유
## 3. 실패한 Gate
## 4. 현재까지 완료된 작업
## 5. 자동 진행하면 안 되는 이유
## 6. 사용자 결정 필요 사항
## 7. 가능한 선택지
### 선택지 A — Hotfix 후 계속 진행
### 선택지 B — 범위 축소
### 선택지 C — 제품 방향 변경
### 선택지 D — 프로젝트 종료
## 8. 권장 선택
```

---

## 16. 판정 후 액션 규칙

Cycle 03 종료 후 판정에 따라 다음 액션이 결정된다:

### Sales Test Ready → 개발 종료 + 영업 테스트 진행

```
더 이상 Cycle 반복하지 않는다.
개발 종료. 영업 테스트 단계 진입.

사용자 액션:
- DM/전화 영업 시작
- 무료 진단 제안
- 반응률 기록
- 유료 전환 시도
```

### Needs Polish → 사용자 승인 시 1회 hotfix 허용

```
자동 진행은 멈춘다.
단, 사용자가 승인하면 1회 hotfix를 허용한다.

hotfix 규칙:
- Cycle 02b: Product Value 또는 Sales Readiness Gate 보완
- Cycle 03 polish hotfix: Sales Test Readiness Gate 또는 문서 보완
- hotfix 후 재판정: 통과 시 Sales Test Ready / 실패 시 Not Ready
- 1회 초과 hotfix 금지 (무한 개선 방지)
```

### Not Ready → 자동 진행 중단 + 방향 재검토

```
더 이상 Cycle 반복하지 않는다.
방향 재검토 필요.

권장 액션:
- BLOCKER_REPORT.md 작성
- 제품 방향 변경 고려
- STORE POWER CRAFT는 Not Ready 상태에서는 권장하지 않음
```

### 판정 후 액션 결정 흐름

```
Cycle 03 종료
  │
  ├─ Sales Test Ready → 개발 종료 → 영업 테스트 시작
  │
  ├─ Needs Polish
  │     ├─ 사용자 승인 있음 → 1회 hotfix → 재판정
  │     └─ 사용자 승인 없음 → Not Ready와 동일 처리
  │
  └─ Not Ready → BLOCKER_REPORT → 방향 재검토
```
