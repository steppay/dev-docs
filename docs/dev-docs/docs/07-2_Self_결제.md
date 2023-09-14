---
stoplight-id: vfp2noeihod03
---

# 비관리형(Self) 결제 가이드

비관리형 결제는 스텝페이의 빌링 결제의 자동화된 기능들을 사용하지 않고 결제만 사용하고 싶을 때 사용하는 결제 서비스 입니다.
비관리형 결제를 통해 정기구독을 구현하려면 별도의 스케쥴러가 필요합니다. 비관리형 결제 기능을 결제 SDK로 제공하고 있으며 간편하게 연동하실 수 있습니다.

## 연관 가이드

- [인증 가이드](./01_인증.md)
- [결제 SDK 가이드](./09-2_결제_SDK.md#결제-sdk)

## 사전 준비 작업

- 스텝페이 포탈에서 [PG 설정](./07-0_결제.md#사전-준비-작업)을 통해 사용하고자 하는 PG가 설정되어 있어야 합니다.

### 최초 결제 하기

다음 순서대로 비관리형(Self) 결제를 연동할 수 있습니다.

`STEP 1` 연동하려는 페이지에서 스텝페이 결제 SDK를 import 합니다.

`STEP 2` 결제 요청을 원하는 시점에 결제 SDK의 결제 요청 메소드를 호출합니다.

`STEP 3` 이벤트 핸들러를 등록하고 결제 결과를 백엔드에서 검증합니다.

### 빌링 결제 하기(구독 갱신 결제)

빌링 결제는 빌링키를 이용한 결제로 사용자 인증 없이 결제를 시킬 수 있습니다. 해당 빌링키는 최초 결제에서 결제수단이 XXX_BILL (CARD_BILL, CMS_BILL) 인 경우에만 빌링키가 발급됩니다.

![setting_sdk.png](https://dev-vercel-dev-steppaykr.vercel.app/api/localize?dir=09_SDKs&name=setting_sdk.png)

```bash
curl --location 'https://api.steppay.kr/api/payment/billing' \
--header 'Secret-Token: ${Secret Token}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "idKey": "${IDKEY of the payment where the billing key was created}",
    "partner": {
        "partnerOrderId" : `${Order number managed by the partner}`,
        "partnerUserId": `${Customer number managed by the partner}`
    },
    "product" : {
          "itemName" : `${Product name managed by the partner}`,
          "amount" : `${Amount to be paid}`,
          "quantity" : `${Total quantity}`
    },
    "customer" : {
          "userName" : `${Customer name managed by the partner}`,
          "phone" : `${Customer phone number managed by the partner}`,
          "email" : `${Customer email managed by the partner}`
    }
}'
```

### 환불하기

```bash
curl --location 'https://api.steppay.kr/api/internal/payment/cancel' \
--header 'Secret-Key: ${Secret Token}' \
--header 'Content-Type: application/json' \
--data '{
    "idKey": "${IDKEY of the payment transaction you want to cancel}",
    "requestPrice": "${Refund amount}"
}'
```

## 결제 웹훅

비관리형(Self) 결제가 성공했을 때 전송됩니다.

### 요청 형식

| HTTP Method       | POST                                                 |
|-------------------|------------------------------------------------------|
| Content-Type 선택가능 | application/json,  application/x-www-form-urlencoded |


### 웹훅 본문

| Feild  | Type   | Required | Description |
|--------|--------|----------|------------|
| webHookType     | String   | 필수       | 웹훅 타입       |
| orderId     | Long   | 필수       | 주문 번호      |
| idKey | String | 필수       | 결제 idKey      |


```json
{
  "webHookType": "PAYMENT",
  "orderId": 1,
  "idKey": "16057932413479698c8vqQG0kMix9"
}
```

#### 웹훅 타입

| 상태                   | 설명                                   |
|----------------------|--------------------------------------|
| PAYMENT              | 결제 완료                                |
| VBANK                | 가상계좌 발급 완료                           |
| CANCELED             | 결제 취소 완료                             |
| USER_CANCELED        | 결제창에서 취소버튼을 눌렀을 때                    |
| FAILED               | 결제 실패                                |
| CMS                  | CMS로 최초 결제                           |
| BILLKEY (deprecated) | 결제 완료 (0원인 경우)<br>-`PAYMENT` 로 변경 예정 |