# SUPER POWER CRAFT 설계 — 자기비판 및 검증 요청

## 배경

단일 AI 에이전트가 작동하는 SDLC 프레임워크(CRAFT → POWER CRAFT → SUPER POWER CRAFT)
38+ 논문 인용, ~60,000 인용 기반.

## 요청

아래에 정리한 **설계 단계에서 수행한 자기비판과 구조 분석 결과**에 대해:

1. 각 비판이 타당한가?
2. 놓친 비판이 있는가?
3. 해결 방안이 있다면 무엇인가?

검토해줘.

---

## 1. POWER CRAFT의 구조적 결함 — 4개 미답 질문

POWER CRAFT(12 layers)는 선형 SDLC 파이프라인이다. Discovery → Deploy → Run까지 한 번 통과하면 끝. 순환(Cyclic) 개선 구조가 전혀 없다.

빈곤하게도 제품 출시 판정을 위해 해결해야 할 질문 4개, 현행 POWER CRAFT는 하나도 답하지 못한다:

| 질문 | POWER CRAFT | 필요한 근거 |
|------|:-----------:|-----------|
| Q1: "이 제품, 출시해도 되나?" | ❌ 판정 기준 없음 | Ellis(2009) PMF · Cooper(1990) Stage-Gate |
| Q2: "몇 번이나 개선해야 하나?" | ❌ 단회 통과 | Boehm(1988) Spiral · Takeuchi & Nonaka(1986) |
| Q3: "무엇을 개선해야 하나?" | ❌ 수동 분석 | Ries(2011) BML · Croll & Yoskovitz(2013) |
| Q4: "개선 후 판정이 바뀌었나?" | ❌ 추적 불가 | Reinertsen(2009) Flow · Poppendieck(2003) |

### 자기 진단

**"갭은 구조적이다."** POWER CRAFT에 단순 레이어 하나 더 얹는 방식으로는 새 프레임워크가 아니라 패치가 된다.
→ 그래서 S Layer(Self-Improving Launch Cycles)를 설계했으나... 아래 의문이 남는다.

---

## 2. S Layer (Self-Improving Launch Cycles) 설계 및 의문

### S1: Launch Readiness Matrix (LRM) — 4축 점수화 → 판정
- 논문: Cooper(1990) Stage-Gate, Ellis(2009) PMF 40%
- 인용: 15,000+
- **의문:** Stage-Gate는 1990년 대기업 R&D용. 단일 AI가 3시간 만에 만든 MVP에 적용하는 게 타당한가? Gate 리뷰를 인간이 아닌 AI가 수행하는데 Stage-Gate의 의미가 유지되는가?

### S2: Cycle Governor — max 3회 제한
- 논문: Boehm(1988) Spiral Model, Reinertsen(2009) WIP
- 인용: 25,000+
- **의문:** "3회"라는 숫자는 어디서 나왔는가? Boehm의 Spiral은 횟수 제한이 없다. Reinertsen의 WIP 제한은 동시 작업 수 제한이지 반복 횟수 제한이 아니다. 이 근거는 논문 인용을 가장한 숫자에 불과한가?

### S3: Auto-Improvement Engine — 갭 분석 → CS-NN 자동 생성
- 논문: Ries(2011) BML, Takeuchi & Nonaka(1986) Scrum
- 인용: 50,000+
- **의문:** Build-Measure-Learn은 실제 고객 데이터로 학습한다. AI가 가상으로 "개선 필요"를 진단하는 것은 BML의 핵심(실제 시장 반응)을 무시한다. 이게 BML인가, BML 흉내인가?

### S4: Classification Gate — Launch Ready / Pre-Launch / Not Ready
- 논문: Olsen(2015) PMF Pyramid, Blank(2013) Customer Dev
- 인용: 10,000+
- **의문:** Pre-Launch 상태에서 재시도 루프가 없음. "Pre-Launch면 Cycle 02로 돌아가라"는 규칙이 없는 이유는? 아니면 무한 루프를 막으려고 일부러 뺀 것인가? Not Ready에서도 마찬가지 — 3 Cycle 실패 후 재시작 트리거가 없음.

---

## 3. FIRE Self-Critique Protocol 자체 진단

모든 논문 기반 제안을 아래 4축으로 검증:

- **F** — Findings replicated? (Open Science 2015)
- **I** — Is context matched? (Yarkoni 2022)
- **R** — Rival explanations? (Ioannidis 2005)
- **E** — Evidence convergence? (Munafò 2017)

→ HIGH / MEDIUM / TENTATIVE 신뢰도 레이블

### 식별된 문제

**R 축이 실제로는 거의 작동하지 않음:** 검색 제약으로 반대 논문을 찾을 수 없어 R 축이 공허해짐. 모든 제안이 사실상 I-E 축만으로 검증됨. FIRE인데 실제론 "FIE"로 작동.

**F 축도 실질적 한계:** 논문 인용 수로 대체하고 있으나, 실제 재현 여부는 확인 불가.

**실효성:** 결국 "이 논문 인용 많고, 문맥이 맞고, 다른 논문과 수렴함"만 확인 → 진짜 반증은 못 함.

---

## 4. Cycle 판정 기준의 근거 의문

### Launch Readiness Gate — 13항목 중 11개 통과

- Launch Ready: 11개 이상
- Pre-Launch: 8~10개
- Not Ready: 7개 이하

**의문:** 이 기준(11/13, 8/10)의 근거는? Cooper(1990) Stage-Gate는 숫자 기준이 아니라 질적 검토(Gate Review Board)다.

### Launch Score — 10축 100점 만점, 80점 이상 Launch Ready

**의문:** 각 축(문제 명확성, 타겟 명확성 등)의 0~10 점수는 누가 판단하는가? 모든 축을 AI가 자체 평가 → 자체 판정. 이게 점수인가, 자기확인인가?

---

## 5. 식별된 6개 Gap (Audit 결과)

| Gap | 심각도 | 현재 대응 | 미해결 문제 |
|-----|:------:|-----------|-------------|
| **Definition of DoD** | P0 | 4개 ✅ 필수 + 2개 🟡/💭 선택 | 🟡/💭 항목이 실제로 수행되는지 강제 불가 |
| **User Acceptance** | P0 | GitHub 확인으로 대체 | 실사용자 피드백 없이 자체 판단. LOA 6-7과 충돌. |
| **Technical Debt** | P2 | TECHNICAL_DEBT.md 로깅 | 상환 트리거 없음, 회계 없음 |
| **Retrospective** | P3 | 없음 | 학습 루프 없음, 같은 실수 반복 가능 |
| **DORA Metrics** | P3 | 설계에 포함, 미구현 | 개선의 객관적 지표 없음 |
| **비용 인식** | P3 | 없음 | 3 Cycle 자동 개선 시 토큰 비용 폭발 가능 |

---

## 6. Ioannidis (2005) 관점

"Why Most Published Research Findings Are False"의 기준 적용:

| 문제 | 해당 여부 | 설명 |
|------|:---------:|------|
| 작은 효과 크기 | ⚠️ | Launch 판정이 실제 출시 성공과 얼마나 상관있는지 불명확 |
| 적은 연구 수 | ⚠️ | 단일 AI, 단일 프로젝트(store-copy-mini)에서만 검증 |
| 유연한 분석 | ⚠️ | Gate 기준/점수는 설계 직후 변경 가능 |
| 경제적/이해관계 편향 | ⚠️ | "프레임워크를 만들었다"는 성과 자체가 검증 편향 |
| 경쟁 연구 많음 | ✅ | DevOps/DORA/Lean Startup은 방대한 competing evidence 존재 |

---

## 검토 요청

위 6개 섹션의 비판 각각에 대해:

1. 타당한 비판인가? (동의/반대/부분)
2. 놓친 더 중요한 비판이 있는가?
3. 해결 방안이 있다면 무엇인가?
