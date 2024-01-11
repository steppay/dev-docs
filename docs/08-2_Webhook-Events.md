---
stoplight-id: eo1f40yz545ad
---

# Webhook-Events

스텝페이가 제공하고 있는 웹훅 이벤트 목록입니다. 도메인 별로 구분되며, 각 이벤트 별로 이벤트 타입과 스키마가 결정됩니다. 스키마는 수신받게 될 object 내에 `data` 프로퍼티와 매칭됩니다.

## Events

### 주문

| 이벤트   | 이벤트 타입        | Schema                                                     |
| ----- | ------------- | ---------------------------------------------------------- |
| 주문 생성 | order.created | [Order](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#order) |
| 주문 변경 | order.updated | [Order](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#order) |
| 주문 결제 성공 | order.payment_completed | [Order](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#order) |

### 구독

| 이벤트      | 이벤트 타입                                | Schema                                                                   |
| -------- | ------------------------------------- | ------------------------------------------------------------------------ |
| 구독 생성    | subscription.created                  | [Subscription](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#subscription) |
| 구독 변경    | subscription.updated                  | [Subscription](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#subscription) |
| 결제 예정 알림 | subscription.payment_due_notification | [Subscription](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#subscription) |
| 사용량 추가   | subscription.usage.added              | [Usage](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#usage)               |

### 청구서

| 이벤트    | 이벤트 타입          | Schema                                                         |
| ------ | --------------- | -------------------------------------------------------------- |
| 청구서 생성 | invoice.created | [Invoice](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#invoice) |
| 청구서 변경 | invoice.updated | [Invoice](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#invoice) |
| 청구서 삭제 | invoice.deleted | [Invoice](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#invoice) |

### 결제

| 이벤트   | 이벤트 타입            | Schema                                                         |
| ----- | ----------------- | -------------------------------------------------------------- |
| 결제 성공 | payment.completed | [Payment](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#payment) |
| 결제 실패 | payment.failed    | [Payment](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#payment) |
| 결제 취소 | payment.canceled  | [Payment](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#payment) |
| 결제 대기 | payment.standby   | [Payment](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#payment) |

### 회원

| 이벤트       | 이벤트 타입           | Schema                                                           |
| :--------- | :--------------- | :--------------------------------------------------------------- |
| 회원 생성     | customer.created | [Customer](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#customer) |
| 회원 정보 변경 | customer.updated | [Customer](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#customer) |
| 회원 삭제     | customer.deleted | [Customer](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#customer) |

### 상품

| 이벤트      | 이벤트 타입                | Schema                                                         |
| :------- | :-------------------- | :------------------------------------------------------------- |
| 상품 생성    | product.created       | [Product](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#product) |
| 상품 수정    | product.updated       | [Product](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#product) |
| 상품 삭제    | product.deleted       | [Product](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#product) |
| 가격 플랜 생성 | product.price.created | [Price](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#price)     |
| 가격 플랜 수정 | product.price.updated | [Price](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#price)     |
| 가격 플랜 삭제 | product.price.deleted | [Price](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#price)     |

### 애드온:스텝커버
| 이벤트      | 이벤트 타입                | Schema                                                         |
| :------- | :-------------------- | :------------------------------------------------------------- |
| 커버 알림 발송    | cover.sent_message       | [Product](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#cover) |
| 커버 알림 나중에 받기    | cover.delayed_message       | [Product](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#cover) |
| 커버 결제일 변경    | cover.changed_payment_date       | [Product](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#cover) |
| 커버 만기    | cover.paused       | [Product](https://docs.develop.steppay.kr/docs/guide/oq1uku3n52qax-webhook-schema#cover) |


</br>

