# 👁️ Oculus — UI 분석 엔진

> **버전:** v0.4 | **역할:** UI 분석 / 오류 진단 / 데이터 추출 3모드

Oculus는 웹 인터페이스를 다각도로 분석하는 비전 엔진입니다. **UI Analysis Mode**(스크린샷/DOM 기반 구조 분석), **Error Diagnosis Mode**(콘솔 오류·네트워크 실패·렌더링 버그 진단), **Data Extraction Mode**(구조화된 데이터 추출 및 JSON 변환)의 3가지 모드를 제공합니다. 기본 OCR 엔진이 실패할 경우 **Tesseract OCR**을 fallback으로 사용하여 텍스트 인식 내성을 확보합니다.

---

## 핵심 기능

| 기능 | 설명 |
|:-----|:------|
| **UI Analysis Mode** | 스크린샷 및 DOM 트리 기반으로 인터페이스 구조 분석, 컴포넌트 식별, 레이아웃 계층 추출 |
| **Error Diagnosis Mode** | 콘솔 에러 로그, 네트워크 실패 응답, 렌더링 버그(레이아웃 쉬프트, 깨짐) 자동 진단 |
| **Data Extraction Mode** | 웹페이지에서 테이블, 리스트, 폼 데이터 등 구조화된 정보 추출 → JSON 변환 |
| **Tesseract OCR Fallback** | 기본 비전 모델이 텍스트 인식에 실패할 경우 Tesseract OCR로 자동 fallback |
| **PIPE 통합 출력** | 분석 결과(컴포넌트 트리, 오류 목록, 추출 데이터)를 파이프라인에 JSON으로 전달 |

---

## 3모드 비교

| 모드 | 입력 | 출력 | 사용 예시 |
|:----|:----|:----|:---------|
| **UI Analysis** | 스크린샷 / DOM HTML | 컴포넌트 트리, 태그 매트릭스 | 페이지 구조 리버스 엔지니어링 |
| **Error Diagnosis** | 콘솔 로그, 네트워크 HAR | 오류 원인, 영향 범위, 수정 제안 | 디버깅 / QA 자동화 |
| **Data Extraction** | HTML / 스크린샷 | JSON (정형 데이터) | 리드 추출, 가격 모니터링 |

---

## YAML 명세

```yaml
name: Oculus
version: 0.4
trigger: UI 분석, 오류 진단, 또는 데이터 추출 요청
input:
  format: PIPE Protocol (JSON)
  schema:
    mode: "ui_analysis" | "error_diagnosis" | "data_extraction"
    source: "screenshot" | "dom" | "console_logs" | "network_logs"
    payload: string (base64 screenshot or raw HTML/log)
output:
  format: PIPE Protocol (JSON)
  schema:
    components: [{ type, selector, bounding_box, properties }]
    errors: [{ severity, type, message, line, suggestion }]
    extracted_data: [{ field, value, confidence }]
    ocr_fallback_used: boolean
dependencies: []
```

---

> **Pipeline:** Oculus(분석) → Picasso(디자인 리뷰) → Argo(UX 진단) → Disney(애니메이션 평가)
