---
stoplight-id: 7ykjolwxq67v2
---

# Iframe 가이드

## Iframe 호출 URL 및 파라미터

각각의 파라미터는 대부분 알림톡 또는 postMessage를 통해 동일한 이름으로 전달됩니다. 파라미터는 GET 방식으로 Query String 으로 전달할 수 있습니다.

### 복구 메인 화면

```
https://cover.steppay.kr/#/?token=1234abcd
```

- `token`: 복구 토큰 (복구 정보를 가져와서 표시합니다.)

### 복구 완료

```
https://cover.steppay.kr/#/recovery-complete/?token=1234abcd&paymentDate=2021-11-09%2020:08:00paymentInfo=A카드%20123*&useChange=true
```

- `token`: 복구 토큰 (복구 정보를 가져와서 표시합니다.)
- `paymentDate`: 결제일
- `paymentInfo`: 결제 수단(카드번호 등)
- `useChange`: 구독의 결제수단을 변경할 지 물어보려면 ‘true’로 설정

### 결제일 변경

```
https://cover.steppay.kr/#/change-date/?token=1234abcd
```

- token: 복구 토큰 -> 복구 정보를 가져와서 표시합니다.
- `token`: 복구 토큰 (복구 정보를 가져와서 표시합니다.)

### 결제일 변경 완료

```
https://cover.steppay.kr/#/change-date-complete/?date=2021-11-09%2020:12:00&productName=상품&price=5000
```

- `date`: 변경한 결제일
- `productName`: 상품명
- `price`: 상품 가격

### 나중에 알림

```
https://cover.steppay.kr/#/delay/?token=1234abcd&useDelay=true
```

- `token`: 복구 토큰 (복구 정보를 가져와서 표시합니다.)
- `useDelay`: ‘true’로 설정

### 결제 실패

```
https://cover.steppay.kr/#/payment-failed/?token=1234abcd&reason=한도초과
```

- `token`: 복구 토큰 (복구 정보를 가져와서 표시합니다.)
- `reason`: 실패 사유

## Iframe postMessage 형식

`event.data.action` 으로 어떤 이벤트가 발생했는지 전달되며 나머지 파라미터도 `event.data` 에 포함됩니다.

### payment-complete 파라미터

| 항목          | 설명                        |
| ----------- | ------------------------- |
| paymentInfo | 결제 수단 정보(카드번호 등)          |
| paymentDate | 결제 시점                     |
| token       | 복구 토큰                     |
| idKey       | 결제정보 idKey                |
| orderId     | 가맹점 주문 ID(partnerOrderId) |

### payment-failed 파라미터

| 항목     | 설명     |
| ------ | ------ |
| reason | 에러 메세지 |
| token  | 복구 토큰  |

### change-date 파라미터

| 항목           | 설명                        |
| ------------ | ------------------------- |
| orderId      | 가맹점 주문 ID(partnerOrderId) |
| selectedDate | 사용자가 선택한 결제일              |

### change-method 파라미터

| 항목      | 설명           |
| ------- | ------------ |
| token   | 복구 토큰        |
| orderId | 결제 완료된 주문 ID |

### redirect 파라미터

- 없음