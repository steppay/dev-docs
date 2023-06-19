# 비관리형 결제

비관리형 결제는 스텝페이의 빌링 결제의 자동화된 기능들을 사용하지 않고 **결제만** 사용하고 싶을 때 사용하는 결제 서비스 입니다.
비관리형 결제를 통해 정기구독을 구현하려면 별도의 스케쥴러가 필요합니다. 비관리형 결제 기능을 결제 SDK로 제공하고 있으며 간편하게 연동하실 수 있습니다.

## 연관된 가이드

- [인증](./01_인증.md)
- [결제 SDK](./09-2_결제_SDK.md#결제-sdk)

## 사전 준비 작업

- [PG 설정](./07-0_결제.md#pg-설정하기)

## How-To

### 최초 결제 하기

다음 순서대로 Self 결제를 연동할 수 있습니다.

STEP 1. 연동하려는 페이지에서 스텝페이 [결제 SDK](https://www.notion.so/SDK-971bbbde6cd749059b4cc9b660f10ba9?pvs=21)를 import 합니다.

STEP 2. 결제 요청을 원하는 시점에 결제 SDK의 결제 요청 메소드를 호출합니다.

STEP 3. 이벤트 핸들러를 등록하고 결제 결과를 백엔드에서 검증합니다.

→ 결제 SDK에 대한 자세한 사용 방법은 [결제 SDK](https://www.notion.so/SDK-971bbbde6cd749059b4cc9b660f10ba9?pvs=21) 문서를 확인해주세요.

### 빌링 결제 하기

![스크린샷 2023-06-15 오후 6.29.33.png](Self%20%E1%84%80%E1%85%A7%E1%86%AF%E1%84%8C%E1%85%A6%20582771af8d7942f9a9f696f4ba46fc9b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-15_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_6.29.33.png)

빌링 결제는 빌링키를 이용한 결제로 사용자 인증 없이 결제를 시킬 수 있습니다. 해당 빌링키는 최초 결제에서 결제수단이 XXX_BILL (CARD_BILL, CMS_BILL) 인 경우에만 빌링키가 발급됩니다.

```bash
curl --location 'https://api.steppay.kr/api/payment/billing' \
--header 'Secret-Token: ${Secret Token}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "idKey": "${빌링키가 생성된 결제의 IDKEY}",
    "partner": {
        "partnerOrderId" : `${가맹점이 관리하는 주문번호}`,
        "partnerUserId": `${가맹점이 관리하는 고객번호}`
    },
    "product" : {
          "itemName" : `${가맹점이 관리하는 상품이름}`,
          "amount" : `${결제되어야 할 금액}`,
          "quantity" : `${총 수량}`
    },
    "customer" : {
          "userName" : `${가맹점이 관리하는 고객 이름}`,
          "phone" : `${가맹점이 관리하는 고객 휴대폰번호}`,
          "email" : `${가맹점이 관리하는 고객 이메일}`
    }
}'
```

### 환불 하기

```bash
curl --location 'https://api.steppay.kr/api/internal/payment/cancel' \
--header 'Secret-Key: ${Secret Token}' \
--header 'Content-Type: application/json' \
--data '{
    "idKey": "${취소하고자 하는 결제건의 IDKEY}",
    "requestPrice": "${환불 금액}"
}'
```

## 결제 웹훅

Self 결제가 성공했을 때 전송됩니다.

### 요청 형식

| HTTP Method | POST |
| --- | --- |
| Content-Type 선택가능 | application/json,  application/x-www-form-urlencoded |

### 웹훅 본문

---

**webHookType** 필수 String

웹훅 타입

- `PAYMENT`: 결제 완료
- `VBANK`: 가상계좌 발급 완료
- `CANCELED`: 결제 취소 완료
- `USER_CANCELED`: 결제창에서 취소버튼을 눌렀을 때
- `FAILED`: 결제 실패
- `CMS`: CMS로 최초 결제
- `BILLKEY` (deprecated): 결제 완료 (0원인 경우)
    - `PAYMENT` 로 변경 예정

---

**orderId** 필수 Long

주문 아이디

---

idKey 필수 String

결제 idKey

---

```json
{
  "webHookType": "PAYMENT",
  "orderId": 1,
	"idKey": "16057932413479698c8vqQG0kMix9"
}
```