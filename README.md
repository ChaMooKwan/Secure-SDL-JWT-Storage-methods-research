# 🛡️ 보안응용프로젝트 11분반 (2026)
### 브라우저 환경에서의 JWT 저장 방식 보안 취약점 분석 및 상황별 인증 아키텍처 제안 
### :OWASP ZAP 분석 결과를 중심으로

| 항목 | 상세 내용 |
| :--- | :--- |
| **소속** | 선문대학교 (Sun Moon University) |
| **기간** | 2026. 05. 01. ~ 2026. 06. 15. (매주 6시간 강의) |
| **팀 구성** | 차무관, 전희재, 조성빈 |
| **담당 교수** | 이택 |

---
## 📂 리포지토리 구조 (Repository Structure)

```text
jwt-storage-security-analysis/
├── 📁 report/
│   ├── 📁 local_storage/                         # Local Storage 기반 프로젝트 ZAP 취약점 분석 결과
│   └── 📁 cookies/                               # Cookies 기반 프로젝트 ZAP 취약점 분석 결과
├── 📝 Automative Searching for Github.ipynb  # GitHub JWT 프로젝트 자동 검색 프로그램
├── 📝 6팀 논문_브라우저 환경에서의 JWT 저장 방식 보안 취약점 분석 및 상황별 인증 아키텍처 제안 OWASP ZAP 분석 결과를 중심으로.pdf
└── 📝 README.md
---
## 📌 연구 논문 요약 📌
## 📌 프로젝트 개요
* [cite_start]현대 웹 애플리케이션에서 JWT(JSON Web Token)는 상태를 유지하지 않는(Stateless) 인증의 표준으로 자리 잡았습니다[cite: 10, 40].
* [cite_start]그러나 발급된 토큰을 브라우저의 어느 공간에 저장할지에 대한 보안적 고려 없이 관행적으로 아키텍처를 채택하는 경우가 다수 존재합니다[cite: 10, 45].
* [cite_start]본 연구는 브라우저 환경에서 JWT를 저장하는 주요 방식(Local Storage, Cookies 등)의 보안 특성과 구현 난이도를 비교 분석합니다[cite: 11, 48].
* [cite_start]서비스의 보안 민감도, 구현 난이도, 출처(Origin) 구성 환경을 종합적으로 고려하여 4가지 상황 맞춤형 JWT 인증 아키텍처를 제안합니다[cite: 15].

## 🔬 연구 및 분석 방법
* [cite_start]JWT 인증을 사용하는 GitHub 오픈소스 프로젝트를 수집하여 저장 방식별로 분류하였습니다[cite: 12, 124].
* [cite_start]자동화 취약점 진단 도구인 OWASP ZAP을 활용하여 CSP 미설정, CORS 오류, 쿠키 보안 속성 누락 등 저장 방식별 취약점을 분석하였습니다[cite: 12, 49].

## 📊 주요 분석 결과
* [cite_start]**Local Storage 기반:** 구현 편의성이 높으나, XSS(Cross-Site Scripting) 공격을 통한 직접적인 토큰 탈취 위험에 취약합니다[cite: 13, 257, 258]. [cite_start]분석 대상 프로젝트 모두에서 CSP Header 미설정 및 CORS 관련 오류가 확인되었습니다[cite: 218].
* [cite_start]**Cookies 기반:** `HttpOnly` 속성을 통해 XSS 방어에는 유리하지만 [cite: 14, 264][cite_start], 쿠키가 자동 전송되므로 CSRF 방어를 위한 추가 대책이 요구됩니다[cite: 14, 44, 312]. [cite_start]교차 출처(Cross-Origin) 환경에서는 설정 복잡도가 크게 증가하는 한계를 보입니다[cite: 14, 269].
* [cite_start]**Hybrid (Local Storage + Cookie) 기반:** Access Token과 Refresh Token의 역할을 분리하여 토큰 탈취 시 피해 범위를 제한할 수 있지만 [cite: 273, 274][cite_start], 토큰 갱신 로직 등이 추가되어 구현 난이도가 가장 높습니다[cite: 277, 283].

## 💡 상황별 JWT 인증 아키텍처 제안

### 1. 소규모 서비스 (구현 편의성 우선)
* [cite_start]**권장 구조:** Local Storage 기반 인증[cite: 301].
* [cite_start]**고려사항:** 구현이 단순하여 내부 테스트나 프로토타입에 적합합니다[cite: 302, 303]. [cite_start]단, 장기 인증 토큰 저장을 지양하고 Access Token 만료 시간을 짧게 설정하며 XSS 방어 기법을 필수적으로 적용해야 합니다[cite: 305].

### 2. 일반적인 웹 서비스 (동일 출처, Same-Origin)
* [cite_start]**권장 구조:** `HttpOnly` 및 `SameSite`가 설정된 Cookie 기반 인증[cite: 308, 313].
* [cite_start]**고려사항:** 동일 출처 환경에서는 CORS 설정 부담이 낮으며 [cite: 309][cite_start], `HttpOnly` 속성을 통해 JavaScript 기반의 토큰 탈취 위험을 크게 줄일 수 있습니다[cite: 311]. [cite_start]단, CSRF 방어 기법이 함께 적용되어야 합니다[cite: 312].

### 3. SPA와 API 서버가 분리된 교차 출처 (Cross-Origin) 환경
* [cite_start]**권장 구조:** Cross-Origin Cookie 기반 인증[cite: 316, 335].
* [cite_start]**고려사항:** 엄격한 CORS 설정(`Access-Control-Allow-Origin`, `Access-Control-Allow-Credentials`)과 클라이언트 측의 `credentials` 옵션 활성화가 필요합니다[cite: 318, 319]. [cite_start]`Secure` 및 `SameSite` 속성 설정 누락을 방지하기 위한 점검이 요구됩니다[cite: 320, 322].

### 4. 보안 민감도가 높은 서비스 (개인정보, 결제 등)
* [cite_start]**권장 구조:** Access Token과 Refresh Token을 분리한 Hybrid 인증 구조[cite: 325].
* [cite_start]**고려사항:** 짧은 수명의 Access Token을 사용하고 [cite: 327][cite_start], Refresh Token은 `HttpOnly` Cookie에 저장하여 피해 범위를 최소화합니다[cite: 327]. [cite_start]Refresh Token Rotation 기법을 함께 고려하는 것이 바람직합니다[cite: 329].
