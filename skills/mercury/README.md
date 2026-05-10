# ✍️ Mercury — 카피라이팅 엔진

> T.A.P. 프레임워크, Voice Matrix, 3레이어 방법론(Strategy→Structure→Execution) 기반 정밀 카피라이팅. 브랜드의 목소리를 데이터로 분석하고, 타겟에 최적화된 메시지를 전략적으로 설계합니다.

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **T.A.P. Framework** | **Target**(대상) — 인구통계/심리그래픽/행동 패턴 분석<br>**Angle**(관점) — 차별화된 메시징 각도 발굴 (문제 중심, 비전 중심, 가치 중심)<br>**Purpose**(목적) — 전환/인지/교육/브랜딩 중 명확한 목표 설정 후 카피 방향 결정 |
| **Voice Matrix** | 브랜드 어조(Tone of Voice)를 권위성-친근감, 전문성-접근성, 진지함-유머 등의 축으로 매트릭스화하여 일관된 브랜드 보이스 유지. 새로운 채널이나 캠페인에도 동일한 보이스 프로필 적용 가능 |
| **3레이어 방법론** | **Strategy Layer** — 브랜드 포지셔닝, 시장 맥락, 경쟁사 메시징 분석<br>**Structure Layer** — 설득 구조(AIDA, PAS, FAB), 정보 계층화,CTA 배치 최적화<br>**Execution Layer** — 어휘 선택, 문장 리듬, 포맷(헤드라인/바디/캡션)에 따른 표현 전달 |
| **A/B 변형 생성** | 동일한 T.A.P. 분석 결과에서 최대 5가지 어조/구조 변형 카피 자동 생성. 효과 예측 스코어(Hook Strength, Clarity, Persuasion) 0-10 척도로 제공 |
| **멀티채널 최적화** | 웹/이메일/SNS/광고/제품 내 카피 등 채널별 특성에 맞춰 글자 수, 어조, CTA 스타일 자동 조정. 동일 메시지의 채널별 변형 일괄 생성 |

## 버전 정보

```yaml
name: Mercury
emoji: ✍️
version: v0.2.0
trigger: 카피라이팅 요청 / 브랜드 메시징 진단 / A/B 테스트 카피 생성
input:
  format: PIPE Protocol (JSON)
  schema:
    brand: { tone_profile, target_audience, channel }
    brief: { purpose, key_message, desired_action }
output:
  format: PIPE Protocol (JSON)
  schema:
    tap_analysis: { target, angle, purpose }
    copies: [{ variant, tone, structure, score }]
dependencies: [Columbus(경쟁사 메시징 조사), Argo(UX 맥락)]
```

---

> *"카피는 단순한 문장이 아닙니다. 전략이 문장이 된 것입니다." — Mercury 엔진 철학*
