---
stoplight-id: mkl28d9swmo2s
---

# Webhook-Schema

웹훅을 통해 보내지는 데이터의 프로퍼티 'data'에는 'Schema'가 포함됩니다. 각각의 이벤트에는 해당 이벤트에 맞는 스키마가 사용됩니다. [Webhook Events](https://docs.steppay.kr/docs/webhook-events)에서 각각의 이벤트에 맞는 스키마를 확인하실 수 있습니다. 또한 API 버전에 따라 스키마가 달라질 수 있습니다.

## Schema

> api version: v1

### Subscription

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "subscriptionId",
    "0-1": "Long",
    "0-2": "구독 번호",
    "0-3": "No",
    "1-0": "status",
    "1-1": "SubscriptionStatus",
    "1-2": "SubscriptionStatus: 구독 상태  \n\\<허용 값>  \n  \nACTIVE: 활성화  \nINCOMPLETE  \nUNPAID: 결제 실패  \nPENDING_PAUSE: 일시정지 예정  \nPAUSE: 일시 정지  \nPENDING_CANCEL: 취소 예정  \nEXPIRED: 구독 만료  \nCANCELED: 구독 취소  \nQUEUEING: 갱신 결제를 위해 큐에 집어넣음",
    "1-3": "No",
    "2-0": "createdAt",
    "2-1": "LocalDateTime",
    "2-2": "생성 일시",
    "2-3": "Yes",
    "3-0": "trialPeriod",
    "3-1": "Period",
    "3-2": "무료체험 기간 정보  \n(하단참조)",
    "3-3": "Yes",
    "4-0": "lastPaymentDate",
    "4-1": "LocalDateTime",
    "4-2": "최근 결제 시점",
    "4-3": "Yes",
    "5-0": "nextPaymentDate",
    "5-1": "LocalDateTime",
    "5-2": "다음 결제 시점",
    "5-3": "Yes",
    "6-0": "originNextPaymentDate",
    "6-1": "LocalDateTime",
    "6-2": "최초 다음 결제 시점",
    "6-3": "Yes",
    "7-0": "endDate",
    "7-1": "LocalDateTime",
    "7-2": "종료일",
    "7-3": "Yes",
    "8-0": "pausedDateTime",
    "8-1": "LocalDateTime",
    "8-2": "일시정지 시점",
    "8-3": "Yes",
    "9-0": "orderId",
    "9-1": "Long",
    "9-2": "구독 생성한 주문 번호",
    "9-3": "Yes",
    "10-0": "orderCode",
    "10-1": "String",
    "10-2": "구독 생성한 주문 코드",
    "10-3": "Yes",
    "11-0": "items",
    "11-1": "List (SubscriptionItem)",
    "11-2": "구독 항목 목  \n(하단참조)",
    "11-3": "Yes",
    "12-0": "customerId",
    "12-1": "Long",
    "12-2": "고객 번호",
    "12-3": "Yes",
    "13-0": "intervalUnit",
    "13-1": "DateUnitType",
    "13-2": "구독 주기 타입  \n  \nDateUnitType: 날짜 단위 타입  \n\\<허용 값>  \n  \n- DAY: 일  \n- WEEK: 주  \n- MONTH: 개월  \n- YEAR: 년",
    "13-3": "Yes",
    "14-0": "intervalCount",
    "14-1": "Int",
    "14-2": "구독 주기",
    "14-3": "Yes",
    "15-0": "paymentMethod",
    "15-1": "SubscriptionPaymentMethod",
    "15-2": "구독 결제 수단  \n(하단참조)",
    "15-3": "Yes",
    "16-0": "currentPeriod",
    "16-1": "Period",
    "16-2": "현재 주기 정보  \n(하단참조)",
    "16-3": "Yes",
    "17-0": "notiBeforePaymentDate",
    "17-1": "LocalDateTime",
    "17-2": "결제 예정 알림 시점",
    "17-3": "Yes"
  },
  "cols": 4,
  "rows": 18,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **SubscriptionPaymentMethod**

    **`paymentMethod`** 필드에는 **`SubscriptionPaymentMethod`** 객체 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "paymentGateway",
    "0-1": "PaymentGateway",
    "0-2": "사용한 PG  \n  \n\\<허용 값>  \n  \nDANAL: 다날  \nKAKAO: 카카오페이  \nKG: KG이니시스  \nNICE: 나이스페이  \nGOOGLE: 구글플레이  \nBANKPAY (deprecated, \"뱅크페이\"로 변경된 BLUE_WALNUT을 사용하세요.): 뱅크페이  \nBLUEWALNUT: 블루월넛  \nKSNET: KSNET  \nTOSS: 토스  \nEXIMBAY: 엑심베이  \nSETTLE: 세틀뱅크  \nNICE_V2: 나이스페이 v2  \nSTRIPE: 스트라이프  \nPAYPLE: 페이플  \nPAYPLE_GLOBAL: 페이플 글로벌  \nUNKNOWN: 알 수 없음",
    "0-3": "Yes",
    "1-0": "paymentInfo",
    "1-1": "String",
    "1-2": "결제수단 정보(카드번호 등)",
    "1-3": "Yes"
  },
  "cols": 4,
  "rows": 2,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **SubscriptionItem**

    **`items`** 필드에는 **`SubscriptionItem`** 객체의 배열이 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "subscriptionItemId",
    "0-1": "Long",
    "0-2": "구독 항목 번호",
    "0-3": "No",
    "1-0": "productName",
    "1-1": "String",
    "1-2": "상품명",
    "1-3": "No",
    "2-0": "featuredImageUrl",
    "2-1": "String",
    "2-2": "이미지 URL",
    "2-3": "Yes",
    "3-0": "selectedProductOptionIds",
    "3-1": "List (Long)",
    "3-2": "선택한 옵션 번호 목록",
    "3-3": "No",
    "4-0": "price",
    "4-1": "Decimal",
    "4-2": "가격",
    "4-3": "No",
    "5-0": "quantity",
    "5-1": "Int",
    "5-2": "수량",
    "5-3": "No",
    "6-0": "isAdditional",
    "6-1": "Boolean",
    "6-2": "추가 구매 상품인지 여부",
    "6-3": "No",
    "7-0": "keepWhenRenew",
    "7-1": "Boolean",
    "7-2": "갱신될 때 유지되는 항목인지 여부",
    "7-3": "No",
    "8-0": "maximumPurchaseQuantity",
    "8-1": "Int",
    "8-2": "최대 구매 가능 수량",
    "8-3": "Yes",
    "9-0": "productCode",
    "9-1": "String",
    "9-2": "상품 코드",
    "9-3": "Yes",
    "10-0": "priceCode",
    "10-1": "String",
    "10-2": "가격 플랜 코드",
    "10-3": "Yes",
    "11-0": "type",
    "11-1": "OrderItemType",
    "11-2": "OrderItemType: 항목 유형  \n\\<허용 값>  \n  \nSKU: 재고관리 상품  \nTAX: 세금  \nSHIPPING: 배송비  \nDISCOUNT: 할인  \nOFFLINE: POS 연동  \nFEE: 기타 요금(도입비, 기본료 등)  \nADDS: 아이템 추가/삭제 시 정산용 추가값",
    "11-3": "No",
    "12-0": "claimMethodType",
    "12-1": "ClaimMethodType",
    "12-2": "선불인지 후불인지 정보  \n\\<허용값>  \n  \n- PRE: 선불  \n- POST: 후불",
    "12-3": "Yes",
    "13-0": "priceType",
    "13-1": "PriceType",
    "13-2": "### PriceType: 가격 유형  \n  \n- **ONE_TIME**: 단건 상품, 1회성 구매  \n- **FLAT**: 구독, 정액제 템플릿  \n- **UNIT_BASED**: 건당 과금 템플릿  \n- **USAGE_BASED**: 사용량 기반  \n- **BUNDLE**: 번들 가격 플랜",
    "13-3": "No",
    "14-0": "selectedOptions",
    "14-1": "List (Long)",
    "14-2": "선택된 옵션 번호",
    "14-3": "No"
  },
  "cols": 4,
  "rows": 15,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **Period**

  **trialPeriod** , **currentPeriod** 필드에는 **Period** 객체가 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

  | 변수명           | 타입            | 설명    | Nullable |
  | ------------- | ------------- | ----- | -------- |
  | startDateTime | LocalDateTime | 시작 시점 | No       |
  | endDateTime   | LocalDateTime | 끝 시점  | No       |

***

### Usage

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "사용량 번호",
    "0-3": "No",
    "1-0": "subscriptionItemId",
    "1-1": "Long",
    "1-2": "구독 항목 번호",
    "1-3": "No",
    "2-0": "accumulatedQuota",
    "2-1": "Long",
    "2-2": "마지막 누적 Quota (후불 일 경우 null)",
    "2-3": "Yes",
    "3-0": "accumulatedRecord",
    "3-1": "Long",
    "3-2": "마지막 누적 Record",
    "3-3": "No",
    "4-0": "recordQuotas",
    "4-1": "List (Object)",
    "4-2": "사용량 기록 목록  \n(하단 참조)",
    "4-3": "No"
  },
  "cols": 4,
  "rows": 5,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **recordQuotas**

    **`recordQuotas`** 필드에는 e객체의 배열이 포함되어 있습니다. 이 객체의 구조는 다음과 같습니다.

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "사용량 기록 번호",
    "0-3": "No",
    "1-0": "deltaQuota",
    "1-1": "Long",
    "1-2": "Quota 증감량",
    "1-3": "No",
    "2-0": "deltaRecord",
    "2-1": "Long",
    "2-2": "Record 증감량",
    "2-3": "No",
    "3-0": "accumulateQuota",
    "3-1": "Long",
    "3-2": "해당 시점의 누적 Quota (후불 일 경우 null)",
    "3-3": "Yes",
    "4-0": "accumulateRecord",
    "4-1": "Long",
    "4-2": "해당 시점의 누적 Record",
    "4-3": "No",
    "5-0": "influxDate",
    "5-1": "LocalDateTime",
    "5-2": "기록시간",
    "5-3": "No",
    "6-0": "via",
    "6-1": "Actor",
    "6-2": "Actor: 기록 주체  \n(허용 값)  \n  - V1: API로 기록 시  \n  - MANAGER: 포탈에서 기록 시  \n  - SYSTEM: 최초 구독 생성 및 갱신 결제 시  \n  - CUSTOMER: 구독매니저에서 변경 시",
    "6-3": "No"
  },
  "cols": 4,
  "rows": 7,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

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

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "청구서 번호",
    "0-3": "Yes",
    "1-0": "status",
    "1-1": "InvoiceStatus",
    "1-2": "InvoiceStatus: 청구서 상태  \n  \n\\<허용 값>  \n  \nTEMPORARY: 임시저장  \nRESERVATION: 발송 예약  \nSENT: 발송  \nPAID: 결제 완료  \nOVER_DUE: 미납입  \nSEND_FAIL: 발송 실패",
    "1-3": "Yes",
    "2-0": "publishType",
    "2-1": "InvoicePublishType",
    "2-2": "InvoicePublishType: 청구서 발행 유형  \n\\<허용 값>  \n  \nNOW: 바로  \nRESERVATION: 예약",
    "2-3": "Yes",
    "3-0": "purchaseDeadline",
    "3-1": "LocalDateTime",
    "3-2": "구매 기한",
    "3-3": "Yes",
    "4-0": "reservationAt",
    "4-1": "LocalDateTime",
    "4-2": "예약 일시",
    "4-3": "Yes",
    "5-0": "deletedAt",
    "5-1": "LocalDateTime",
    "5-2": "삭제 일시",
    "5-3": "Yes",
    "6-0": "publishMethod",
    "6-1": "List (InvoicePublishMethod)",
    "6-2": "InvoicePublishMethod: 발송 수단  \n\\<허용 값>  \n  \n- KAKAO: 알림톡  \n- SMS: SMS  \n- EMAIL: 이메일",
    "6-3": "Yes",
    "7-0": "discount",
    "7-1": "Decimal",
    "7-2": "할인 금액",
    "7-3": "Yes",
    "8-0": "memoToCustomer",
    "8-1": "String",
    "8-2": "청구서 메모",
    "8-3": "Yes",
    "9-0": "orderId",
    "9-1": "Long",
    "9-2": "주문 아이디",
    "9-3": "Yes",
    "10-0": "orderCode",
    "10-1": "String",
    "10-2": "주문 코드",
    "10-3": "Yes",
    "11-0": "customerId",
    "11-1": "Long",
    "11-2": "고객 아이디",
    "11-3": "Yes"
  },
  "cols": 4,
  "rows": 12,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

###  Order

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "주문 번호",
    "0-3": "No",
    "1-0": "code",
    "1-1": "String",
    "1-2": "주문 코드",
    "1-3": "No",
    "2-0": "type",
    "2-1": "OrderType",
    "2-2": "OrderType: 주문 유형  \n\\<허용 값>  \n  \nRECURRING: 갱신 결제  \nONE_TIME: 단건 주문  \nPAYMENT_METHOD: 결제수단 변경  \nRECURRING_INITIAL: 갱신 결제(최초 주문)  \nADD_USAGE: 사용량 추가",
    "2-3": "No",
    "3-0": "paidAmount",
    "3-1": "Decimal",
    "3-2": "주문 금액",
    "3-3": "No",
    "4-0": "returnedAmount",
    "4-1": "Decimal",
    "4-2": "환불된 금액",
    "4-3": "No",
    "5-0": "leftAmount",
    "5-1": "Decimal",
    "5-2": "남은 금액",
    "5-3": "No",
    "6-0": "discountedAmount",
    "6-1": "Decimal",
    "6-2": "할인 금액",
    "6-3": "No",
    "7-0": "productName",
    "7-1": "String",
    "7-2": "상품 이름",
    "7-3": "No",
    "8-0": "paymentDate",
    "8-1": "LocalDateTime",
    "8-2": "결제 시점",
    "8-3": "Yes",
    "9-0": "paymentDueDate",
    "9-1": "LocalDateTime",
    "9-2": "결제일 지정",
    "9-3": "Yes",
    "10-0": "createdAt",
    "10-1": "LocalDateTime",
    "10-2": "생성된 시점",
    "10-3": "Yes",
    "11-0": "modifiedAt",
    "11-1": "LocalDateTime",
    "11-2": "수정된 시점",
    "11-3": "Yes",
    "12-0": "purchaseDeadline",
    "12-1": "LocalDateTime",
    "12-2": "결제 기한",
    "12-3": "Yes",
    "13-0": "idKey",
    "13-1": "String",
    "13-2": "결제 정보 조회용 idKey",
    "13-3": "Yes",
    "14-0": "customerId",
    "14-1": "Long",
    "14-2": "주문 고객 번호",
    "14-3": "Yes",
    "15-0": "shipping",
    "15-1": "Shipping",
    "15-2": "주문 배송지 정보  \n(하단 참조)",
    "15-3": "Yes",
    "16-0": "items",
    "16-1": "List (OrderItem)",
    "16-2": "주문 항목들  \n(하단 참조)",
    "16-3": "Yes",
    "17-0": "subscriptions",
    "17-1": "List (Long)",
    "17-2": "관련 구독 목록",
    "17-3": "Yes",
    "18-0": "invoiceId",
    "18-1": "Long",
    "18-2": "청구서 번호",
    "18-3": "Yes"
  },
  "cols": 4,
  "rows": 19,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

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

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "주문 항목 번호",
    "0-3": "No",
    "1-0": "code",
    "1-1": "String",
    "1-2": "주문 항목 코드",
    "1-3": "No",
    "2-0": "type",
    "2-1": "OrderItemType",
    "2-2": "OrderItemType: 주문 항목 유형  \n\\<허용 값>  \n  \nSKU: 재고관리 상품  \nTAX: 세금  \nSHIPPING: 배송비  \nDISCOUNT: 할인  \nOFFLINE: POS 연동  \nFEE: 기타 요금(도입비, 기본료 등)  \nADDS: 아이템 추가/삭제 시 정산용 추가값",
    "2-3": "Yes",
    "3-0": "status",
    "3-1": "OrderItemStatus",
    "3-2": "OrderItemStatus: 주문 항목 상태  \n\\<허용 값>  \n  \nCREATED: 결제 대기중  \nDEPOSIT_WAITING: 입금 대기  \nCANCELLED: 취소 완료  \nPAID: 결제 완료  \nCANCELLATION_REQUEST: 취소 요청  \nCANCELLATION_REQUEST_CANCELLED: 취소 요청 취소  \nCANCELLATION_REQUEST_DENIED: 취소 요청 거부  \nCANCELLATION_REFUNDING: 환불 진행 중  \nCANCELLATION_REFUNDED: 전액 환불  \nCANCELLATION_REFUNDED_PARTIALLY: 부분 환불  \nORDER_DELIVERY_PREPARING: 배송 준비 중  \nORDER_DELIVERY_SUSPENDED: 배송 준비 중 중지하고 취소로 갈 경우  \nORDER_DELIVERY_ON_THE_WAY: 배송 중  \nORDER_DELIVERY_COMPLETED: 배송 완료  \nEXCHANGE_REQUEST: 교환 요청  \nEXCHANGE_REQUEST_CANCELLED: 교환 요청 취소  \nEXCHANGE_REQUEST_REJECTED: 교환 요청 거부  \nEXCHANGE_COLLECTION_PREPARING: 수거 준비중  \nEXCHANGE_COLLECTION_ON_THE_WAY: 교환 수거중  \nEXCHANGE_COLLECTION_COMPLETED: 교환 수거 완료  \nEXCHANGE_DELIVERY_PREPARING: 교환 재배송 준비중  \nEXCHANGE_DELIVERY_ON_THE_WAY: 교환 재배송 진행중  \nEXCHANGE_DELIVERY_COMPLETED: 교환 재배송 완료  \nEXCHANGE_REJECT_DELIVERY_PREPARING: 교환 재배송 준비중  \nEXCHANGE_REJECT_DELIVERY_ON_THE_WAY: 교환 재배송 진행중  \nEXCHANGE_REJECT_DELIVERY_COMPLETED: 교환 재배송 완료  \nEXCHANGE_PENDING: 교환 보류  \nEXCHANGE_REJECTED: 교환 거부  \nRETURN_REQUEST: 반품 요청  \nRETURN_REQUEST_CANCELLED: 반품 요청 취소  \nRETURN_REQUEST_REJECTED: 반품 요청 거부  \nRETURN_COLLECTION_PREPARING: 수거 준비중  \nRETURN_COLLECTION_ON_THE_WAY: 반품 수거중  \nRETURN_COLLECTION_COMPLETED: 반품 수거 완료  \nRETURN_REJECT_DELIVERY_PREPARING: 반품 재배송 준비중  \nRETURN_REJECT_DELIVERY_ON_THE_WAY: 반품 재배송 진행중  \nRETURN_REJECT_DELIVERY_COMPLETED: 반품 재배송 완료  \nRETURN_PENDING: 반품 보류  \nRETURN_REJECTED: 반품 거부  \nRETURN_REFUNDING: 환불 진행중  \nRETURN_REFUNDED: 환불 완료  \nRETURN_REFUNDED_PARTIALLY: 부분 환불  \nPAYMENT_FAILURE: 결제 실패  \nFINISHED_EXCHANGE_AVAILABLE: 교환/반품 가능 1주일  \nFINISHED_RETURN_AVAILABLE: 교환/반품 가능 1개월  \nFINISHED_SUCCESSFULLY: 구매 완료",
    "3-3": "No",
    "4-0": "createdAt",
    "4-1": "LocalDateTime",
    "4-2": "생성된 시점",
    "4-3": "Yes",
    "5-0": "modifiedAt",
    "5-1": "LocalDateTime",
    "5-2": "수정된 시점",
    "5-3": "Yes",
    "6-0": "canceledDateTime",
    "6-1": "LocalDateTime",
    "6-2": "취소 시점",
    "6-3": "Yes",
    "7-0": "paidAmount",
    "7-1": "Decimal",
    "7-2": "결제 금액",
    "7-3": "No",
    "8-0": "currency",
    "8-1": "String",
    "8-2": "통화 코드",
    "8-3": "No",
    "9-0": "quantity",
    "9-1": "Int",
    "9-2": "수량",
    "9-3": "No",
    "10-0": "priceCode",
    "10-1": "String",
    "10-2": "가격 플랜 코드",
    "10-3": "Yes",
    "11-0": "productCode",
    "11-1": "String",
    "11-2": "상품 코드",
    "11-3": "Yes",
    "12-0": "productType",
    "12-1": "ProductType",
    "12-2": "주문 시점의 상품 타입  \n  \nProductType: 제품 유형  \n\\<허용 값>  \n  \nBOX: 배송상품  \nSOFTWARE: 무형의 상품(서비스 포함)  \nBUNDLE: 포함해서 판매하는 상품 (배송이 필요할 수도, 필요하지 않을 수도 있음. 현재 사용되지 않음.)  \nINVOICE: 청구서 페이지에서 생성될 때 설정되는 상품 유형  \nDRAFT: 초안",
    "12-3": "No",
    "13-0": "productName",
    "13-1": "String",
    "13-2": "주문 시점의 상품 이름",
    "13-3": "No",
    "14-0": "featuredImageUrl",
    "14-1": "String",
    "14-2": "상품 이미지 URL",
    "14-3": "Yes",
    "15-0": "selectedProductOptionLabel",
    "15-1": "String",
    "15-2": "선택한 상품 옵션",
    "15-3": "Yes",
    "16-0": "selectedProductOptionIds",
    "16-1": "List (Long)",
    "16-2": "선택한 옵션 ID 목록",
    "16-3": "No",
    "17-0": "planName",
    "17-1": "String",
    "17-2": "주문 시점의 가격 플랜 이름",
    "17-3": "No",
    "18-0": "discountName",
    "18-1": "String",
    "18-2": "할인 타입(주문 항목 타입이 DISCOUNT인 경우)",
    "18-3": "Yes",
    "19-0": "relatedOrderItemId",
    "19-1": "Long",
    "19-2": "연관된 주문 항목 (주문 항목 타입이 DISCOUNT인 경우)",
    "19-3": "Yes",
    "20-0": "priceSetupType",
    "20-1": "PriceOptionType",
    "20-2": "기본료 주문 항목인 경우 1회 또는 정기적으로 구분하는 타입  \n  \nPriceOptionType: 가격 옵션 유형  \n\\<허용 값>  \n  \nINITIALLY: 1회  \nPERIODIC: 주기적",
    "20-3": "Yes",
    "21-0": "demoCycle",
    "21-1": "DemoCycle",
    "21-2": "무료체험이 적용됐는지 적용 여부 및 기간  \n  \n(하단 참조)",
    "21-3": "Yes",
    "22-0": "minimumQuantity",
    "22-1": "Int",
    "22-2": "최소 구매 가능 수량",
    "22-3": "Yes",
    "23-0": "parentOrderItemCode",
    "23-1": "String",
    "23-2": "파생 주문 아이템의 부모(번들) 주문 아이템 코드",
    "23-3": "Yes"
  },
  "cols": 4,
  "rows": 24,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **`demoCycle`** 필드에는 **`demoCycle`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "num",
    "0-1": "Int",
    "0-2": "수령인 이름",
    "0-3": "No",
    "1-0": "type",
    "1-1": "DateUnitType",
    "1-2": "DateUnitType: 날짜 단위  \n(허용 값)  \n    - DAY: 일  \n    - WEEK: 주  \n    - MONTH: 개월  \n    - YEAR: 년 | No |",
    "1-3": "No"
  },
  "cols": 4,
  "rows": 2,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

### Payment

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "paymentId",
    "0-1": "Long",
    "0-2": "스텝페이 결제 번호",
    "0-3": "No",
    "1-0": "idKey",
    "1-1": "String",
    "1-2": "결제 정보 조회용 idKey",
    "1-3": "No",
    "2-0": "orderId",
    "2-1": "String",
    "2-2": "주문 번호 (paymentOnly = true 일때는 가맹점의 주문 번호)",
    "2-3": "Yes",
    "3-0": "customerId",
    "3-1": "String",
    "3-2": "주문 번호 (paymentOnly = true 일때는 가맹점의 고객 번호)",
    "3-3": "Yes",
    "4-0": "productName",
    "4-1": "String",
    "4-2": "결제 상품 명",
    "4-3": "Yes",
    "5-0": "paidAmount",
    "5-1": "Decimal",
    "5-2": "결제 금액",
    "5-3": "Yes",
    "6-0": "paidAt",
    "6-1": "LocalDateTime",
    "6-2": "결제 일시",
    "6-3": "Yes",
    "7-0": "status",
    "7-1": "String",
    "7-2": "결제 상태  \n\\<허용 값>  \n  \nSTANDBY: 대기중  \nCOMPLETE: 완료  \nCANCELED: 취소됨  \nPARTIAL_CANCELED: 부분 취소됨  \nUSER_CANCELED: 사용자에 의해 취소됨  \nCANCELED_FAIL: 취소 실패  \nFAILED: 실패  \nVIRTUAL_BANK_STANDBY: 가상계좌 대기중  \nCMS_STANDBY: CMS 대기중",
    "7-3": "No",
    "8-0": "paymentGateway",
    "8-1": "String",
    "8-2": "결제 PG  \n\\<허용 값>  \n  \nDANAL: 다날  \nKAKAO: 카카오페이  \nKG: KG이니시스  \nNICE: 나이스페이  \nGOOGLE: 구글플레이  \nBANKPAY (deprecated, \"뱅크페이\"로 변경된 BLUE_WALNUT을 사용하세요.): 뱅크페이  \nBLUEWALNUT: 블루월넛  \nKSNET: KSNET  \nTOSS: 토스  \nEXIMBAY: 엑심베이  \nSETTLE: 세틀뱅크  \nNICE_V2: 나이스페이 v2  \nSTRIPE: 스트라이프  \nPAYPLE: 페이플  \nPAYPLE_GLOBAL: 페이플 글로벌  \nUNKNOWN: 알 수 없음",
    "8-3": "No",
    "9-0": "paymentMethod",
    "9-1": "String",
    "9-2": "결제 수단  \n\\<허용 값>  \n  \nCARD: 신용카드  \nVBANK: 가상계좌  \nBANK: 계좌이체  \nCELLPHONE: 휴대폰 결제  \nSIMPLE_PAY: 간편결제  \nCMS: 통장결제  \nCARD_BILL: 신용카드 빌링  \nCELLPHONE_BILL: 휴대폰 결제 빌링  \nCMS_BILL: 통장결제 빌링",
    "9-3": "No",
    "10-0": "paymentOnly",
    "10-1": "Boolean",
    "10-2": "",
    "10-3": "Yes",
    "11-0": "errorMessage",
    "11-1": "String",
    "11-2": "에러 발생 시, 에러 메시지",
    "11-3": "Yes",
    "12-0": "cancel",
    "12-1": "Cancel",
    "12-2": "(하단 참조)",
    "12-3": "Yes",
    "13-0": "vBank",
    "13-1": "VBank",
    "13-2": "(하단 참조)",
    "13-3": "Yes",
    "14-0": "niceCms",
    "14-1": "NiceCms",
    "14-2": "(하단 참조)",
    "14-3": "Ye,s"
  },
  "cols": 4,
  "rows": 15,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **VBank**

  | 변수명           | 타입            | 설명    | Nullable |
  | ------------- | ------------- | ----- | -------- |
  | bankCode      | String        | 은행 코드 | Yes      |
  | bankName      | String        | 은행 명  | No       |
  | accountNumber | String        |       | No       |
  | accountName   | String        |       | No       |
  | bankDate      | LocalDateTime |       | No       |
- **NiceCms**

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "corporateManager",
    "0-1": "String",
    "0-2": "법인 명",
    "0-3": "No",
    "1-0": "companyName",
    "1-1": "String",
    "1-2": "회사 명",
    "1-3": "No",
    "2-0": "companyRegistrationNumber",
    "2-1": "String",
    "2-2": "신청인 정보",
    "2-3": "Yes",
    "3-0": "accountHolderSocialSecurityNumber",
    "3-1": "String",
    "3-2": "법인일 시, 사업자번호  \n개인일 시, 생년월일",
    "3-3": "No",
    "4-0": "bankCode",
    "4-1": "String",
    "4-2": "은행 코드  \n\\<허용 값>  \n  \nKDB: 한국산업은행  \nIBK: 기업은행  \nKB: 국민은행  \nKEB: 하나은행 (구외환)  \nSH: 수협중앙회  \nNH: 농협중앙회  \nWOORI: 우리은행  \nSC: 제일은행  \nHANMI: 한국씨티은행 (한미은행)  \nDGB: 대구은행  \nBNK_BS: 부산은행  \nKJB: 광주은행  \nJEJU: 제주은행  \nJB: 전북은행  \nBNK_KN: 경남은행  \nMG: 새마을금고  \nCREDIT_UNION: 신용협동조합중앙회  \nPOST: 우체국  \nHANA: 하나은행  \nSHINHAN_UNIFIED: 신한은행(조흥 통합)  \nKBANK: 케이뱅크  \nKAKAO_BANK: 카카오뱅크  \nTOSS_BANK: 토스뱅크",
    "4-3": "No",
    "5-0": "bankAccount",
    "5-1": "String",
    "5-2": "계좌 번호",
    "5-3": "No",
    "6-0": "date",
    "6-1": "LocalDateTime",
    "6-2": "'status' 가 발생한 일시",
    "6-3": "No",
    "7-0": "status",
    "7-1": "String",
    "7-2": "계좌 상태  \n\\<허용 값>  \n  \nACCOUNT_PENDING: 계좌 등록 진행중  \nACCOUNT_FAIL: 계좌 등록 실패  \nACCOUNT_SUCCESS: 계좌 등록 성공 (계좌 등록 성공 후 출금 진행중이 아닐때만 표시됨)  \nWITHDRAW_PENDING: 출금 진행중  \nWITHDRAW_FAIL: 출금 실패  \nWITHDRAW_SUCCESS: 출금 성공",
    "7-3": "No",
    "8-0": "errorReturn",
    "8-1": "String",
    "8-2": "",
    "8-3": "Yes"
  },
  "cols": 4,
  "rows": 9,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **Cancel**

  | 변수명              | 타입            | 설명       | Nullable |
  | :--------------- | :------------ | :------- | :------- |
  | canceledAmount   | Decimal       | 취소 금액    | No       |
  | lastCanceledDate | LocalDateTime | 최종 취소 일시 | Yes      |

***

### Customer

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "고객 번호",
    "0-3": "No",
    "1-0": "username",
    "1-1": "String",
    "1-2": "고객 아이디",
    "1-3": "Yes",
    "2-0": "name",
    "2-1": "String",
    "2-2": "고객 이름",
    "2-3": "Yes",
    "3-0": "email",
    "3-1": "String",
    "3-2": "고객 이메일",
    "3-3": "Yes",
    "4-0": "phone",
    "4-1": "String",
    "4-2": "고객 전화번호",
    "4-3": "Yes",
    "5-0": "shipping",
    "5-1": "Shipping",
    "5-2": "고객 기본 배송 정보  \n(하단 참조)",
    "5-3": "Yes",
    "6-0": "code",
    "6-1": "String",
    "6-2": "고객 코드",
    "6-3": "Yes",
    "7-0": "attributes",
    "7-1": "Map (String, String)",
    "7-2": "고객 추가 데이터",
    "7-3": "Yes",
    "8-0": "createdAt",
    "8-1": "LocalDateTime",
    "8-2": "고객 생성 시점",
    "8-3": "Yes",
    "9-0": "additionalRecipients",
    "9-1": "List (String)",
    "9-2": "추가 수신 이메일",
    "9-3": "Yes"
  },
  "cols": 4,
  "rows": 10,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

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

[block:parameters]
{
  "data": {
    "h-0": "변수명",
    "h-1": "타입",
    "h-2": "설명",
    "h-3": "Nullable",
    "0-0": "code",
    "0-1": "String",
    "0-2": "상품 코드",
    "0-3": "No",
    "1-0": "type",
    "1-1": "ProductType",
    "1-2": "ProductType: 상품 타입  \n\\<허용 값>  \n  \nBOX: 배송상품  \nSOFTWARE: 무형의 상품(서비스 포함)  \nBUNDLE: 포함해서 판매하는 상품 (배송이 필요할 수도, 필요하지 않을 수도 있음. 현재 사용되지 않음.)  \nINVOICE: 청구서 페이지에서 생성될 때 설정되는 상품 유형  \nDRAFT: 초안",
    "1-3": "Yes",
    "2-0": "status",
    "2-1": "ProductStatus",
    "2-2": "ProductStatus: 상품 상태  \n\\<허용 값>  \n  \nSALE: 판매 중  \nOUT_OF_STOCK: 재고 없음  \nUNSOLD: 판매되지 않음  \nWAITING_APPROVAL: 승인 대기 중  \nREJECTED: 거부됨",
    "2-3": "Yes",
    "3-0": "name",
    "3-1": "String",
    "3-2": "상품 이름",
    "3-3": "Yes",
    "4-0": "subTitle",
    "4-1": "String",
    "4-2": "부제목",
    "4-3": "Yes",
    "5-0": "featuredImageUrl",
    "5-1": "String",
    "5-2": "상품 대표 이미지 URL",
    "5-3": "Yes",
    "6-0": "imageUrls",
    "6-1": "List (String)",
    "6-2": "상품 이미지 URL",
    "6-3": "Yes",
    "7-0": "description",
    "7-1": "String",
    "7-2": "상품 설명",
    "7-3": "Yes",
    "8-0": "quantity",
    "8-1": "Int",
    "8-2": "재고 수량",
    "8-3": "Yes",
    "9-0": "optionGroups",
    "9-1": "List (ProductOptionGroup)",
    "9-2": "옵션 그룹 목록  \n(하단 참조)",
    "9-3": "Yes",
    "10-0": "prices",
    "10-1": "List (PriceSchema)",
    "10-2": "가격 플랜 목록  \n(하단 참조)",
    "10-3": "Yes",
    "11-0": "categories",
    "11-1": "List (ProductCategory)",
    "11-2": "카테고리 목록  \n(하단 참조)",
    "11-3": "Yes",
    "12-0": "createdAt",
    "12-1": "LocalDateTime",
    "12-2": "생성 시점",
    "12-3": "Yes",
    "13-0": "modifiedAt",
    "13-1": "LocalDateTime",
    "13-2": "수정 시점",
    "13-3": "Yes",
    "14-0": "enabledDemo",
    "14-1": "Boolean",
    "14-2": "무료 체험 활성화 여부",
    "14-3": "Yes",
    "15-0": "demoPeriod",
    "15-1": "Int",
    "15-2": "무료 체험 기간",
    "15-3": "Yes",
    "16-0": "demoPeriodUnit",
    "16-1": "DateUnitType",
    "16-2": "무료 체험 기간 단위",
    "16-3": "Yes"
  },
  "cols": 4,
  "rows": 17,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

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

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Nullable",
    "0-0": "priceCode",
    "0-1": "String",
    "0-2": "가격 코드",
    "0-3": "No",
    "1-0": "price",
    "1-1": "Decimal",
    "1-2": "가격 금액",
    "1-3": "No",
    "2-0": "unit",
    "2-1": "String",
    "2-2": "단위",
    "2-3": "Yes",
    "3-0": "type",
    "3-1": "PriceType",
    "3-2": "PriceType: 가격 유형  \n\\<허용 값>  \n  \nONE_TIME: 단건 상품  \nFLAT: 구독, 정액제 템플릿  \nUNIT_BASED: 건당 과금 템플릿  \nUSAGE_BASED: 사용량 기반  \nBUNDLE: 번들 플랜",
    "3-3": "Yes",
    "4-0": "membershipExpirationDate",
    "4-1": "Int",
    "4-2": "구독 만기 기간",
    "4-3": "No",
    "5-0": "membershipExpirationDateType",
    "5-1": "DateUnitType",
    "5-2": "구독 만기 기간 단위",
    "5-3": "Yes",
    "6-0": "setupOption",
    "6-1": "SetupOption",
    "6-2": "기본료 정보  \n(하단 참조)",
    "6-3": "Yes",
    "7-0": "options",
    "7-1": "List (PriceOption)",
    "7-2": "옵션 정보  \n(하단 참조)",
    "7-3": "No",
    "8-0": "additionalBilling",
    "8-1": "PriceAdditionalBilling",
    "8-2": "추가 과금 정보  \n(하단 참조)",
    "8-3": "Yes",
    "9-0": "recurring",
    "9-1": "Interval",
    "9-2": "구독 주기 단위  \n(하단 참조)",
    "9-3": "Yes",
    "10-0": "createdAt",
    "10-1": "LocalDateTime",
    "10-2": "생성된 시점",
    "10-3": "Yes",
    "11-0": "modifiedAt",
    "11-1": "LocalDateTime",
    "11-2": "수정된 시점",
    "11-3": "Yes",
    "12-0": "plan",
    "12-1": "Plan",
    "12-2": "플랜 정보  \n(하단 참조)",
    "12-3": "Yes",
    "13-0": "firstSaleEnabled",
    "13-1": "Boolean",
    "13-2": "첫 구매 할인 적용 여부",
    "13-3": "Yes",
    "14-0": "firstSalePrice",
    "14-1": "Long",
    "14-2": "첫 구매 할인 금액",
    "14-3": "Yes",
    "15-0": "claim",
    "15-1": "Claim",
    "15-2": "청구 방식 정보  \n(하단 참조)",
    "15-3": "Yes",
    "16-0": "basicServing",
    "16-1": "Int",
    "16-2": "기본 제공량 - 계정/사용량 기반 요금 사용시",
    "16-3": "No",
    "17-0": "bundlePrices",
    "17-1": "List (PriceBundle)",
    "17-2": "번들 플랜 - 번들 상품 구성  \n(하단 참조)",
    "17-3": "No",
    "18-0": "onetimeBundlePrice",
    "18-1": "Decimal",
    "18-2": "번들 플랜 - 단건 상품 금액",
    "18-3": "No"
  },
  "cols": 4,
  "rows": 19,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **SetupOption**

    **`setupOption`** 필드에는 **`SetupOption`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "기본료 번호",
    "0-3": "No",
    "1-0": "name",
    "1-1": "String",
    "1-2": "기본료 이름",
    "1-3": "Yes",
    "2-0": "type",
    "2-1": "PriceOptionType",
    "2-2": "기본료 타입  \n  \n- INITIALLY: 최초 1회  \n- PERIODIC: 정기적",
    "2-3": "Yes",
    "3-0": "price",
    "3-1": "Long",
    "3-2": "기본료 금액",
    "3-3": "No",
    "4-0": "claimMethodType",
    "4-1": "ClaimMethodType",
    "4-2": "선불/후불  \n  \n- PRE: 선불  \n- POST: 후불",
    "4-3": "No"
  },
  "cols": 4,
  "rows": 5,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **PriceAdditionalBilling**

    **`additionalBilling`** 필드에는 **`PriceAdditionalBilling`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Nullable",
    "0-0": "id",
    "0-1": "Long",
    "0-2": "추가 과금 번호",
    "0-3": "No",
    "1-0": "type",
    "1-1": "AdditionalBillingType",
    "1-2": "AdditionalBillingType: 추가 과금 유형  \n\\<허용 값>  \n  \nUSAGE_BASED_WITH_RANGE: 구간별 건당 과금  \nUSAGE_BASED_WITH_RANGE_AND_FIXED_PRICE: 구간별 고정 금액",
    "1-3": "No",
    "2-0": "ranges",
    "2-1": "List (PriceAdditionalBillingRange)",
    "2-2": "추가 과금 범위 정보  \n(하단참조)",
    "2-3": "No"
  },
  "cols": 4,
  "rows": 3,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **PriceAdditionalBillingRange**

  **`ranges`** 필드에는 **`PriceAdditionalBillingRange`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | Field Name | Type    | Description | Nullable |
  | ---------- | ------- | ----------- | -------- |
  | id         | Long    | 추가 과금 범위 번호 | Yes      |
  | until      | Long    | 범위가 어디까지인지  | Yes      |
  | price      | Decimal | 범위에 적용되는 금액 | Yes      |

- **Interval**

    **`recurring`** 필드에는 **`Interval`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Nullable",
    "0-0": "unit",
    "0-1": "DateUnitType",
    "0-2": "주기 단위  \nDateUnitType: 날짜 단위 타입  \n\\<허용 값>  \n  \n- DAY: 일  \n- WEEK: 주  \n- MONTH: 개월  \n- YEAR: 년",
    "0-3": "Yes",
    "1-0": "count",
    "1-1": "Int",
    "1-2": "주기",
    "1-3": "Yes"
  },
  "cols": 4,
  "rows": 2,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

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

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Type",
    "h-2": "Description",
    "h-3": "Nullable",
    "0-0": "methodType",
    "0-1": "ClaimMethodType",
    "0-2": "선불/후불",
    "0-3": "No",
    "1-0": "whenToClaimType",
    "1-1": "WhenToClaimType",
    "1-2": "후불인 경우, 청구 시점  \n  \n- FIRST_PAYMENT: 최초 결제일 기준 반복  \n- DATE: 결제일 지정",
    "1-3": "No",
    "2-0": "billingDate",
    "2-1": "Int",
    "2-2": "청구 시점 내 날짜 (익월 n일)",
    "2-3": "No",
    "3-0": "provideStartDay",
    "3-1": "Int",
    "3-2": "서비스 제공 시작일",
    "3-3": "Yes"
  },
  "cols": 4,
  "rows": 4,
  "align": [
    null,
    null,
    null,
    null
  ]
}
[/block]

- **PriceBundle**

    **`bundlePrices`** 필드에는 **`PriceBundle`** 객체가 포함됩니다. 이 객체의 구조는 다음과 같습니다.

  | Field Name  | Type   | Description | Nullable |
  | ----------- | ------ | ----------- | -------- |
  | productCode | String | 상품 코드       | Yes      |
  | priceCode   | String | 플랜 코드       | Yes      |
