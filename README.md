# AMUGEONA — 중고거래 플랫폼 (Spring Boot + MySQL)

> **핵심 지표**  
> HTTP p95 ~74ms · Error rate 0.00% · Login success 100% (k6 5 VUs × 1m, local)  
> List/Detail p95 ~15.6ms (GET /product/list, /product/{id})

## 개요
- Spring Boot + MySQL 기반 마켓플레이스. 인증/보안과 성능 최적화를 중점으로 구현.
- 핵심 기능: 회원/로그인, 상품 등록·검색·상세, 제안/거래, 리뷰, 즐겨찾기.

## 아키텍처(요약)
- Backend: Java 21, Spring Boot 3.x, Spring Security, JPA/MyBatis
- DB: MySQL 8 (InnoDB, 복합 인덱스, 슬로우쿼리/EXPLAIN)
- Infra/Dev: Gradle, Docker(로컬), GitHub Actions(배포 준비)
- Observability: Micrometer/Prometheus(도입 준비), 표준 로그
<!-- 다이어그램 이미지 자리 -->
<!-- ![architecture](./docs/images/arch.png) -->

## 내가 한 일 (문제 → 해결 → 효과)
- **인증/보안**: 정적 로그인 폼 + CSRF 쿠키/헤더 매칭, 세션 하드닝(SameSite 등) → 로그인 안정화
- **DB 성능**: 정규화·복합 인덱스 설계, 슬로우쿼리/실행계획 튜닝 → 목록/상세 p95 개선
- **지표화**: k6 시나리오(로그인/목록/상세) + 임계값(threshold) 세팅 → 품질 지표 확보/자동 확인
- **오류 개선**: 4xx/5xx 에러 핸들링 표준화, 404 설계 분리로 실패율 0% 유지

## 실행 방법 (로컬)
```bash
git clone https://github.com/torye2/AMGN.git
cd AMGN
# 환경변수 파일 준비 (.env 참고)
./gradlew bootRun
```
## 스크린샷
<!-- 썸네일 2~3장 먼저, 상세는 /docs/images에 저장 -->
<!--
![list](./docs/images/list.png)
![detail](./docs/images/detail.png)
-->
