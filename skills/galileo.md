# 🔭 Galileo — 웹앱 검증 엔진

> 웹 애플리케이션을 8단계 검증 파이프라인으로 종합 테스트하는 엔진. HTML 구조부터 모바일 반응형까지 전 계층을 커버하며, Verification Score 0-10과 P-Level P0~P4로 품질 상태를 정량화합니다.

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **8단계 검증 파이프라인** | **① HTML 구조** — 시맨틱 마크업, 메타 태그, heading 계층, aria 속성 검사<br>**② CSS 렌더링** — 레이아웃 일관성, 컬러 대비(WCAG AA/AAA), 폰트 로딩, 반응형 중단점<br>**③ JavaScript 실행** — 콘솔 오류, 런타임 예외, 번들 크기, 동적 로딩 타이밍<br>**④ 콘솔 에러** — Warning/Error 분류, deprecated API 사용 감지, 네트워크 실패 로그<br>**⑤ 네트워크** — HTTP 상태 코드, 리소스 로딩 실패, CORS 오류, API 호출 성능<br>**⑥ SEO** — robots.txt, sitemap, OG 태그, canonical URL, 인덱싱 가능성<br>**⑦ 성능** — Core Web Vitals(LCP/FID/CLS), 최초 로딩 시간, 번들 최적화 정도<br>**⑧ 모바일 반응형** — 뷰포트 메타, 터치 타겟 크기(≥48px), 콘텐츠 오버플로우, 가로 스크롤 |
| **Verification Score (0-10)** | 8단계 각각의 통과율을 가중 평균한 종합 점수.<br>**9-10**: 프로덕션 배포 준비 완료<br>**7-8**: 경미한 이슈, 배포 가능하나 수정 권장<br>**5-6**: 주요 이슈 존재, QA 통과 불가<br>**0-4**: 심각한 문제, 개발 단계 재검토 필요<br><br>가중치: 성능(20%) > HTML/JS/모바일(각 15%) > CSS/콘솔/네트워크(각 10%) > SEO(5%) |
| **P-Level (P0~P4)** | 각 검증 단계별 발견된 이슈의 심각도 등급.<br>**P0 (Critical)** — 서비스 중단/데이터 손실 위험. 즉시 수정<br>**P1 (High)** — 주요 사용자 경험 저하. 이번 스프린트 수정<br>**P2 (Medium)** — 기능적 결함. 다음 스프린트 수정<br>**P3 (Low)** — UX 개선 사항. 백로그 등록<br>**P4 (Cosmetic)** — 스타일/코드 스타일. 시간 여유 시 수정 |
| **Lighthouse 연동** | Google Lighthouse/PageSpeed Insights API와 연동하여 Core Web Vitals 데이터 수집. 자체 검증 결과와 Lighthouse 결과를 교차 검증하여 신뢰도 향상. 모바일/데스크톱 별도 점수 산출 |
| **회귀 테스트 모드** | 이전 검증 결과와 비교하여 신규/해결/재발생 이슈 자동 식별. Verification Score 증감 추이 그래프 생성. 주요 변경 사항이 성능/접근성에 미친 영향 분석 리포트 제공 |

## 버전 정보

```yaml
name: Galileo
emoji: 🔭
version: v0.4.0
trigger: 웹앱 배포 전 검증 / PR 머지 게이트 / 정기 QA 주기
input:
  format: PIPE Protocol (JSON)
  schema:
    target: { url, device?, viewport? }
    scope: { stages: [1-8], lighthouse?, regression? }
output:
  format: PIPE Protocol (JSON)
  schema:
    verification_score: { overall, by_stage }
    issues: [{ stage, p_level, detail, fix_guide }]
    lighthouse_data: { lcp, fid, cls, performance_score }
    regression: { new_issues, fixed_issues, regressed_issues }
dependencies: [Columbus(페이지 탐색), Oculus(DOM/렌더링 분석)]
```

---

> *"측정할 수 없는 것은 개선할 수 없습니다. 검증되지 않은 것은 배포할 수 없습니다." — Galileo 엔진 원칙*
