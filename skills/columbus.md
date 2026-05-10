# 🔍 Columbus — 다중 출처 웹 탐색 엔진

> **버전:** v3.3.0 | **역할:** 다중 출처 웹 탐색 및 Quality Score 기반 품질 평가

Columbus는 다중 검색 소스(Google, Bing, 직접 URL)에서 정보를 수집하고 교차 검증하는 웹 탐색 스킬입니다. 수집된 결과에 대해 **Quality Score(0–10)** 를 산출하여 저품질/스팸 콘텐츠를 필터링하며, **Quick Scan**과 **Full Expedition** 듀얼 모드로 탐색 깊이를 조절할 수 있습니다. PIPE Protocol(JSON)로 구조화된 검색 결과(URL, 스니펫, 스코어)를 상위 파이프라인에 전달합니다.

---

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **다중 소스 수집** | Google, Bing, 직접 URL 등 여러 출처에서 동시에 정보 수집 및 교차 검증 |
| **Quality Score (0–10)** | 신뢰도, 최신성, 출처 권위, 관련성 4축 평가로 품질 점수 산출 |
| **Quick Scan / Full Expedition** | 빠른 개요 확인(Quick Scan) vs 심층 탐색(Full Expedition) 듀얼 모드 지원 |
| **스팸/저품질 필터링** | Quality Score 임계값 기반 자동 필터링 및 이상 탐지 |
| **PIPE 구조화 출력** | URL, 스니펫, 스코어, 메타데이터를 포함한 JSON 형식 결과 전달 |

---

## 듀얼 모드

| 모드 | 대상 | 탐색 깊이 | 예상 시간 |
|:----|:-----|:---------:|:---------:|
| **Quick Scan** | 빠른 개요 확인 | 상위 3–5 결과 | < 10초 |
| **Full Expedition** | 심층 조사 | 10+ 결과 + 연쇄 탐색 | 30–60초 |

---

## YAML 명세

```yaml
name: Columbus
version: 3.3.0
trigger: 사용자가 웹 검색/정보 수집 요청
input:
  format: PIPE Protocol (JSON)
  schema:
    query: string
    mode: "quick_scan" | "full_expedition"
    sources: ["google", "bing", "url"]
output:
  format: PIPE Protocol (JSON)
  schema:
    results: [{ url, snippet, title, quality_score, source, fetched_at }]
    summary: string
dependencies: []
```

---

> **Pipeline:** Socrates(진단) → Router(경로 선택) → Columbus(탐색) → 상위 스킬(분석/요약)
