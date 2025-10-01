# AMUGEONA — 중고거래 플랫폼 (Spring Boot + MySQL)

> 이 저장소는 **문서/포트폴리오 레포**입니다. 실행 코드는 별도 저장소에 있어요.

## 🔗 Quick Links
- OpenAPI (YAML): [docs/openapi.yaml](docs/openapi.yaml)
- API 문서 (Redoc, GitHub Pages): https://torye2.github.io/portfolio/api-redoc.html
- 기능 명세서(Functional Spec): [docs/AMGN_Functional_Spec_from_OpenAPI.md](docs/AMGN_Functional_Spec_from_OpenAPI.md)
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
