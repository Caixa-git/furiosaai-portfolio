# 🧭 Argo — UX 진단 엔진

> **버전:** v0.3 | **역할:** 6계층 UX 진단 (P1 접근성 ~ P6 브랜드 일관성)

Argo는 웹 애플리케이션의 사용자 경험을 **6개 계층(P1~P6)** 으로 나누어 진단하는 UX 엔진입니다. **접근성(WCAG 2.1)**부터 **터치/모바일 최적화**, **레이아웃 구조**, **내비게이션 흐름**, **정보 구조**, **브랜드 일관성**까지 전 계층을 아우르며, CLI 기반 UX 평가도 지원합니다. **Oculus → Picasso → Argo → Disney** 파이프라인의 세 번째 단계로, 이전 단계의 분석 결과를 입력받아 UX 관점의 종합 진단을 수행합니다.

---

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **6계층 UX 진단 (P1~P6)** | 접근성 → 터치/모바일 → 레이아웃 → 내비게이션 → 정보 구조 → 브랜드 일관성 |
| **P1 접근성 평가** | WCAG 2.1 AA 기준 명도 대비(4.5:1), 키보드 내비게이션 탭 순서, ARIA 속성 완전성 검사 |
| **P2 터치/모바일** | 터치 타겟 크기(최소 44×44px), 제스처 호환성, 반응형 레이아웃 미디어 쿼리 검증 |
| **P3~P6 심화 진단** | 레이아웃 그리드 일관성, 내비게이션 흐름 최단 경로, 정보 구조 깊이, 브랜드 컬러/폰트 일관성 |
| **CLI UX 평가** | 터미널 기반 애플리케이션의 사용성, 명령어 일관성, 에러 메시지 품질 평가 |
| **파이프라인 연동** | Oculus(분석) → Picasso(디자인) → Argo(UX) → Disney(애니메이션) 순차 실행 |

---

## 6계층 UX 진단 (P1~P6)

| 계층 | 평가 영역 | 주요 체크포인트 |
|:----|:---------|:---------------|
| **P1** 접근성 | WCAG 2.1, 키보드, ARIA | 명도 대비 ≥ 4.5:1, 탭 순서 논리적, ARIA 레이블 존재 |
| **P2** 터치/모바일 | 반응형, 터치 타겟 | 타겟 크기 ≥ 44×44px, 뷰포트 메타태그, 미디어 쿼리 |
| **P3** 레이아웃 | 그리드, 정렬, 일관성 | 컬럼 정렬, 패딩 일관성, 오버플로우 없음 |
| **P4** 내비게이션 | 흐름, 깊이, breadcrumb | 페이지 간 이동 최단 경로, 3클릭 룰, breadcrumb 존재 |
| **P5** 정보 구조 | 라벨링, 분류, 검색 | 메뉴 라벨 명확성, 콘텐츠 분류 논리성, 검색 기능 |
| **P6** 브랜드 | 색상, 폰트, 톤앤매너 | 브랜드 컬러 팔레트 일관성, 폰트 시스템 통일, Tone of Voice |

---

## CLI UX 평가 항목

| 항목 | 기준 |
|:-----|:------|
| 명령어 일관성 | 하이픈(-) vs 서브커맨드 일관된 패턴 |
| 에러 메시지 | 구체적 원인 + 해결 방법 제시 |
| 진행 표시 | 장시간 작업 시 spinner/progress bar 제공 |
| 도움말 | `--help` 출력의 완전성과 가독성 |

---

## YAML 명세

```yaml
name: Argo
version: 0.3
trigger: UX 진단 요청 (Picasso 출력 기반)
input:
  format: PIPE Protocol (JSON)
  schema:
    picasso_report: { report_card, items, output_code }
    target: "web" | "cli"
output:
  format: PIPE Protocol (JSON)
  schema:
    layers: [{ id: "P1".."P6", score, findings: [{ severity, criteria, passed, detail }] }
    cli_evaluation: [{ criteria, score, detail }]
    overall_ux_score: number
    recommendations: [string]
dependencies: [Oculus, Picasso]
```

---

> **Pipeline:** Oculus(분석) → Picasso(디자인 리뷰) → Argo(UX 진단) → Disney(애니메이션 평가)
