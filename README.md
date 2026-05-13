# Secure-SDL-JWT-Storage-methods-research
선문대학교 보안응용프로젝트(2026.05.01 ~ 2026.06.15. 매주 6시간 강의)
주제: JWT 저장방식(Session, Local, Cookie)에 따른 취약점 분석/비교 및 최적의 인증 아키텍처 제안
팀 구성: 차무관(팀장), 전희재, 조성빈
연구 방법: 
  1. OSS에 공개된 200~300개의 JWT 인증 시스템 리스트업 후 저장방식 유형 분류
     -유형 1: 로그인을 완료한 후 JWT를 브라우저의 LocalStorage에 저장하고, 이후 API 요청 시 Authorization 헤더에 담아 전송하는 아키텍처
     -유형 2: JWT를 브라우저의 SessionStorage에 저장하고 활용하는 아키텍처
     -유형 3: JWT를 서버 측에서 발급할 때 HttpOnly 및 Secure 플래그를 설정하여 브라우저 Cookie에 자동 저장되도록 하는 아키텍처
  2. 각 유형에 대해 취약점 분석 도구로 테스팅(OWASP ZAP, OWASP Juice Shop 등)
  3. 유형 별 취약점 분석 및 대응방안 제시
