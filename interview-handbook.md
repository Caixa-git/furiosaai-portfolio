# FuriosaAI Agent System Engineer — 면접 대비 핸드북

> *alchemy로 구현한 경험을 학술 용어와 연결한다*

---

## 1. Agent란 무엇인가

| 용어 | 설명 | alchemy 연결 |
|:-----|:-----|:------------|
| **Agent** | 환경을 인지하고 목표를 위해 행동하는 자율 시스템 | alchemy의 메인 루프: `alchemy_agent.h` |
| **Tool Use** | Agent가 외부 도구(API, 함수)를 호출하는 능력 | `alchemy_tool.h` — 14개 슬래시 명령어 |
| **ReAct** | Reasoning + Acting 순환: 생각→행동→관찰 | Socrates→Router→Pipeline 3계층 순환 |
| **Plan-and-Execute** | 먼저 계획 수립 후 단계별 실행 | CRAFT의 9계층 파이프라인 |
| **Reflection** | 자기 출력을 스스로 평가하고 수정 | FIRE 필터 (self-critique) |
| **Orchestration** | 여러 에이전트/도구를 조율 | PIPE Protocol + Router |

**면접 포인트:** "ReAct 패턴을 alchemy에서는 Socrates(진단) → Router(경로 선택) → Pipeline(실행)의 3계층으로 구현했습니다. 단순히 LLM을 호출하는 수준을 넘어, 각 단계에서 Pre/Post Hook으로 검증을 수행합니다."

---

## 2. LLM Inference 기본

| 개념 | 설명 | 면접 질문 예시 |
|:-----|:-----|:-------------|
| **Transformer** | Attention 기반 시퀀스 모델 | "Self-Attention이 뭔가요?" |
| **Tokenization** | 텍스트를 토큰 단위로 분할 | "토큰 수는 어떻게 계산하나요?" |
| **Context Window** | LLM이 한 번에 처리할 수 있는 토큰 수 | "Context Window가 초과되면 어떻게 처리하나요?" |
| **Temperature** | 출력의 무작위성 제어 (0=결정적, 1=창의적) | "Temperature 0으로 설정하면 항상 같은 답이 나오나요?" |
| **Top-K / Top-P** | 다음 토큰 선택 방식 | "Top-K와 Top-P의 차이는?" |
| **Streaming** | 토큰 단위 실시간 출력 | alchemy: SSE streaming 구현 |
| **Structured Output** | JSON 등 형식 강제 출력 | alchemy: PIPE Protocol (JSON) |

**면접 포인트:** "alchemy에서는 멀티 프로바이더 LLM 라우터를 직접 C99로 구현했습니다. SSE 스트리밍, 자동 폴백, 토큰 비용 추적까지 포함합니다. Context Window 관리를 위해 슬라이딩 윈도우 + 자동 트렁케이션을 적용했습니다."

---

## 3. Agent Architecture 패턴

### 3.1 단일 에이전트 (Single Agent)

```
Input → LLM → Tool Call → LLM → Output
```

alchemy의 기본 구조. 하나의 에이전트가 모든 도구를 소유.

### 3.2 멀티 에이전트 (Multi-Agent)

| 패턴 | 설명 | 유사 구현 |
|:-----|:-----|:---------|
| **Supervisor** | 상위 에이전트가 하위 에이전트에 작업 위임 | CRAFT 파이프라인 |
| **Routing** | 입력에 따라 적절한 에이전트로 전달 | alchemy Router |
| **Parallel** | 여러 에이전트 동시 실행 후 결과 취합 | fork+pipe 서브에이전트 |
| **Debate** | 에이전트 간 토론으로 더 나은 결론 도출 | — |
| **Hierarchical** | 계층적 구조로 복잡한 문제 분해 | CRAFT 9계층 (L1→L9) |

### 3.3 Tool Calling (Function Calling) 메커니즘

```
LLM 응답 → tool_calls 파싱 → 함수 실행 → 결과 반환 → LLM 재호출
```

1. 시스템 프롬프트에 도구 스키마 포함
2. LLM이 도구 호출 결정 (JSON 형식)
3. 도구 실행 (격리된 환경)
4. 결과를 컨텍스트에 추가
5. LLM이 최종 응답 생성

**alchemy:** `alchemy_tool.h` + Pre/Post Hook → dlopen 플러그인 로더로 도구 등록

---

## 4. Memory Systems

| 유형 | 설명 | alchemy 구현 |
|:-----|:-----|:------------|
| **Session Memory** | 대화 컨텍스트 유지 (슬라이딩 윈도우) | `alchemy_context.h` |
| **Episodic Memory** | 과거 세션 경험 저장/검색 | `alchemy_memory.h` (파일 기반 KV) |
| **Vector Memory** | 의미 기반 검색 (RAG) | Library 스킬 (FRS/LVS 점수) |
| **Skill Memory** | 스킬 레벨/경험치 영구 저장 | Dreyfus 진화 시스템 |

**면접 포인트:** "메모리는 단순히 '맥락 유지'가 아니라 계층적으로 설계해야 합니다. alchemy에서는 세션 메모리(컨텍스트), 영구 메모리(KV 스토어), 스킬 메모리(Dreyfus 레벨)를 분리했고, Library 스킬에서 Full Read Score로 검색 우선순위를 정량화했습니다."

---

## 5. Multi-Provider LLM Routing

| 개념 | 설명 |
|:-----|:-----|
| **Provider Abstraction** | OpenAI, Anthropic, Ollama 등 다양한 제공자를 통일된 인터페이스로 추상화 |
| **Auto-fallback** | 기본 제공자 실패 시 자동으로 다음 제공자로 전환 |
| **Cost Tracking** | 모델별 토큰 비용 계산 (alchemy: `/cost` 명령어) |
| **Model Selection** | 작업 유형에 따라 적절한 모델 자동 선택 |

**면접 포인트:** "싱글벤더 락인을 피하기 위해 alchemy에서는 Provider 추상화 계층을 두고, 실패 시 자동 폴백, 작업별 모델 자동 선택을 구현했습니다. C99에서 HTTP/S 클라이언트를 직접 구현한 점이 차별점입니다."

---

## 6. Process Isolation & Security

| 개념 | 설명 | alchemy 구현 |
|:-----|:-----|:------------|
| **Process Isolation** | 서브에이전트를 별도 프로세스로 실행 | `fork()+pipe()` |
| **Sandboxing** | 도구 실행을 제한된 환경에서 수행 | LOCKED XOR 페르소나 |
| **Permission Matrix** | 도구별 허용/거부/확인 정책 | `.alchemy/settings.json` |
| **Plugin Security** | 동적 로딩 플러그인의 보안 검증 | dlopen + Hook 체인 검증 |

**면접 포인트:** "8년간 C++ 시스템 엔지니어링 경험을 통해 프로세스 격리와 메모리 안전성의 중요성을 체득했습니다. alchemy에서는 서브에이전트를 fork+pipe로 격리하고, 도구 실행 전 Pre-Hook에서 권한을 검증합니다. 대부분의 Python 기반 에이전트 프레임워크가 이 부분을 간과합니다."

---

## 7. Agent Framework 비교

| 프레임워크 | 언어 | 특징 | alchemy 대비 |
|:-----------|:-----|:------|:-------------|
| **LangChain** | Python | 가장 대중적, 풍부한 통합 | 무거움 (200MB+), Python 의존 |
| **CrewAI** | Python | 멀티 에이전트 역할 기반 | Python only |
| **AutoGen** | Python | Microsoft, 대화형 멀티 에이전트 | 복잡한 설정 |
| **Semantic Kernel** | C#/Python | Microsoft, AI 오케스트레이션 | .NET 의존 |
| **Claude Code** | TypeScript | Anthropic, 터미널 기반 | Node.js 필요 |
| **Codex CLI** | TypeScript | OpenAI, 터미널 기반 | Node.js 필요 |
| **alchemy** | **C99** | **136KB, 0 의존성, 독립 실행** | 유일무이 |

**면접 포인트:** "대부분의 에이전트 프레임워크가 Python/Node.js에 의존하는 반면, alchemy는 C99 단일 바이너리(136KB)로 동작합니다. 이는 임베디드/엣지 환경이나 리소스가 제한된 서버에서의 AI Agent 운영이 가능함을 의미합니다. FuriosaAI의 NPU와 결합하면 온디바이스 Agent 실행까지 확장 가능합니다."

---

## 8. CRAFT 9계층 파이프라인 (심화)

| 계층 | 기능 | 학술 용어 |
|:----:|:-----|:---------|
| L1 | Task 수신 | Task Parsing |
| L2 | 진단 (Socrates) | Meta-cognition |
| L3 | 경로 선택 (Router) | Decision Making |
| L4 | 실행 (Pipeline) | Execution |
| L5 | 도구 호출 | Tool Use |
| L6 | 검증 (Hook) | Verification |
| L7 | 자기 비판 (FIRE) | Self-critique / Reflection |
| L8 | 결과 통합 | Aggregation |
| L9 | 저장/보고 (Library) | Memory Consolidation |

**CRITICALITY 점수:** 작업 중요도를 0-10으로 정량화. 높은 점수 = 더 많은 검증 단계 필요.
**FIRE 필터:** 출력이 기준을 통과하지 못하면 재생성. (Filtered Inference for Reliable Execution)

---

## 9. 예상 면접 질문

### 기본 개념
1. "Agent가 무엇이라고 생각하나요?"
2. "ReAct 패턴에 대해 설명해보세요."
3. "Tool Calling은 어떻게 동작하나요?"

### 시스템 설계
4. "멀티 에이전트 시스템에서 오케스트레이션은 어떻게 설계해야 하나요?"
5. "Context Window 한계를 어떻게 극복할 수 있나요?"
6. "에이전트 시스템의 메모리는 어떻게 설계해야 하나요?"
7. "LLM 호출 실패/지연에 어떻게 대응하나요?"

### alchemy 기반 (강점)
8. "직접 만든 에이전트 프레임워크(alchemy)의 아키텍처를 설명해보세요."
9. "왜 C99로 만들기로 결정했나요? Python보다 어떤 장점이 있나요?"
10. "CRAFT 9계층 파이프라인의 CRITICALITY 점수는 어떻게 계산하나요?"
11. "fork+pipe 서브에이전트의 프로세스 격리 전략을 설명해보세요."
12. "15개 스킬 엔진의 PIPE Protocol은 어떻게 설계했나요?"

### 실제 경험
13. "가장 어려웠던 기술적 문제와 해결 방법은?"
14. "FuriosaAI의 Agent System 팀에서 어떤 역할을 하고 싶나요?"
15. "앞으로 에이전트 시스템이 어떻게 발전할 거라고 생각하나요?"

---

## 10. 모르는 질문 대처법

1. **솔직하게** — "그건 잘 모르겠습니다. 하지만 alchemy에서 이렇게 비슷한 문제를 해결한 경험이 있습니다."
2. **경험 연결** — "이론적으로 깊이 아는 건 아니지만, 실제로 구현해본 경험으로 말씀드리면..."
3. **질문 반전** — "그 부분은 제가 더 공부해야 할 것 같습니다. 혹시 추천 자료가 있으신가요?"

> **핵심:** FuriosaAI는 "이론만 아는 사람"보다 "실제로 만들어본 사람"을 원한다.
> alchemy 136KB C99 구현 경험은 어떤 이론서보다 강력한 증거다.
