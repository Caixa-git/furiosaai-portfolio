# 🎵 Disney — 웹 애니메이션 평가/생성 엔진

> **버전:** v0.3 | **역할:** CSS/anime.js 웹 애니메이션 평가 및 생성

Disney는 웹 애니메이션을 **E1~E7 7축 평가 기준**으로 진단하고, **CSS `@keyframes` Transition** 또는 **anime.js** 기반 애니메이션 코드를 자동 생성하는 스킬입니다. 평가 기준은 Disney의 **12가지 애니메이션 원칙**(Squash & Stretch, Anticipation, Follow Through 등)을 웹 환경에 맞게 계량화했으며, 성능(60fps), 부드러움, 접근성(동작 줄이기 `prefers-reduced-motion`), 타이밍/이징, 일관성, 연속성, 코드 품질을 종합적으로 평가합니다.

---

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **E1~E7 7축 평가** | 성능(60fps), 부드러움, 접근성, 일관성, 타이밍/이징, 연속성, 코드 품질 |
| **CSS 애니메이션 생성** | `@keyframes` + `transition` 속성을 활용한 최적화된 CSS 코드 자동 생성 |
| **anime.js 생성** | JavaScript anime.js 라이브러리 기반 복합 애니메이션 코드 자동 생성 |
| **Disney 12 원칙 매핑** | Squash & Stretch, Anticipation, Follow Through 등 12 원칙을 웹 메트릭스로 계량화 |
| **접근성 고려** | `prefers-reduced-motion` 미디어 쿼리 및 `will-change` 최적화 포함 |

---

## E1~E7 평가 기준

| # | 항목 | 기준 | Disney 원칙 매핑 |
|:-:|:-----|:----|:----------------|
| **E1** | 성능(Performance) | 60fps 유지, 레이아웃 쓰레싱 없음 | Timing |
| **E2** | 부드러움(Smoothness) | 이징 곡선 자연스러움, 가속/감속 | Slow In & Slow Out |
| **E3** | 접근성(Accessibility) | `prefers-reduced-motion` 대응, 깜빡임 주의 | Staging |
| **E4** | 일관성(Consistency) | 사이트 전반 애니메이션 스타일/지속시간 통일 | Appeal |
| **E5** | 타이밍/이징(Timing & Easing) | easing 함수 적절성, 지속시간(200–500ms 권장) | Arcs |
| **E6** | 연속성(Continuity) | 페이지 전환, 요소 등장/퇴장의 자연스러운 흐름 | Follow Through |
| **E7** | 코드 품질(Code Quality) | 하드웨어 가속(transform/opacity), 최적화, 유지보수성 | Solid Drawing |

---

## 생성 모드

| 모드 | 대상 | 출력 형식 | 예시 |
|:----|:----|:---------|:-----|
| **CSS @keyframes** | 단순 트랜지션, hover 효과 | CSS | `@keyframes fadeIn { ... }` |
| **CSS Transition** | 상태 변경 애니메이션 | CSS | `transition: transform 0.3s ease;` |
| **anime.js** | 복합 시퀀스, 스크롤 연동 | JavaScript | `anime({ targets, translateX, rotate, ... })` |

---

## YAML 명세

```yaml
name: Disney
version: 0.3
trigger: 애니메이션 평가 또는 생성 요청 (Argo 출력 기반)
input:
  format: PIPE Protocol (JSON)
  schema:
    argo_report: { layers, overall_ux_score, recommendations }
    mode: "evaluate" | "generate"
    target_elements: [{ selector, animation_type }]
output:
  format: PIPE Protocol (JSON)
  schema:
    evaluation: { E1..E7: { score, detail, principle_mapped } }
    generated_code: { css, javascript, anime_script }
    recommendations: [string]
    accessibility_notes: [string]
dependencies: [Oculus, Picasso, Argo]
```

---

> **Pipeline:** Oculus(분석) → Picasso(디자인 리뷰) → Argo(UX 진단) → Disney(애니메이션 평가/생성)
>
> **Disney 12 Principles:** Squash & Stretch · Anticipation · Staging · Straight Ahead & Pose to Pose · Follow Through & Overlapping Action · Slow In & Slow Out · Arcs · Secondary Action · Timing · Exaggeration · Solid Drawing · Appeal
