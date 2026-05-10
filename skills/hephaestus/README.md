# 🔧 Hephaestus — CI/빌드 복구 엔진

> CI/CD 파이프라인 및 빌드 실패를 정밀 분석하고 자동 복구하는 엔진. 빌드 로그를 파싱하여 10개 원인 카테고리로 분류하고, Recovery Score로 복구 난이도와 자동화 가능성을 정량화합니다.

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **10개 원인 카테고리 분류** | **DEP** — 의존성 버전 충돌 / 누락된 패키지<br>**CFG** — 설정 오류 (YAML 구문, 환경 변수, CI 설정)<br>**SYN** — 구문/컴파일 에러 (TypeError, ImportError)<br>**LNK** — 링킹 실패 / 바이너리 호환성 문제<br>**TST** — 테스트 실패 (불안정한 테스트, 플레이크)<br>**RSC** — 리소스 부족 (메모리, 디스크, 빌드 시간 초과)<br>**SEC** — 보안 정책 위반 (비밀키 노출, 취약점 게이트)<br>**CCH** — 캐시 문제 (오래된/깨진 캐시)<br>**ENV** — 환경 차이 (로컬 vs CI, OS 버전, 런타임)<br>**NET** — 네트워크 실패 (패키지 다운로드, 원격 API 타임아웃) |
| **Recovery Score (0-10)** | 빌드 로그 분석 → 각 실패 카테고리별 복구 난이도 점수 산출.<br>**0-3**: 자동 복구 가능 (재시도, 패치 적용)<br>**4-6**: 반자동 (원인 진단 + 수정안 제시)<br>**7-10**: 수동 개입 필요 (근본 원인 분석 보고서 생성) |
| **자동 복구 파이프라인** | ① 실패 감지 → ② 로그 캡처 및 파싱 → ③ 원인 카테고리 분류 → ④ Recovery Score 산출 → ⑤ 자동 패치 생성 → ⑥ 재빌드 트리거. 복구 성공 시 Diff 기록, 실패 시 상세 진단 보고서 출력 |
| **CI 환경 설정 진단** | GitHub Actions / GitLab CI / Jenkins 파이프라인 YAML 구문 검증. 캐시 전략, 매트릭스 빌드, 병렬 실행 설정 최적화 제안. Runner 가용성 및 아티팩트 관리 문제 감지 |

## 버전 정보

```yaml
name: Hephaestus
emoji: 🔧
version: v0.3.0
trigger: CI/빌드 실패 알림 / PR 머지 게이트 위반
input:
  format: PIPE Protocol (JSON)
  schema:
    build_log: { raw_text, ci_provider, commit_sha, branch }
    context: { previous_builds, diff_summary }
output:
  format: PIPE Protocol (JSON)
  schema:
    root_cause: { category, detail, recovery_score }
    fix: { auto_patch?, patch_diff, rebuild_result }
    report: { summary, timeline, recommendations }
dependencies: [Prometheus(복구 스킬 진화)]
```

---

> *"빌드는 실패하는 법을 배우고, 우리는 그 실패에서 복구하는 법을 배웁니다." — Hephaestus 설계 원칙*
