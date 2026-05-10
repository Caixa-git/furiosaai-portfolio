# 🔎 Sherlock — 레포 분석 엔진

> GitHub 저장소를 심층 분석하여 위험 파일, 개선 우선순위, 구조적 문제점을 탐지하는 엔진. 4단계 파이프라인(수집→분석→진단→보고)으로 동작하며, Risk Score 0-10으로 각 파일과 전체 레포의 건강 상태를 정량화합니다.

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **4단계 분석 파이프라인** | **1. 수집(Collect)** — 디렉터리 트리, 파일 메타데이터, Git 히스토리, 의존성 파일 스캔<br>**2. 분석(Analyze)** — 언어별 비율, 코드 복잡도, 의존성 그래프, 보안 취약점 DB 크로스 체크<br>**3. 진단(Diagnose)** — 위험 패턴 매칭, 변경 빈도×영향도 매트릭스, 기술 부채 추정<br>**4. 보고(Report)** — 우선순위별 액션 아이템, 위험 파일 목록, 개선 로드맵 생성 |
| **Risk Score (0-10)** | 각 파일 및 레포 전체에 대해 위험도 점수 산출.<br>**0-3**: 양호 — 정기 모니터링 대상<br>**4-6**: 주의 — 중간 위험, 계획적 리팩토링 필요<br>**7-8**: 위험 — 즉시 검토 필요<br>**9-10**: 심각 — 즉시 조치 필요 (시크릿 노출, 치명적 보안 취약점)<br><br>산출 요소: 보안 취약점 수, 하드코딩된 값, 파일 크기/나이, 테스트 커버리지, 의존성 깊이, 최근 변경 빈도 |
| **위험 파일 탐지** | • **시크릿 누출** — API 키, 토큰, 비밀번호, SSH 키 정규식 매칭 (2,000+ 패턴)<br>• **크고 오래된 파일** — 500줄 초과 / 6개월 이상 미변경 파일<br>• **취약한 의존성** — OSV(Open Source Vulnerabilities) DB 기반 CVE 매칭<br>• **이상 패턴** — 바이너리 파일, 대용량 데이터 파일, .env 파일, 디버그 코드 잔재 |
| **개선 우선순위 엔진** | 변경 빈도(Frequency) × 영향도(Impact) × 위험도(Risk) 3차원 매트릭스.<br>**Hot Zone** (고빈도+고영향) — 최우선 리팩토링 대상<br>**Deferred Zone** (저빈도+저영향) — 백로그 등록<br>**Watch Zone** (고위험+저빈도) — 모니터링 강화<br><br>리팩토링 예상 시간과 영향 범위를 함께 제공하여 의사결정 지원 |

## 버전 정보

```yaml
name: Sherlock
emoji: 🔎
version: v0.4.0
trigger: 레포 분석 요청 / PR 생성 시 / 정기 감사 주기
input:
  format: PIPE Protocol (JSON)
  schema:
    repo: { url, branch, depth, exclude_patterns }
    analysis_scope: { security?, structure?, dependencies?, history? }
output:
  format: PIPE Protocol (JSON)
  schema:
    risk_score: { overall, file_count_by_risk }
    findings: [{ file, risk_score, category, detail, severity, fix_suggestion }]
    priorities: [{ item, zone, impact, effort_hours, recommendation }]
    timeline: { analysis_duration, files_scanned, patterns_matched }
dependencies: [Columbus(취약점 DB 조회), Prometheus(분석 스킬 품질 평가)]
```

---

> *"데이터를 보는 것이 아니라, 데이터가 말하지 않는 것을 보는 것입니다." — Sherlock 분석 철학*
