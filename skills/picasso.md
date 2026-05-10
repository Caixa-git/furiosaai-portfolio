# 🎨 Picasso — 디자인 리뷰 엔진

> **버전:** v0.6 | **역할:** 20항목 정량 체크리스트 기반 디자인 리뷰

Picasso는 UI 디자인을 **20항목 정량 체크리스트**로 평가하여 **Report Card(A+~F)** 성적을 산출하는 디자인 리뷰 스킬입니다. **Review**(현황 분석) → **Propose**(개선 제안) → **Generate**(수정 코드 생성)의 3-stage 프로세스로 동작하며, 일관성, 타이포그래피, 색상 대비, 여백, 계층 구조 등 디자인 전 영역을 정량 평가합니다. 각 항목별 점수와 함께 시각적 증거(스크린샷 마킹)를 첨부하여 구체적인 피드백을 제공합니다.

---

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **20항목 체크리스트** | 일관성, 타이포그래피, 색상 대비, 여백, 계층 구조, 아이콘 일관성 등 20개 항목 정량 평가 |
| **Report Card (A+ ~ F)** | 항목별 점수 가중합 → 종합 성적 자동 산출 (A+ 상위 5%, F 하위 5%) |
| **3-Stage 프로세스** | Review(현황분석) → Propose(개선제안) → Generate(수정코드생성) 단계적 실행 |
| **시각적 증거 첨부** | 각 평가 항목에 해당하는 UI 스크린샷 영역 마킹 및 비교 이미지 생성 |
| **개선 우선순위** | 영향도 × 용이도 매트릭스 기반으로 수정 권장 순위 자동 제안 |

---

## 3-Stage 프로세스

| Stage | 활동 | 산출물 |
|:------|:-----|:-------|
| **1. Review** | 20항목 체크리스트 기반 현황 분석 | 항목별 점수 + 스크린샷 증거 |
| **2. Propose** | 문제 항목별 개선 방안 및 우선순위 제안 | 개선 제안서 (Impact × Effort) |
| **3. Generate** | CSS/HTML 수정 코드 자동 생성 | 수정된 컴포넌트 코드 |

---

## 항목 예시 (20항목 중 일부)

| # | 항목 | 평가 기준 |
|:-:|:-----|:----------|
| 1 | **시각적 일관성** | 버튼, 입력 필드 등 유사 요소의 스타일 통일 여부 |
| 2 | **타이포그래피** | 폰트 크기, 행간, 자간의 가독성 및 계층 |
| 3 | **색상 대비** | WCAG AA 이상 명도 대비 비율 (4.5:1) 충족 여부 |
| 4 | **여백/스페이싱** | 그리드 및 패딩의 일관된 여백 시스템 |
| 5 | **계층 구조** | 시각적 위계(Hierarchy)의 명확성 |

---

## YAML 명세

```yaml
name: Picasso
version: 0.6
trigger: 디자인 리뷰 요청 (Oculus 출력 기반)
input:
  format: PIPE Protocol (JSON)
  schema:
    oculus_report: { components, layout_tree, errors }
    checklist_overrides: [integer, ...]
output:
  format: PIPE Protocol (JSON)
  schema:
    report_card: { grade, overall_score, items: [{ id, name, score, max, evidence }] }
    stage: "review" | "propose" | "generate"
    output_code: string (CSS/HTML)
dependencies: [Oculus]
```

---

> **Pipeline:** Oculus(분석) → Picasso(디자인 리뷰) → Argo(UX 진단) → Disney(애니메이션 평가)
