# ⚡ Prometheus — 스킬 메타 엔진

> 스킬의 생성/진화/검토를 담당하는 메타 스킬. 새로운 스킬을 설계하고, 기존 스킬의 성능을 5축 평가로 측정하며, Dreyfus 모델 기반 숙련도 진화를 자동화합니다. 자가 개선하는 스킬 생태계의 핵심 엔진입니다.

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **스킬 생성** | 사용 사례 정의 → YAML 스키마 설계 → 트리거 조건 설정 → I/O 계약 정의 → 초기 테스트 케이스 생성까지 스킬 수명 주기 자동화. 신규 스킬은 P-Level P2(초기 검증 완료)로 시작 |
| **5축 평가 시스템** | **Quality Score (0-10)** — 정확성, 일관성, 오류율 기반 종합 품질<br>**P-Level (P0-P4)** — P0=프로덕션 검증 / P1=안정 / P2=초기 검증 / P3=개발 중 / P4=컨셉<br>**ALCHEMY** — 스킬 간 시너지 점수. 다른 스킬과의 결합 시 효율성 증가율 측정<br>**KPI** — 실행 시간, 정확도, 사용자 만족도, 복구율 등 운영 지표 트래킹<br>**Merge Score** — 기존 스킬과의 통합 적합도. 중복 기능, 인터페이스 충돌 위험 평가 |
| **Dreyfus 모델 기반 진화** | 초보자(Novice) → 고급 초보자(Advanced Beginner) → 유능(Competent) → 숙련(Proficient) → 전문가(Expert) 5단계 숙련도 모델. 각 레벨업 조건: 실행 횟수, 오류율 감소, 컨텍스트 적응력, 자동화된 의사결정 비율 |
| **스킬 검토 자동화** | 주기적 스킬 감사 — Quality Score 하락 감지 → 원인 분석 → 개선 PR 생성. 사용률 KPI 기반 폐기/통합/분할 의사결정 지원. 모든 평가 결과를 PIPE Protocol로 스킬 레지스트리에 기록 |
| **메타 학습 루프** | 각 스킬의 실행 결과를 수집 → 패턴 분석 → 스킬 동작 파라미터 최적화. 실패율이 높은 스킬에 자동으로 추가 검증 단계 삽입하거나, 과도하게 보수적인 스킬의 임계값 조정 |

## 버전 정보

```yaml
name: Prometheus
emoji: ⚡
version: v0.3.0
trigger: 신규 스킬 생성 요청 / 스킬 진화 주기 / 품질 임계값 위반
input:
  format: PIPE Protocol (JSON)
  schema:
    action: { create | evolve | review | audit }
    skill_context: { name, version, metrics, usage_stats }
output:
  format: PIPE Protocol (JSON)
  schema:
    assessment: { quality_score, p_level, alchemy, kpi, merge_score }
    evolution: { current_dreyfus_level, next_milestone, upgrade_diff }
    actions: [ { type, description, pr_link? } ]
dependencies: [모든 스킬 (메타 평가 의존)]
```

---

> *"가장 위대한 발명은 발명하는 방법 그 자체입니다." — Prometheus 설계 철학*
