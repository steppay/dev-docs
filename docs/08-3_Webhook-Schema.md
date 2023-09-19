---
stoplight-id: oq1uku3n52qax
---

# Webhook-Schema
['웹훅 v2'](https://docs.develop.steppay.kr/docs/guide/har8c97gh696g-webhook-v2)에서 제공되는 Schema 목록입니다.

웹훅을 통해 보내지는 데이터의 프로퍼티 'data'에는 'Schema'가 포함됩니다. 각각의 이벤트에는 해당 이벤트에 맞는 스키마가 사용됩니다. [Webhook Events](https://docs.develop.steppay.kr/docs/guide/eo1f40yz545ad-webhook-events)에서 각각의 이벤트에 맞는 스키마를 확인하실 수 있습니다. 또한 API 버전에 따라 스키마가 달라질 수 있습니다.

## Schema

### Subscription

| 변수명           | 타입             | 설명                                        | Nullable |
|------------------|------------------|---------------------------------------------|----------|
| subscriptionId   | Long             | 구독 번호                                   | No       |
| status           | SubscriptionStatus | SubscriptionStatus: 구독 상태<br/>- ACTIVE: 활성화<br/>- INCOMPLETE<br/>- UNPAID: 결제 실패<br/>- PENDING_PAUSE: 일시정지 예정<br/>- PAUSE: 일시 정지<br/>- PENDING_CANCEL: 취소 예정<br/>- EXPIRED: 구독 만료<br/>- CANCELED: 구독 취소<br/>- QUEUEING: 갱신 결제를 위해 큐에 집어넣음 | No       |
| createdAt        | LocalDateTime    | 생성 일시                                   | Yes      |
| trialPeriod      | Period           | 무료체험 기간 정보 (하단참조)               | Yes      |
| lastPaymentDate  | LocalDateTime    | 최근 결제 시점                             | Yes      |
| nextPaymentDate  | LocalDateTime    | 다음 결제 시점                             | Yes      |
| originNextPaymentDate | LocalDateTime | 최초 다음 결제 시점                     | Yes      |
| endDate          | LocalDateTime    | 종료일                                      | Yes      |
| pausedDateTime   | LocalDateTime    | 일시정지 시점                              | Yes      |
| orderId          | Long             | 구독 생성한 주문 번호                       | Yes      |
| orderCode        | String           | 구독 생성한 주문 코드                       | Yes      |
| items            | List (SubscriptionItem) | 구독 항목 목 (하단참조)               | Yes      |
| customerId       | Long             | 고객 번호                                   | Yes      |
| intervalUnit     | DateUnitType     | 구독 주기 타입<br/>- DateUnitType: 날짜 단위 타입<br/>- DAY: 일<br/>- WEEK: 주<br/>- MONTH: 개월<br/>- YEAR: 년 | Yes      |
| intervalCount    | Int              | 구독 주기                                   | Yes      |
| paymentMethod    | SubscriptionPaymentMethod | 구독 결제 수단 (하단참조)       | Yes      |
| currentPeriod    | Period           | 현재 주기 정보 (하단참조)                   | Yes      |
| notiBeforePaymentDate | LocalDateTime | 결제 예정 알림 시점                  | Yes      |



- **SubscriptionPaymentMethod**

    **`paymentMethod`** 필드에는 **`SubscriptionPaymentMethod`** 객체 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명           | 타입             | 설명                                        | Nullable |
  |------------------|------------------|---------------------------------------------|----------|
  | paymentGateway  | PaymentGateway   | 사용한 PG<br/>(허용 값)<br/> - DANAL: 다날<br/> - KAKAO: 카카오페이<br/> - KG: KG이니시스<br/> - NICE: 나이스페이<br/> - GOOGLE: 구글플레이<br/> - BANKPAY (deprecated, "뱅크페이"로 변경된 BLUE_WALNUT을 사용하세요.): 뱅크페이<br/> - BLUEWALNUT: 블루월넛<br/> - KSNET: KSNET<br/> - TOSS: 토스<br/> - EXIMBAY: 엑심베이<br/> - SETTLE: 세틀뱅크<br/> - NICE_V2: 나이스페이 v2<br/> - STRIPE: 스트라이프<br/> - PAYPLE: 페이플<br/> - PAYPLE_GLOBAL: 페이플 글로벌<br/> - UNKNOWN: 알 수 없음 | Yes      |
  | paymentInfo      | String           | 결제수단 정보(카드번호 등)                 | Yes      |



- **SubscriptionItem**

    **`items`** 필드에는 **`SubscriptionItem`** 객체의 배열이 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명                   | 타입                    | 설명                                        | Nullable |
  |--------------------------|-------------------------|---------------------------------------------|----------|
  | subscriptionItemId       | Long                    | 구독 항목 번호                               | No       |
  | productName              | String                  | 상품명                                      | No       |
  | featuredImageUrl         | String                  | 이미지 URL                                  | Yes      |
  | selectedProductOptionIds | List (Long)             | 선택한 옵션 번호 목록                        | No       |
  | price                    | Decimal                 | 가격                                        | No       |
  | quantity                 | Int                     | 수량                                        | No       |
  | isAdditional             | Boolean                 | 추가 구매 상품인지 여부                      | No       |
  | keepWhenRenew            | Boolean                 | 갱신될 때 유지되는 항목인지 여부            | No       |
  | maximumPurchaseQuantity  | Int                     | 최대 구매 가능 수량                         | Yes      |
  | productCode              | String                  | 상품 코드                                   | Yes      |
  | priceCode                | String                  | 가격 플랜 코드                              | Yes      |
  | type                     | OrderItemType           | OrderItemType: 항목 유형<br/>- SKU: 재고관리 상품<br/>- TAX: 세금<br/>- SHIPPING: 배송비<br/>- DISCOUNT: 할인<br/>- OFFLINE: POS 연동<br/>- FEE: 기타 요금(도입비, 기본료 등)<br/>- ADDS: 아이템 추가/삭제 시 정산용 추가값 | No       |
  | claimMethodType          | ClaimMethodType         | 선불인지 후불인지 정보<br/>- PRE: 선불<br/>- POST: 후불 | Yes      |
  | priceType                | PriceType               | PriceType: 가격 유형<br/>- ONE_TIME: 단건 상품, 1회성 구매<br/>- FLAT: 구독, 정액제 템플릿<br/>- UNIT_BASED: 건당 과금 템플릿<br/>- USAGE_BASED: 사용량 기반<br/>- BUNDLE: 번들 가격 플랜 | No       |
  | selectedOptions          | List (Long)             | 선택된 옵션 번호                             | No       |


- **Period**

  **trialPeriod** , **currentPeriod** 필드에는 **Period** 객체가 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명           | 타입            | 설명    | Nullable |
  | ------------- | ------------- | ----- | -------- |
  | startDateTime | LocalDateTime | 시작 시점 | No       |
  | endDateTime   | LocalDateTime | 끝 시점  | No       |

***

### Usage

| 변수명             | 타입             | 설명                                      | Nullable |
|--------------------|------------------|-------------------------------------------|----------|
| id                 | Long             | 사용량 번호                               | No       |
| subscriptionItemId | Long             | 구독 항목 번호                           | No       |
| accumulatedQuota   | Long             | 마지막 누적 Quota (후불 일 경우 null)   | Yes      |
| accumulatedRecord  | Long             | 마지막 누적 Record                        | No       |
| recordQuotas       | List (Object)    | 사용량 기록 목록<br/>(하단 참조)         | No       |


- **recordQuotas**

    **`recordQuotas`** 필드에는 객체의 배열이 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명            | 타입           | 설명                               | Nullable |
  |-------------------|----------------|------------------------------------|----------|
  | id                | Long           | 사용량 기록 번호                   | No       |
  | deltaQuota        | Long           | Quota 증감량                       | No       |
  | deltaRecord       | Long           | Record 증감량                      | No       |
  | accumulateQuota   | Long           | 해당 시점의 누적 Quota (후불 일 경우 null) | Yes |
  | accumulateRecord  | Long           | 해당 시점의 누적 Record            | No       |
  | influxDate        | LocalDateTime  | 기록시간                           | No       |
  | via               | Actor          | Actor: 기록 주체<br/>(허용 값)<br/>- V1: API로 기록 시<br/>- MANAGER: 포탈에서 기록 시<br/>- SYSTEM: 최초 구독 생성 및 갱신 결제 시<br/>- CUSTOMER: 구독매니저에서 변경 시 | No |


- **JSON Example**

```json
{
  "id": 1,
  "subscriptionItemId": 1,
  "accumulatedRecord": 1000,
  "recordQuotas": [
    {
      "id": 1,
      "deltaRecord": 0,
      "influxDate": "2023-07-07T01:35:42",
      "accumulateRecord": 0,
      "via": "SYSTEM"
    },
    {
      "id": 2,
      "deltaRecord": 1000,
      "influxDate": "2023-07-07T02:38:47",
      "accumulateRecord": 1000,
      "via": "MANAGER"
    }
  ]
}
```

### Invoice

| 변수명           | 타입                    | 설명                                        | Nullable |
|------------------|-------------------------|---------------------------------------------|----------|
| id               | Long                    | 청구서 번호                                | Yes      |
| status           | InvoiceStatus           | InvoiceStatus: 청구서 상태<br/>(허용 값)<br/>- TEMPORARY: 임시저장<br/>- RESERVATION: 발송 예약<br/>- SENT: 발송<br/>- PAID: 결제 완료<br/>- OVER_DUE: 미납입<br/>- SEND_FAIL: 발송 실패 | Yes      |
| publishType      | InvoicePublishType      | InvoicePublishType: 청구서 발행 유형<br/>(허용 값)<br/>- NOW: 바로<br/>- RESERVATION: 예약 | Yes      |
| purchaseDeadline | LocalDateTime           | 구매 기한                                 | Yes      |
| reservationAt    | LocalDateTime           | 예약 일시                                 | Yes      |
| deletedAt        | LocalDateTime           | 삭제 일시                                 | Yes      |
| publishMethod    | List (InvoicePublishMethod) | InvoicePublishMethod: 발송 수단<br/>(허용 값)<br/>- KAKAO: 알림톡<br/>- SMS: SMS<br/>- EMAIL: 이메일 | Yes |
| discount         | Decimal                | 할인 금액                                 | Yes      |
| memoToCustomer   | String                 | 청구서 메모                               | Yes      |
| orderId          | Long                    | 주문 아이디                                | Yes      |
| orderCode        | String                  | 주문 코드                                 | Yes      |
| customerId       | Long                    | 고객 아이디                                | Yes      |


###  Order

| 변수명             | 타입                    | 설명                                        | Nullable |
|--------------------|-------------------------|---------------------------------------------|----------|
| id                 | Long                    | 주문 번호                                 | No       |
| code               | String                  | 주문 코드                                 | No       |
| type               | OrderType               | OrderType: 주문 유형<br/>(허용 값)<br/>- RECURRING: 갱신 결제<br/>- ONE_TIME: 단건 주문<br/>- PAYMENT_METHOD: 결제수단 변경<br/>- RECURRING_INITIAL: 갱신 결제(최초 주문)<br/>- ADD_USAGE: 사용량 추가 | No |
| paidAmount         | Decimal                | 주문 금액                                 | No       |
| returnedAmount     | Decimal                | 환불된 금액                               | No       |
| leftAmount         | Decimal                | 남은 금액                                 | No       |
| discountedAmount   | Decimal                | 할인 금액                                 | No       |
| productName        | String                  | 상품 이름                                 | No       |
| paymentDate        | LocalDateTime           | 결제 시점                                 | Yes      |
| paymentDueDate     | LocalDateTime           | 결제일 지정                               | Yes      |
| createdAt          | LocalDateTime           | 생성된 시점                               | Yes      |
| modifiedAt         | LocalDateTime           | 수정된 시점                               | Yes      |
| purchaseDeadline   | LocalDateTime           | 결제 기한                                 | Yes      |
| idKey              | String                  | 결제 정보 조회용 idKey                    | Yes      |
| customerId         | Long                    | 주문 고객 번호                             | Yes      |
| shipping           | Shipping                | 주문 배송지 정보<br/>(하단 참조)           | Yes      |
| items              | List (OrderItem)        | 주문 항목들<br/>(하단 참조)                | Yes      |
| subscriptions      | List (Long)             | 관련 구독 목록                            | Yes      |
| invoiceId          | Long                    | 청구서 번호                               | Yes      |


- **Shipping**

    **`shipping`** 필드에는 **`Shipping`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명         | 타입     | 설명       | Nullable |
  | ----------- | ------ | -------- | -------- |
  | name        | String | 수령인 이름   | No       |
  | phone       | String | 수령인 전화번호 | No       |
  | postcode    | String | 우편번호     | No       |
  | address1    | String | 주소       | No       |
  | address2    | String | 세부 주소    | No       |
  | state       | String | 주 정보     | Yes      |
  | city        | String | 도시 정보    | Yes      |
  | countryCode | String | 국가 코드    | Yes      |
- **OrderItem**

    **`items`** 필드에는 **`OrderItem`** 객체의 배열이 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명                  | 타입                 | 설명                                          | Nullable |
  |-------------------------|----------------------|-----------------------------------------------|----------|
  | id                      | Long                 | 주문 항목 번호                                | No       |
  | code                    | String               | 주문 항목 코드                                | No       |
  | type                    | OrderItemType        | OrderItemType: 주문 항목 유형<br/>(허용 값)<br/>- SKU: 재고관리 상품<br/>- TAX: 세금<br/>- SHIPPING: 배송비<br/>- DISCOUNT: 할인<br/>- OFFLINE: POS 연동<br/>- FEE: 기타 요금(도입비, 기본료 등)<br/>- ADDS: 아이템 추가/삭제 시 정산용 추가값 | Yes |
  | status                  | OrderItemStatus      | OrderItemStatus: 주문 항목 상태<br/>(허용 값)<br/>- CREATED: 결제 대기중<br/>- DEPOSIT_WAITING: 입금 대기<br/>- CANCELLED: 취소 완료<br/>- PAID: 결제 완료<br/>- CANCELLATION_REQUEST: 취소 요청<br/>- CANCELLATION_REQUEST_CANCELLED: 취소 요청 취소<br/>- CANCELLATION_REQUEST_DENIED: 취소 요청 거부<br/>- CANCELLATION_REFUNDING: 환불 진행 중<br/>- CANCELLATION_REFUNDED: 전액 환불<br/>- CANCELLATION_REFUNDED_PARTIALLY: 부분 환불<br/>- ORDER_DELIVERY_PREPARING: 배송 준비 중<br/>- ORDER_DELIVERY_SUSPENDED: 배송 준비 중 중지하고 취소로 갈 경우<br/>- ORDER_DELIVERY_ON_THE_WAY: 배송 중<br/>- ORDER_DELIVERY_COMPLETED: 배송 완료<br/>- EXCHANGE_REQUEST: 교환 요청<br/>- EXCHANGE_REQUEST_CANCELLED: 교환 요청 취소<br/>- EXCHANGE_REQUEST_REJECTED: 교환 요청 거부<br/>- EXCHANGE_COLLECTION_PREPARING: 수거 준비중<br/>- EXCHANGE_COLLECTION_ON_THE_WAY: 교환 수거중<br/>- EXCHANGE_COLLECTION_COMPLETED: 교환 수거 완료<br/>- EXCHANGE_DELIVERY_PREPARING: 교환 재배송 준비중<br/>- EXCHANGE_DELIVERY_ON_THE_WAY: 교환 재배송 진행중<br/>- EXCHANGE_DELIVERY_COMPLETED: 교환 재배송 완료<br/>- EXCHANGE_REJECT_DELIVERY_PREPARING: 교환 재배송 준비중<br/>- EXCHANGE_REJECT_DELIVERY_ON_THE_WAY: 교환 재배송 진행중<br/>- EXCHANGE_REJECT_DELIVERY_COMPLETED: 교환 재배송 완료<br/>- EXCHANGE_PENDING: 교환 보류<br/>- EXCHANGE_REJECTED: 교환 거부<br/>- RETURN_REQUEST: 반품 요청<br/>- RETURN_REQUEST_CANCELLED: 반품 요청 취소<br/>- RETURN_REQUEST_REJECTED: 반품 요청 거부<br/>- RETURN_COLLECTION_PREPARING: 수거 준비중<br/>- RETURN_COLLECTION_ON_THE_WAY: 반품 수거중<br/>- RETURN_COLLECTION_COMPLETED: 반품 수거 완료<br/>- RETURN_REJECT_DELIVERY_PREPARING: 반품 재배송 준비중<br/>- RETURN_REJECT_DELIVERY_ON_THE_WAY: 반품 재배송 진행중<br/>- RETURN_REJECT_DELIVERY_COMPLETED: 반품 재배송 완료<br/>- RETURN_PENDING: 반품 보류<br/>- RETURN_REJECTED: 반품 거부<br/>- RETURN_REFUNDING: 환불 진행중<br/>- RETURN_REFUNDED: 환불 완료<br/>- RETURN_REFUNDED_PARTIALLY: 부분 환불<br/>- PAYMENT_FAILURE: 결제 실패<br/>- FINISHED_EXCHANGE_AVAILABLE: 교환/반품 가능 1주일<br/>- FINISHED_RETURN_AVAILABLE: 교환/반품 가능 1개월<br/>- FINISHED_SUCCESSFULLY: 구매 완료 | No |
  | createdAt               | LocalDateTime         | 생성된 시점                                 | Yes      |
  | modifiedAt              | LocalDateTime         | 수정된 시점                                 | Yes      |
  | canceledDateTime        | LocalDateTime         | 취소 시점                                   | Yes      |
  | paidAmount              | Decimal               | 결제 금액                                   | No       |
  | currency                | String                | 통화 코드                                   | No       |
  | quantity                | Int                   | 수량                                        | No       |
  | priceCode               | String                | 가격 플랜 코드                              | Yes      |
  | productCode             | String                | 상품 코드                                   | Yes      |
  | productType             | ProductType           | 주문 시점의 상품 타입<br/>ProductType: 제품 유형<br/>(허용 값)<br/>- BOX: 배송상품<br/>- SOFTWARE: 무형의 상품(서비스 포함)<br/>- BUNDLE: 포함해서 판매하는 상품 (배송이 필요할 수도, 필요하지 않을 수도 있음. 현재 사용되지 않음.)<br/>- INVOICE: 청구서 페이지에서 생성될 때 설정되는 상품 유형<br/>- DRAFT: 초안 | No |
  | productName             | String                | 주문 시점의 상품 이름                         | No       |
  | featuredImageUrl        | String                | 상품 이미지 URL                             | Yes      |
  | selectedProductOptionLabel | String             | 선택한 상품 옵션                             | Yes      |
  | selectedProductOptionIds | List (Long)          | 선택한 옵션 ID 목록                          | No       |
  | planName                | String                | 주문 시점의 가격 플랜 이름                  | No       |
  | discountName            | String                | 할인 타입(주문 항목 타입이 DISCOUNT인 경우) | Yes      |
  | relatedOrderItemId      | Long                  | 연관된 주문 항목 (주문 항목 타입이 DISCOUNT인 경우) | Yes |
  | priceSetupType          | PriceOptionType       | 기본료 주문 항목인 경우 1회 또는 정기적으로 구분하는 타입<br/>PriceOptionType: 가격 옵션 유형<br/>(허용 값)<br/>- INITIALLY: 1회<br/>- PERIODIC: 주기적 | Yes |
  | demoCycle               | DemoCycle             | 무료체험이 적용됐는지 적용 여부 및 기간 (하단 참조) | Yes      |
  | minimumQuantity         | Int                   | 최소 구매 가능 수량                         | Yes      |
  | parentOrderItemCode     | String                | 파생 주문 아이템의 부모(번들) 주문 아이템 코드 | Yes |


- **`demoCycle`** 필드에는 **`demoCycle`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

| 변수명    | 타입            | 설명                                          | Nullable |
|-----------|-----------------|-----------------------------------------------|----------|
| num       | Int             | 수령인 이름                                  | No       |
| type      | DateUnitType    | DateUnitType: 날짜 단위<br/>(허용 값)<br/>- DAY: 일<br/>- WEEK: 주<br/>- MONTH: 개월<br/>- YEAR: 년 | No       |


### Payment

| 변수명           | 타입        | 설명                                       | Nullable |
|------------------|-------------|--------------------------------------------|----------|
| paymentId        | Long        | 스텝페이 결제 번호                        | No       |
| idKey            | String      | 결제 정보 조회용 idKey                    | No       |
| orderId          | String      | 주문 번호 (paymentOnly = true 일때는 가맹점의 주문 번호) | Yes      |
| customerId       | String      | 주문 번호 (paymentOnly = true 일때는 가맹점의 고객 번호) | Yes      |
| productName      | String      | 결제 상품 명                              | Yes      |
| paidAmount       | Decimal     | 결제 금액                                 | Yes      |
| paidAt           | LocalDateTime | 결제 일시                               | Yes      |
| status           | String      | 결제 상태<br/>(허용 값)<br/>- STANDBY: 대기중<br/>- COMPLETE: 완료<br/>- CANCELED: 취소됨<br/>- PARTIAL_CANCELED: 부분 취소됨<br/>- USER_CANCELED: 사용자에 의해 취소됨<br/>- CANCELED_FAIL: 취소 실패<br/>- FAILED: 실패<br/>- VIRTUAL_BANK_STANDBY: 가상계좌 대기중<br/>- CMS_STANDBY: CMS 대기중 | No       |
| paymentGateway   | String      | 결제 PG<br/>(허용 값)<br/>- DANAL: 다날<br/>- KAKAO: 카카오페이<br/>- KG: KG이니시스<br/>- NICE: 나이스페이<br/>- GOOGLE: 구글플레이<br/>- BANKPAY (deprecated, "뱅크페이"로 변경된 BLUE_WALNUT을 사용하세요.): 뱅크페이<br/>- BLUEWALNUT: 블루월넛<br/>- KSNET: KSNET<br/>- TOSS: 토스<br/>- EXIMBAY: 엑심베이<br/>- SETTLE: 세틀뱅크<br/>- NICE_V2: 나이스페이 v2<br/>- STRIPE: 스트라이프<br/>- PAYPLE: 페이플<br/>- PAYPLE_GLOBAL: 페이플 글로벌<br/>- UNKNOWN: 알 수 없음 | No       |
| paymentMethod    | String      | 결제 수단<br/>(허용 값)<br/>- CARD: 신용카드<br/>- VBANK: 가상계좌<br/>- BANK: 계좌이체<br/>- CELLPHONE: 휴대폰 결제<br/>- SIMPLE_PAY: 간편결제<br/>- CMS: 통장결제<br/>- CARD_BILL: 신용카드 빌링<br/>- CELLPHONE_BILL: 휴대폰 결제 빌링<br/>- CMS_BILL: 통장결제 빌링 | No       |
| paymentOnly      | Boolean     |                                            | Yes      |
| errorMessage     | String      | 에러 발생 시, 에러 메시지                  | Yes      |
| cancel           | Cancel      | (하단 참조)                               | Yes      |
| vBank            | VBank       | (하단 참조)                               | Yes      |
| niceCms          | NiceCms     | (하단 참조)                               | Yes      |


- **VBank**

  | 변수명           | 타입            | 설명    | Nullable |
  | ------------- | ------------- | ----- | -------- |
  | bankCode      | String        | 은행 코드 | Yes      |
  | bankName      | String        | 은행 명  | No       |
  | accountNumber | String        |       | No       |
  | accountName   | String        |       | No       |
  | bankDate      | LocalDateTime |       | No       |
- **NiceCms**

| 변수명                            | 타입            | 설명                                        | Nullable |
|-----------------------------------|-----------------|---------------------------------------------|----------|
| corporateManager                 | String          | 법인 명                                     | No       |
| companyName                      | String          | 회사 명                                     | No       |
| companyRegistrationNumber        | String          | 신청인 정보<br/>법인일 시, 사업자번호<br/>개인일 시, 생년월일 | Yes      |
| accountHolderSocialSecurityNumber | String          | 법인일 시, 사업자번호<br/>개인일 시, 생년월일 | No       |
| bankCode                         | String          | 은행 코드<br/>(허용 값)<br/>- KDB: 한국산업은행<br/>- IBK: 기업은행<br/>- KB: 국민은행<br/>- KEB: 하나은행 (구외환)<br/>- SH: 수협중앙회<br/>- NH: 농협중앙회<br/>- WOORI: 우리은행<br/>- SC: 제일은행<br/>- HANMI: 한국씨티은행 (한미은행)<br/>- DGB: 대구은행<br/>- BNK_BS: 부산은행<br/>- KJB: 광주은행<br/>- JEJU: 제주은행<br/>- JB: 전북은행<br/>- BNK_KN: 경남은행<br/>- MG: 새마을금고<br/>- CREDIT_UNION: 신용협동조합중앙회<br/>- POST: 우체국<br/>- HANA: 하나은행<br/>- SHINHAN_UNIFIED: 신한은행(조흥 통합)<br/>- KBANK: 케이뱅크<br/>- KAKAO_BANK: 카카오뱅크<br/>- TOSS_BANK: 토스뱅크 | No       |
| bankAccount                      | String          | 계좌 번호                                   | No       |
| date                             | LocalDateTime   | 'status' 가 발생한 일시                     | No       |
| status                           | String          | 계좌 상태<br/>(허용 값)<br/>- ACCOUNT_PENDING: 계좌 등록 진행중<br/>- ACCOUNT_FAIL: 계좌 등록 실패<br/>- ACCOUNT_SUCCESS: 계좌 등록 성공 (계좌 등록 성공 후 출금 진행중이 아닐때만 표시됨)<br/>- WITHDRAW_PENDING: 출금 진행중<br/>- WITHDRAW_FAIL: 출금 실패<br/>- WITHDRAW_SUCCESS: 출금 성공 | No       |
| errorReturn                      | String          |                                            | Yes      |


- **Cancel**

  | 변수명              | 타입            | 설명       | Nullable |
  | :--------------- | :------------ | :------- | :------- |
  | canceledAmount   | Decimal       | 취소 금액    | No       |
  | lastCanceledDate | LocalDateTime | 최종 취소 일시 | Yes      |

***

### Customer

| 변수명                  | 타입                   | 설명                        | Nullable |
|-------------------------|------------------------|-----------------------------|----------|
| id                      | Long                   | 고객 번호                   | No       |
| username                | String                 | 고객 아이디                 | Yes      |
| name                    | String                 | 고객 이름                   | Yes      |
| email                   | String                 | 고객 이메일                 | Yes      |
| phone                   | String                 | 고객 전화번호               | Yes      |
| shipping                | Shipping               | 고객 기본 배송 정보<br/>(하단 참조) | Yes      |
| code                    | String                 | 고객 코드                   | Yes      |
| attributes              | Map (String, String)   | 고객 추가 데이터            | Yes      |
| createdAt               | LocalDateTime          | 고객 생성 시점             | Yes      |
| additionalRecipients    | List (String)          | 추가 수신 이메일            | Yes      |


- **Shipping**

    **`shipping`** 필드에는 **`Shipping`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명         | 타입     | 설명       | Nullable |
  | ----------- | ------ | -------- | -------- |
  | name        | String | 수령인 이름   | No       |
  | phone       | String | 수령인 전화번호 | No       |
  | postcode    | String | 우편번호     | No       |
  | address1    | String | 주소       | No       |
  | address2    | String | 세부 주소    | No       |
  | state       | String | 주 정보     | Yes      |
  | city        | String | 도시 정보    | Yes      |
  | countryCode | String | 국가 코드    | Yes      |

***

### Product

| 변수명       | 타입               | 설명                           | Nullable |
|--------------|-------------------|------------------------------|----------|
| code         | String            | 상품 코드                      | No       |
| type         | ProductType       | ProductType: 상품 타입  <br/><허용 값>  <br/>  <br/>BOX: 배송상품  <br/>SOFTWARE: 무형의 상품(서비스 포함)  <br/>BUNDLE 포함해서 판매하는 상품 (배송이 필요할 수도, 필요하지 않을 수도 있음. 현재 사용되지 않음.)  <br/>INVOICE: 청구서 페이지에서 생성될 때 설정되는 상품 유형  <br/>DRAFT: 초안                      | Yes      |
| status       | ProductStatus     | ProductStatus: 상품 상태  <br/><허용 값>  <br/>  <br/>SALE: 판매 중  <br/>OUT_OF_STOCK: 재고 없음  <br/>UNSOLD: 판매되지 않음  <br/>WAITING_APPROVAL: 승인 대기 중  <br/>REJECTED: 거부됨 | Yes      |
| name         | String            | 상품 이름                      | Yes      |
| subTitle     | String            | 부제목                          | Yes      |
| featuredImageUrl | String      | 상품 대표 이미지 URL       | Yes      |
| imageUrls    | List (String)     | 상품 이미지 URL                | Yes      |
| description  | String            | 상품 설명                      | Yes      |
| quantity     | Int               | 재고 수량                      | Yes      |
| optionGroups | List (ProductOptionGroup) | 옵션 그룹 목록 <br/>(하단 참조) | Yes      |
| prices       | List (PriceSchema)| 가격 플랜 목록  <br/>(하단 참조)             | Yes      |
| categories   | List (ProductCategory) | 카테고리 목록  <br/>(하단 참조)  | Yes      |
| createdAt    | LocalDateTime     | 생성 시점                      | Yes      |
| modifiedAt   | LocalDateTime     | 수정 시점                      | Yes      |
| enabledDemo  | Boolean           | 무료 체험 활성화 여부   | Yes      |
| demoPeriod   | Int               | 무료 체험 기간               | Yes      |
| demoPeriodUnit | DateUnitType    | 무료 체험 기간 단위     | Yes      |


- **ProductCategory**

    **`categories`** 필드에는 **`ProductCategory`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명        | 타입     | 설명      | Nullable |
  | ---------- | ------ | ------- | :------- |
  | categoryId | Long   | 카테고리 번호 | No       |
  | name       | String | 카테고리 이름 | No       |
- **ProductOptionGroup**

    **`optionGroups`** 필드에는 **`ProductOptionGroup`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명     | 타입                   | 설명       | Nullable |
  | ------- | -------------------- | -------- | :------- |
  | id      | Long                 | 옵션 그룹 번호 | No       |
  | name    | String               | 옵션 그룹 이름 | No       |
  | options | List (ProductOption) | 옵션 리스트   | No       |

  - **ProductOption**

      **`options`** 필드에는 **`ProductOption`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

    | 변수명      | 타입      | 설명    | Nullable |
    | -------- | ------- | ----- | -------- |
    | id       | Long    | 옵션 번호 | No       |
    | name     | String  | 옵션 이름 | No       |
    | quantity | Int     | 수량    | Yes      |
    | price    | Decimal | 가격    | No       |

***

### Price

| Field Name                  | Type                    | Description                                                    | Nullable |
|-----------------------------|-------------------------|----------------------------------------------------------------|----------|
| priceCode                   | String                  | 가격 코드                                                      | No       |
| price                       | Decimal                 | 가격 금액                                                      | No       |
| unit                        | String                  | 단위                                                            | Yes      |
| type                        | PriceType               | PriceType: 가격 유형 <br/> <허용 값>  <br/>  ONE_TIME: 단건 상품  <br/>  FLAT: 구독, 정액제 템플릿  <br/>  UNIT_BASED: 건당 과금 템플릿  <br/>  USAGE_BASED: 사용량 기반  <br/>  BUNDLE: 번들 플랜 | Yes      |
| membershipExpirationDate    | Int                     | 구독 만기 기간                                                 | No       |
| membershipExpirationDateType| DateUnitType            | 구독 만기 기간 단위                                            | Yes      |
| setupOption                 | SetupOption             | 기본료 정보  <br/> (하단 참조)                                      | Yes      |
| options                     | List (PriceOption)      | 옵션 정보  <br/> (하단 참조)                                        | No       |
| additionalBilling           | PriceAdditionalBilling  | 추가 과금 정보  <br/> (하단 참조)                                    | Yes      |
| recurring                   | Interval                | 구독 주기 단위  <br/> (하단 참조)                                    | Yes      |
| createdAt                   | LocalDateTime           | 생성된 시점                                                    | Yes      |
| modifiedAt                  | LocalDateTime           | 수정된 시점                                                    | Yes      |
| plan                        | Plan                    | 플랜 정보  <br/> (하단 참조)                                        | Yes      |
| firstSaleEnabled            | Boolean                 | 첫 구매 할인 적용 여부                                         | Yes      |
| firstSalePrice              | Long                    | 첫 구매 할인 금액                                              | Yes      |
| claim                       | Claim                   | 청구 방식 정보  <br/> (하단 참조)                                    | Yes      |
| basicServing                | Int                     | 기본 제공량 - 계정/사용량 기반 요금 사용시                    | No       |
| bundlePrices                | List (PriceBundle)      | 번들 플랜 - 번들 상품 구성  <br/> (하단 참조)                      | No       |
| onetimeBundlePrice          | Decimal                 | 번들 플랜 - 단건 상품 금액                                    | No       |


- **SetupOption**

    **`setupOption`** 필드에는 **`SetupOption`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  |Field Name|Type|Description|Nullable|
  |----------|----|-----------|--------|
  |id|Long|기본료 번호|No|
  |name|String|기본료 이름|Yes|
  |type|PriceOptionType|기본료 타입  <br/>  <br/>- INITIALLY: 최초 1회  <br/>- PERIODIC: 정기적|Yes|
  |price|Long|기본료 금액|No|
  |claimMethodType|ClaimMethodType|선불/후불  <br/>  <br/>- PRE: 선불  <br/>- POST: 후불|No|


- **PriceAdditionalBilling**

    **`additionalBilling`** 필드에는 **`PriceAdditionalBilling`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  |Field Name|Type|Description|Nullable|
  |----------|----|-----------|--------|
  |id|Long|추가 과금 번호|No|
  |type|AdditionalBillingType|AdditionalBillingType: 추가 과금 유형  <br/>\<허용 값>  <br/>  <br/>USAGE_BASED_WITH_RANGE: 구간별 건당 과금  <br/>USAGE_BASED_WITH_RANGE_AND_FIXED_PRICE: 구간별 고정 금액|No|
  |ranges|List (PriceAdditionalBillingRange)|추가 과금 범위 정보  <br/>(하단참조)|No|


- **PriceAdditionalBillingRange**

  **`ranges`** 필드에는 **`PriceAdditionalBillingRange`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | Field Name | Type    | Description | Nullable |
  | ---------- | ------- | ----------- | -------- |
  | id         | Long    | 추가 과금 범위 번호 | Yes      |
  | until      | Long    | 범위가 어디까지인지  | Yes      |
  | price      | Decimal | 범위에 적용되는 금액 | Yes      |

- **Interval**

    **`recurring`** 필드에는 **`Interval`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  |Field Name|Type|Description|Nullable|
  |----------|----|-----------|--------|
  |unit|DateUnitType|주기 단위  <br/>DateUnitType: 날짜 단위 타입  <br/>\<허용 값>  <br/>  <br/>- DAY: 일  <br/>- WEEK: 주  <br/>- MONTH: 개월  <br/>- YEAR: 년|Yes|
  |count|Int|주기|Yes|


- **Plan**

    **`plan`** 필드에는 **`Plan`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | Field Name        | Type    | Description | Nullable |
  | ----------------- | ------- | ----------- | -------- |
  | name              | String  | 플랜 이름       | No       |
  | description       | String  | 플랜 설명       | No       |
  | detailDescription | String  | 자세히 보기      | Yes      |
  | isHiddenFromShop  | Boolean | 플랜 사용 여부    | No       |
  | adminName         | String  | 어드민 플랜 이름   | Yes      |

- **Claim**

    **`claim`** 필드에는 **`Claim`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  |Field Name|Type|Description|Nullable|
  |----------|----|-----------|--------|
  |methodType|ClaimMethodType|선불/후불|No|
  |whenToClaimType|WhenToClaimType|후불인 경우, 청구 시점  <br/>  <br/>- FIRST_PAYMENT: 최초 결제일 기준 반복  <br/>- DATE: 결제일 지정|No|
  |billingDate|Int|청구 시점 내 날짜 (익월 n일)|No|
  |provideStartDay|Int|서비스 제공 시작일|Yes|


- **PriceBundle**

    **`bundlePrices`** 필드에는 **`PriceBundle`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | Field Name  | Type   | Description | Nullable |
  | ----------- | ------ | ----------- | -------- |
  | productCode | String | 상품 코드       | Yes      |
  | priceCode   | String | 플랜 코드       | Yes      |