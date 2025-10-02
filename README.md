# AMUGEONA — 중고거래 플랫폼 (Spring Boot + MySQL)

## Team Overview
- 인원 5명 / 기간 5주 / 역할 분담
  - 강효조(팀장): 기획, ERD 설계, Security, Signup, Form Login/Logout, OAuth, MyPage, User, Profile, Admin, Report/Block, Swagger 문서화
  - 우승우: 주문/결제, 리뷰, uploads
  - 이상혁: Listing, 채팅, Region, Category, Search, 이달의 판매왕
  - 김해민: 상점페이지, Follow, 1:1문의, 자주하는질문, header/footer, AWS배포
  - 박유진: 공지사항

## My Role & Contributions
- [Auth/MFA] 폼 로그인 → Security/OAuth 전환, TOTP 등록/검증/재인증 플로우
  - 문제: 기존 폼 로그인과 보안 정책 충돌
  - 해결: CSRF 쿠키 전략, 세션 재인증 인터셉터, 에러 모델 통일
  - 효과: 로그인 실패율 ↓, 민감 액션 보안 강화
  - 증빙: PR #12, #18 / 커밋 1a2b3c / 시퀀스 다이어그램(`/docs/mfa-flow.png`)
- [Listings] 멀티파트 업로드(사진) + 검색/정렬 + Swagger 스펙 작성
  - 문제: JSON+파일 혼합 업로드 불안정
  - 해결: `@RequestPart` 구조, S3 프리사인(또는 로컬) 분리
  - 효과: 업로드 성공률↑, 문서 신뢰도↑
  - 증빙: PR #27 / `/docs/openapi.yaml` 해당 섹션
- [Reports]
  - 신고-정지-해제 워크플로우

## Other Team Work (Summary)
- 주문/결제(우승우): 결제 사전등록/완료/취소 플로우 구현  
- 채팅(이상혁): WebSocket 기반 실시간 채팅
> 각 파트 코드는 원 저장소 참조. 본 레포에는 **문서/스펙/스크린샷**만 포함.

## 🔗 Quick Links
- OpenAPI (YAML): [docs/openapi.yaml](docs/openapi.yaml)
- API 문서 (Redoc, GitHub Pages): https://torye2.github.io/portfolio/api-redoc.html
- 기능 명세서(Functional Spec): [docs/AMGN_Functional_Spec_v1.0_2025-10-01.md](docs/AMGN_Functional_Spec_v1.0_2025-10-01.md)
- 코드 저장소(실행용): https://github.com/torye2/AMGN

## 개요
- Spring Boot + MySQL 기반 마켓플레이스. 인증/보안과 성능 최적화를 중점으로 구현.
- 핵심 기능: 회원/로그인(OAuth, MFA), 상품 등록·검색·상세, 주문/결제, 리뷰, 찜/팔로우, 신고/관리자.

## 아키텍처(요약)
- Backend: Java 21, Spring Boot 3.x, Spring Security, JPA/MyBatis
- DB: MySQL 8 (InnoDB, 복합 인덱스)
- Infra/Dev: Gradle, (문서) Swagger UI / Redoc
- Observability: (도입 준비) Micrometer/Prometheus

## 내가 한 일 (문제 → 해결 → 효과)
- 인증/보안: 정적 폼 + CSRF 쿠키/헤더 매칭, 세션 하드닝 → 로그인 안정화
- DB 성능: 정규화·복합 인덱스, 슬로우쿼리/EXPLAIN → 목록/상세 p95 개선
- 에러 표준화: 4xx/5xx 응답 모델 통일 → 실패율↓, 디버깅 속도↑

## 실행 방법 (코드 레포)
```bash
git clone https://github.com/torye2/AMGN.git
cd AMGN
./gradlew bootRun   # 환경변수/설정은 코드 레포 문서 참고
```
## 스크린샷
> 아래 경로에 캡처 이미지를 넣고 파일명을 맞춰 주세요.
>
> `docs/screenshots/swagger.png`, `docs/screenshots/listing-detail.png`
>
> (예: Swagger UI, 상품 상세, MFA 등록)

![Swagger UI](docs/screenshots/swagger.png)
![상품 상세](docs/screenshots/listing-detail.png)

## 라이선스 & 문의
- MIT License
- 문의: <your-email@example.com> 또는 GitHub Issues

## 로드맵
- [ ] 결제 모듈 실결제 연동
- [ ] 검색 고도화(카테고리·지역·키워드 복합)
- [ ] 알림(거래 상태/채팅/팔로우)
- [ ] CI/CD로 문서 자동 배포
