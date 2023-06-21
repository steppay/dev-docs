# 개발 문서 관리

# History
| 버전    | 설명        | 개정 이력      |
|-------|-----------|------------|
| 0.0.1 | 최초 작성     | 2023.06.16 |
| 0.1.0 | 개발 가이드 적용 | 2023.06.21 |

# TODO

### 결제
- 결제 검증 및 에러 핸들링
- 지원하는 결제수단- PG 부분에 특정 값들을 어디서찾아서 넣을 수 있는지 스크린샷 제공
- product-service 에서 Commit이 실패, 구독 생성이 실패 등의 경우가 발생했을 때 환불 요청하는데 이 과정이 불완전함(모든 PG별로 테스트가 안정적이지않은?)

# Reference
- [Stripe 결제](https://stripe.com/docs/payments)
- [Stripe API](https://stripe.com/docs/api/customers)
- [Paddle API](https://developer.paddle.com/api-reference/1384a288aca7a-api-reference)