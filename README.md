# 🛡️ 보안응용프로젝트 (2026)
### JWT 저장 방식에 따른 취약점 분석 및 최적의 인증 아키텍처 제안

| 항목 | 상세 내용 |
| :--- | :--- |
| **소속** | 선문대학교 (Sun Moon University) |
| **기간** | 2026. 05. 01. ~ 2026. 06. 15. (매주 6시간 강의) |
| **팀 구성** | 차무관, 전희재, 조성빈 |

---

## 📝 프로젝트 개요
본 프로젝트는 현대 웹 서비스에서 가장 널리 쓰이는 **JWT(JSON Web Token)** 인증 방식의 보안성을 심층 분석합니다. 특히 브라우저 내 저장 위치(**LocalStorage, SessionStorage, Cookie**)에 따라 발생하는 보안 위협을 비교 실험하고, 이를 보완할 수 있는 최적의 인증 아키텍처를 도출하는 것을 목적으로 합니다.

---

## 🔍 연구 방법 및 단계

### 1. 인증 시스템 유형 분류
오픈소스 소프트웨어(OSS)에 공개된 **약 200~300개의 JWT 인증 시스템**을 전수 조사하여, 데이터 저장 방식에 따라 다음과 같이 3가지 핵심 유형으로 분류합니다.

*   **유형 1: LocalStorage 기반**
    *   로그인 완료 후 JWT를 브라우저 `LocalStorage`에 저장.
    *   API 요청 시 `Authorization` 헤더에 토큰을 포함하여 전송.
*   **유형 2: SessionStorage 기반**
    *   브라우저 탭 세션 동안만 유지되는 `SessionStorage`를 활용한 아키텍처.
*   **유형 3: HttpOnly Cookie 기반**
    *   서버에서 JWT 발급 시 `HttpOnly` 및 `Secure` 플래그를 설정.
    *   브라우저 쿠키에 자동 저장 및 전송되도록 설계된 아키텍처.

### 2. 보안 취약점 테스팅
검증된 보안 도구 및 환경을 활용하여 각 아키텍처의 견고함을 테스트합니다.
*   **도구:** `OWASP ZAP`, `Burp Suite`
*   **환경:** `OWASP Juice Shop` 등 취약점 분석용 모의 해킹 환경 활용

### 3. 결과 분석 및 대응방안 제시
*   각 유형별 **XSS(Cross-Site Scripting)** 및 **CSRF(Cross-Site Request Forgery)** 공격에 대한 노출 정도 분석.
*   분석 결과를 바탕으로 보안성과 사용자 편의성을 모두 고려한 **최적의 인증 가이드라인** 제시.

---

## 🛠️ 주요 활용 기술
*   **Authentication:** JSON Web Token (JWT) Storage
*   **Security Tools:** OWASP ZAP
*   **Analysis:** Dynamic Analysis of Web Architectures
