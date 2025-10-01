# portfolio

AMGN 중고거래 플랫폼 — 포트폴리오 문서

요약: Spring Boot + MySQL 기반 중고거래 서비스. 로그인/OAuth/MFA, 상품 등록·검색, 주문/결제, 리뷰, 찜/팔로우, 신고/관리자 기능을 포함합니다. 이 저장소는 문서 중심 포트폴리오이며, 실행 코드는 별도 저장소에 있습니다.

🔗 Quick Links

기능 명세서(Functional Spec): /docs/AMGN_Functional_Spec_from_OpenAPI.md

OpenAPI 스펙(YAML): /docs/openapi.yaml

(선택) Redoc 문서: /docs/api-redoc.html

데모/시연 영상: (업로드 후 링크)

운영/개발 저장소(코드): (별도 repo 링크)

1. 프로젝트 개요

목표: 개인 간 중고거래의 신뢰와 편의성을 높이는 거래 플랫폼 구현

핵심 가치: 안전한 인증(이중 인증), 간결한 거래 흐름, 분쟁 최소화(리뷰/신고 체계)

역할: 기획 · 백엔드 · 일부 프론트(HTML/CSS/JS) · 데이터 모델링

2. 핵심 기능

인증/계정: 이메일 로그인, OAuth(구글/카카오/네이버), MFA(TOTP), 세션 보안

상품(Listings): 등록/수정/삭제, 상태(판매중/예약/완료), 사진 업로드, 검색/필터

거래/결제: 주문 생성 → 결제 사전등록 → 결제 완료 → 인도/완료, 취소/분쟁 플로우

리뷰/평판: 거래 기반 리뷰 작성/수정/삭제, 판매자 평판 요약

관계 기능: 찜(관심상품), 팔로우(판매자), 문의/FAQ, 채팅(기본)

운영/관리: 신고 접수 → 관리자 조치(정지/해제), 이달의 판매왕 집계

상세 경로와 파라미터는 OpenAPI 문서를 참고하세요: /docs/openapi.yaml

3. 아키텍처 & 기술 스택

Backend: Spring Boot (Java 21), Spring Security, OAuth2 Client, MyBatis/JPA 혼합

DB: MySQL 8 (InnoDB, utf8mb4), 인덱스 최적화 및 정규화 설계

Infra(개발): Swagger UI(Springdoc), Actuator, (선택) Cloudflare Tunnel / ngrok

Build/IDE: Gradle, IntelliJ IDEA

기타: AES-GCM(백업코드), ZXing(QR), java-otp(TOTP)

4. API 문서

YAML(권장): /docs/openapi.yaml

Redoc(정적 HTML): /docs/api-redoc.html

기능 명세서: Swagger 스펙을 바탕으로 도메인·플로우 중심으로 재구성 → /docs/AMGN_Functional_Spec_from_OpenAPI.md

5. 데이터 모델(요약)

주요 테이블: users, oauth_identities, mfa_secrets, listings, listings_photos, orders, reviews, user_addresses, follows, wishes …

인덱스: 상태/작성일/지역 기반 조회 최적화, FK 일관성 유지
(ERD 이미지는 추후 첨부: /docs/erd.png 등)

6. 보안 & 운영(NFR 요약)

보안: HTTPS 전제, CSRF 보호, 세션 고정화 방지, 민감 액션에 MFA 재검증

성능: 목록/검색 인덱스, 이미지 업로드 분리(CDN 고려)

가용성: 헬스체크(/actuator/health), 장애 응답 템플릿

관측성: 구조화 로깅, 에러/트레이싱 대시보드(도입 용이한 형태로 설계)

7. 스크린샷 / 시연

Swagger UI 캡처, 주요 화면(상품 상세/주문/리뷰/MFA 등록 등)
(예시 이미지 경로: /docs/screenshots/swagger.png, /docs/screenshots/listing-detail.png)

8. 개발 기록(선택)

문제 해결 사례: 기존 Form 로그인 → Spring Security & OAuth 전환 시 충돌 해결, CSRF 토큰 쿠키 전략, 세션 기반 재인증 플로우

트러블슈팅: 사진 업로드 경로, 포트 충돌(8080), MyBatis 예외, 로그인 세션 전달 등

배운 점: 보안/운영 관점 설계 중요성, 명세 주도 개발의 효율

9. 로드맵

 결제 모듈 실결제 연동(테스트 가맹점 → 실가맹)

 검색 고도화(키워드/카테고리/지역 복합 필터)

 알림(거래 상태 변경/채팅/팔로우 업데이트)

 배포 자동화(GitHub Actions)

10. 라이선스 & 문의

MIT License

문의: your-email@example.com
 / GitHub Issues
