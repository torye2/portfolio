# 기능 명세서 (Functional Spec) — 생성 기준 OpenAPI: **OpenAPI definition v0**

- 생성시각: 2025-10-01 06:57
- 총 엔드포인트: **121개**


## 1. 범위(Scope)
본 문서는 제공된 OpenAPI 스펙(`/v3/api-docs`)을 기준으로 실제 사용자 시나리오에 맞춰 기능을 정리합니다. 프론트/백엔드/QA가 공통 레퍼런스로 사용할 수 있도록 도메인별 기능과 주요 흐름을 요약합니다.

## 2. 사용자/역할(Actors & Roles)
- **비회원**: 브라우징, 검색 일부
- **일반 사용자(구매자/판매자)**: 상품등록/주문/리뷰/팔로우/찜/프로필/주소 관리
- **관리자**: 신고 처리, 제재(정지/해제), 시스템 점검

## 3. 주요 도메인 & 대표 플로우

### 상품(리스트/상세/작성/수정/찜/검색)
- 관련 엔드포인트 수: **17**
- 대표 경로 예시:

  - `POST /product/{listingId}/edit`
  - `POST /product/write`
  - `GET /product/{listingId}`
  - `DELETE /product/{listingId}`
  - `GET /product/{id}/related`
  - `GET /product/seller/{sellerId}/products`
  - … (총 17개)

### 주문/결제/배송상태
- 관련 엔드포인트 수: **23**
- 대표 경로 예시:

  - `PUT /orders/reviews/{reviewId}`
  - `DELETE /orders/reviews/{reviewId}`
  - `GET /orders`
  - `POST /orders`
  - `POST /orders/{orderId}/tracking`
  - `POST /orders/{orderId}/revert`
  - … (총 23개)

### 리뷰(작성/조회/수정/삭제)
- 관련 엔드포인트 수: **12**
- 대표 경로 예시:

  - `PUT /api/reviews/{reviewId}`
  - `DELETE /api/reviews/{reviewId}`
  - `POST /api/reviews`
  - `GET /api/reviews/seller/{sellerId}`
  - `GET /api/reviews/seller/{sellerId}/summary`
  - `GET /api/reviews/received`
  - … (총 12개)

### 인증/MFA/계정관리
- 관련 엔드포인트 수: **20**
- 대표 경로 예시:

  - `GET /debug/session`
  - `POST /api/oauth/unlink`
  - `GET /api/oauth/reauth/{provider}`
  - `GET /api/oauth/me`
  - `GET /api/oauth/connect/{provider}`
  - `GET /api/user/status`
  - … (총 20개)

### 프로필/주소/팔로우/샵
- 관련 엔드포인트 수: **19**
- 대표 경로 예시:

  - `GET /api/user/profile`
  - `PUT /api/user/profile`
  - `POST /api/user/verify-password`
  - `GET /api/addresses/{id}`
  - `PUT /api/addresses/{id}`
  - `DELETE /api/addresses/{id}`
  - … (총 19개)

### 신고/관리자/시스템
- 관련 엔드포인트 수: **10**
- 대표 경로 예시:

  - `POST /api/reports`
  - `POST /api/reports/{id}/evidence`
  - `POST /api/admin/suspensions/{id}/revoke`
  - `POST /api/admin/reports/{id}/suspend`
  - `POST /api/admin/reports/{id}/actions`
  - `GET /api/admin/users/{userId}/suspensions`
  - … (총 10개)

### 채팅/문의/FAQ
- 관련 엔드포인트 수: **14**
- 대표 경로 예시:

  - `POST /api/chat/room/open`
  - `GET /chat/rooms`
  - `GET /chat/messages`
  - `GET /api/chat/rooms`
  - `GET /api/chat/room`
  - `GET /api/inquiries`
  - … (총 14개)


## 4. API 상세(태그별)

### order-controller  
총 20개

| Method | Path | Summary |
|---|---|---|
| GET | `/orders` | getOrders |
| POST | `/orders` | create |
| GET | `/orders/buy` | getBuyOrders |
| POST | `/orders/reviews` | createReview |
| GET | `/orders/reviews/orders/{orderId}` | getReviewsByOrder |
| DELETE | `/orders/reviews/{reviewId}` | deleteReview |
| PUT | `/orders/reviews/{reviewId}` | updateReview |
| GET | `/orders/sell` | getSellOrders |
| DELETE | `/orders/{orderId}` | deleteOrder |
| DELETE | `/orders/{orderId}/cancel` | cancel |
| POST | `/orders/{orderId}/cancel-by-seller` | cancelBySeller |
| POST | `/orders/{orderId}/complete` | complete |
| POST | `/orders/{orderId}/confirm-delivery` | delivered |
| POST | `/orders/{orderId}/confirm-meetup` | confirmMeetup |
| POST | `/orders/{orderId}/dispute` | dispute |
| POST | `/orders/{orderId}/pay` | payDefault |
| POST | `/orders/{orderId}/pay/inicis` | payInicis |
| POST | `/orders/{orderId}/pay/kakao` | payKakao |
| POST | `/orders/{orderId}/revert` | revertCancel |
| POST | `/orders/{orderId}/tracking` | inputTracking |


### listing-controller  
총 11개

| Method | Path | Summary |
|---|---|---|
| GET | `/product/all` | getAllProducts |
| GET | `/product/category/{categoryId}` | getProductsByCategory |
| GET | `/product/list` | list_1 |
| GET | `/product/my-products` | getMyProducts |
| GET | `/product/region/{regionId}` | getProductsByRegion |
| GET | `/product/seller/{sellerId}/products` | getProductsBySeller |
| POST | `/product/write` | writeListing |
| GET | `/product/{id}/related` | getRelatedProducts |
| DELETE | `/product/{listingId}` | deleteListing |
| GET | `/product/{listingId}` | getProductDetail |
| POST | `/product/{listingId}/edit` | editListing |


### report-controller  
총 8개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/admin/reports` | list_3 |
| GET | `/api/admin/reports/{id}` | detail |
| POST | `/api/admin/reports/{id}/actions` | addAction |
| POST | `/api/admin/reports/{id}/suspend` | suspend |
| POST | `/api/admin/suspensions/{id}/revoke` | revoke |
| GET | `/api/admin/users/{userId}/suspensions` | list_2 |
| POST | `/api/reports` | create_1 |
| POST | `/api/reports/{id}/evidence` | addEvidence |


### review-controller  
총 8개

| Method | Path | Summary |
|---|---|---|
| POST | `/api/reviews` | createReview_1 |
| GET | `/api/reviews/mine` | myOrders |
| GET | `/api/reviews/orders/{orderId}` | getReviews |
| GET | `/api/reviews/received` | receivedReviews |
| GET | `/api/reviews/seller/{sellerId}` | getSellerReviews |
| GET | `/api/reviews/seller/{sellerId}/summary` | getSellerReviewsSummary |
| DELETE | `/api/reviews/{reviewId}` | deleteReview_1 |
| PUT | `/api/reviews/{reviewId}` | updateReview_1 |


### user-follow-controller  
총 7개

| Method | Path | Summary |
|---|---|---|
| DELETE | `/api/follows/{sellerId}` | unfollow |
| POST | `/api/follows/{sellerId}` | follow |
| GET | `/api/follows/{sellerId}/count` | count |
| GET | `/api/follows/{sellerId}/followers` | followers |
| GET | `/api/follows/{sellerId}/me` | myFollowStatus |
| GET | `/api/follows/{userId}/following` | following |
| GET | `/api/follows/{userId}/following/count` | followingCount |


### address-controller  
총 6개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/addresses` | list |
| POST | `/api/addresses` | create_2 |
| DELETE | `/api/addresses/{id}` | delete |
| GET | `/api/addresses/{id}` | get |
| PUT | `/api/addresses/{id}` | update |
| PATCH | `/api/addresses/{id}/default` | setDefault |


### chat-controller  
총 5개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/chat/room` | getRoom |
| POST | `/api/chat/room/open` | openRoom |
| GET | `/api/chat/rooms` | getChatRooms |
| GET | `/chat/messages` | getMessages |
| GET | `/chat/rooms` | getSellerRooms |


### inquiry-api-controller  
총 5개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/inquiries` | getAllInquiriesForAdmin |
| POST | `/api/inquiries` | createInquiry |
| GET | `/api/inquiries/my` | getMyInquiries |
| GET | `/api/inquiries/{inquiryId}/replies` | getRepliesForInquiry |
| POST | `/api/inquiries/{inquiryId}/replies` | replyToInquiry |


### listing-wish-controller  
총 5개

| Method | Path | Summary |
|---|---|---|
| GET | `/product/wish/my` | myWishes |
| GET | `/product/wish/my/count` | myWishCount |
| DELETE | `/product/{listingId}/wish` | removeWish |
| GET | `/product/{listingId}/wish` | getWishStatus |
| POST | `/product/{listingId}/wish` | toggleWish |


### mfa-controller  
총 5개

| Method | Path | Summary |
|---|---|---|
| POST | `/api/mfa/totp/activate` | activate |
| POST | `/api/mfa/totp/disable` | disable |
| GET | `/api/mfa/totp/setup` | setup |
| GET | `/api/mfa/totp/status` | status_1 |
| POST | `/api/mfa/totp/verify` | verify |


### faq-api-controller  
총 4개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/faqs` | listFaqs |
| POST | `/api/faqs` | createFaq |
| DELETE | `/api/faqs/{id}` | deleteFaq |
| PUT | `/api/faqs/{id}` | updateFaq |


### oauth-controller  
총 4개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/oauth/connect/{provider}` | connect |
| GET | `/api/oauth/me` | me |
| GET | `/api/oauth/reauth/{provider}` | reauth |
| POST | `/api/oauth/unlink` | unlink |


### find-controller  
총 3개

| Method | Path | Summary |
|---|---|---|
| POST | `/api/find-id` | findId |
| POST | `/api/pw-reset/check` | verifyAndToken |
| POST | `/api/pw-reset/commit` | resetPassword |


### geo-controller  
총 3개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/geo/coord2regioncode` | reverse_2 |
| GET | `/api/geo/coord2reverse` | reverse |
| GET | `/api/geo/reverse` | reverse_1 |


### payment-controller  
총 3개

| Method | Path | Summary |
|---|---|---|
| POST | `/payment/complete` | completePayment |
| GET | `/payment/payment/test-pre-register/{orderId}/{amount}` | testPreRegister |
| POST | `/payment/prepare` | preparePayment |


### profile-controller  
총 3개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/user/profile` | getProfile |
| PUT | `/api/user/profile` | updateProfile |
| POST | `/api/user/verify-password` | verifyPassword |


### shop-controller  
총 3개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/shop/{sellerId}` | getShop |
| POST | `/api/shop/{sellerId}` | upsertShopProfile |
| PUT | `/api/shop/{sellerId}` | upsertShopProfile_1 |


### user-controller  
총 3개

| Method | Path | Summary |
|---|---|---|
| DELETE | `/api/user/delete` | deleteMe |
| GET | `/api/user/me` | getLoginUser |
| GET | `/api/user/nickname/{userId}` | getNickname |


### category-controller  
총 2개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/categories` | getCategories |
| GET | `/api/categories/{parentId}` | getSubCategories |


### region-controller  
총 2개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/regions` | regions |
| GET | `/api/suggest` | suggest |


### auth-status-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/user/status` | status |


### award-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/awards/top-sellers` | topSellers |


### csrf-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/csrf` | csrf |


### flash-msg-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/flash` | getFlashMsg |


### listing-search-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/listings/search` | searchByTitle |


### login-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/debug/session` | session |


### onboarding-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| POST | `/api/onboarding` | complete_1 |


### region-resolve-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/regions/resolve` | resolve |


### search-redirect-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/search` | redirectToProductSearch |


### system-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/system/uploads/diagnose` | diagnoseUploads |


### user-check-controller  
총 1개

| Method | Path | Summary |
|---|---|---|
| GET | `/api/users/exist` | checkId |


## 5. 공통 규격 제안
- **인증/보안**: 세션 또는 Bearer 기반 `securitySchemes` 명시, 인증 필요한 경로에 `security` 부착.
- **페이징/정렬**: `page,size,sort` 파라미터로 통일, 응답은 `content,totalElements,totalPages,page,size,sort` 권장.
- **에러 모델**: 전역 `ErrorResponse { code, message, detail }` 도입, 400/401/403/404/409/422/500 응답 정의.
- **파일 업로드**: `multipart/form-data` + `@RequestPart` 패턴으로 JSON/파일 분리.
- **버전관리**: 상위 prefix `/api/v1` 고정.

## 6. 비즈니스 규칙(추출)
- 주문 상태 전이: 주문 생성 → 결제 준비/요청 → 결제 완료 → 배송/만남 확인 → 완료, 중간에 취소/분쟁/되돌리기 경로 존재.
- 리뷰: 주문 단위 작성/조회/수정/삭제 지원, 판매자별 요약 제공.
- 찜/팔로우: 사용자 관심도 관리(토글), 카운트/목록 제공.
- MFA(TOTP): 등록/상태조회/검증/비활성화 제공, 민감행동 보호.
- 신고/제재: 신고 등록 → 관리자 검토 → 조치 추가/정지 → 해제.

## 7. 비기능 요구(요약)
- 보안: HTTPS, CSRF, CORS, 세션 하이재킹 방지, 감사 로그.
- 성능: 검색/목록 캐시, DB 인덱스 전략, 이미지 업로드 CDN 고려.
- 가용성: 장애 페이지, 헬스체크 `/actuator/health`.
- 관측성: 구조화 로깅, 트레이싱, 에러 대시보드.

## 8. 용어 사전(Glossary)
- Listing: 판매 상품 등록 단위
- Wish: 찜(관심상품)
- Follow: 판매자 팔로우
- Order: 주문(결제/배송 포함)
- Review: 거래 후 평가


---
*본 문서는 제공된 OpenAPI 스펙으로부터 자동 생성된 요약이며, 실제 구현과의 차이는 PR로 보정하십시오.*
