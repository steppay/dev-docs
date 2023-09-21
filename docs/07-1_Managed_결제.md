---
stoplight-id: ulwq2kcokkbf0
---

# 관리형(Managed) 결제 가이드

관리형(Managed) 결제는 결제 페이지 부터 스케쥴링, 구독, 배송 등의 서비스를 제공해주는 결제 서비스입니다.
구독에 대한 관리형 결제에서는 최초 결제 프로세스와 갱신 결제 프로세스를 구분하여 설명합니다.

<img src="https://docs-image-translator-steppay.vercel.app/api/localize?dir=07_payment&name=managed_paymnet_type.png" width="70%" style="display: block; margin: 0 auto; transition: none;">

## 연관 가이드

- [인증 가이드](https://docs.develop.steppay.kr/docs/guide/urvjmavys1lar-)
- [주문 가이드](https://docs.develop.steppay.kr/docs/guide/jash7i7rudebo-)
- [구독 가이드](https://docs.develop.steppay.kr/docs/guide/3fho91a9pl1bs-)

## 사전 준비 작업

관리형 결제를 위해서는 다음의 과정을 거쳐 결제 URL을 생성할 수 있습니다.

<img src="https://docs-image-translator-steppay.vercel.app/api/localize?dir=0_guide&name=process.png" width="80%" style="display: block; margin: 0 auto; padding: 10px; transition: none;">

- [Secret-Token 확인하기](https://docs.develop.steppay.kr/docs/guide/urvjmavys1lar-#1-secret-token)
- 주문이 생성되어 있어야 합니다.
    - 주문 생성 API의 Response에 `orderCode`를 확인하여 `orderCode`로 결제 URL요청이 가능합니다.
    - 주문 생성 API의 Response에 `idKey`를 확인하여 `idKey`로 결제 조회가 가능합니다.

## 최초 결제
최초 결제는 단건 또는 구독 상품의 첫 결제를 의미합니다. 최초 결제는 4가지 흐름으로 진행됩니다.

### 최초 결제 단계
![initial_payment.png](https://docs-image-translator-steppay.vercel.app/api/localize?dir=07_payment&name=initial_payment.png)

`STEP 1` 연동하려는 페이지에서 스텝페이 결제 화면을 표시합니다.

`STEP 2` 성공 또는 실패했을 시 요청한 URL로 REDIRECT되며, Query String에서 정보를 추출합니다.

`STEP 3` 추출한 정보로 데이터가 올바른지 검증합니다.

`STEP 4` 검증 결과에 따라 사용자에게 적절한 화면을 표시합니다.

### Step1: 결제창

스텝페이에서는 3가지 방법으로 결제 화면을 고객에게 보여줄 수 있습니다.
결제 화면을 호출하면 스텝페이 내의 시스템에서 결제 절차를 진행하게 되고, 결제 과정에서 결제가 성공하거나 실패하면 요청 파라미터의 Redicrect URL로 이동하게 됩니다.

#### 1. Redirection
고객의 브라우저에서 결제화면으로 이동하게 합니다.
    
```jsx
let params = {
    successUrl: `${successUrl}`,
    errorUrl: `${errorUrl}`
};
let url = new URL(`https://api.steppay.kr/api/public/orders/${orderCode}/pay`);
url.search = new URLSearchParams(params).toString();
// Redirection
window.location.href = url;
```
        
#### 2. Popup (Tab)
브라우저에서 결제화면을 팝업 창에서 띄우거나 새로운 탭에서 띄웁니다.
        
```jsx
let params = {
    successUrl: `${successUrl}`,
    errorUrl: `${errorUrl}`
};
let url = new URL(`https://api.steppay.kr/api/public/orders/${orderCode}/pay`);
url.search = new URLSearchParams(params).toString();
// New Tab or New Popup
window.open(url, "_blank");
```
        
#### 3. Iframe
Iframe 영역을 생성하고, 브라우저에서 Iframe 태그의 src 값을 수정합니다.
        
```jsx
let params = {
    successUrl: `${successUrl}`,
    errorUrl: `${errorUrl}`
};
let url = new URL(`https://api.steppay.kr/api/public/orders/${orderCode}/pay`);
url.search = new URLSearchParams(params).toString();
document.querySelector("#myIframe").src = url;
// Modifies the value inside the iframe.
// This will load the URL in the iframe
```

</br>

| property   | 타입     | 설명                                          |
|------------|--------|---------------------------------------------|
| successUrl | String | 결제 성공 시 Redirect URL                        |
| errorUrl   | String | 결제 실패 시 Redirect URL                        |
| orderCode  | String | [주문 생성 API](./05_주문.md)로 생성된 orderCode      |

### Step2: 결제화면 Callback 처리

스텝페이의 결제화면에서 결제 성공 또는 실패 시 `successUrl` 또는 `errorUrl` 로 Redicrect 되며, 결제 요청 결과를 Query String으로 전달합니다.
`successUrl` 또는 `errorUrl`은 아래와 같은 형식입니다.

```text
https://{partner-domain}.com/success?order_id=${order_id}&order_code=${order_code}&status=${status}
```

| property   | 타입     | 설명                         |
|------------|--------|----------------------------|
| order_id   | Int    | 스텝페이 주문 ID                 |
| order_code | String | 스텝페이 주문 코드                 |
| status     | String | 결제 결과 (“success”, “error”) |

### Step3: 결제 검증

화면에서 발생한 Redirection이 스텝페이의 결제화면에서 리다이렉션됐는지 확인할 수 있는 결제 검증 API를 개발합니다.
결제 응답의 Query String에 포함된 `order_code`를 사용해서 [주문 조회 API](https://docs.develop.steppay.kr/docs/api-reference/knup8adkdiv9i-)를 호출합니다.
주문 조회 API의 응답값에 `paymentDate` 프로퍼티 값이 null 이 아닌 경우 결제가 정상적으로 완료되었음을 확인할 수 있습니다. 

#### 검증 API 호출 예시

```jsx
<script>
document.querySelector("#myButton").addEventListener("click", function() {
        // 'Additional parameters' extracted from step2
		var params = new URLSearchParams(window.location.search);
    
    fetch('Payment verification API URL', {
        method: 'POST',
				headers: {
			    "Content-Type": "application/json",
			  },
			  body: JSON.stringify({
			    orderCode: params["order_code"],
			    orderId: params["order_id"],
			    status: params["order_id"],
			  }),
    })
    .then(response => response.json())
    .then(data => {
        // Show payment completed or failed payment data
    })
    .catch((error) => {
      console.error('Error:', error);
    });
});
</scrip>
```

#### 주문 조회 API 호출 예시 (node)
    
```jsx
const axios = require('axios');

let config = {
  method: 'get',
  url: 'https://api.steppay.kr/api/payment/receipt/${idKey}',
  headers: { 
    'Secret-Token': '${Secret-Token}'
  }
};

axios.request(config)
.then((response) => {
	const receiptResponse = JSON.stringify(response.data);
    // If status is successful
	if(status == "success" && receiptResponse.paymentDate !== null) {
		// Do some logic
	}else {
		// something went wrong
	}
	if(status == "error" && receiptResponse.paymentStatus == null) {
		// Do some logic
	}else {
		// something went wrong
	}
})
.catch((error) => {
  console.log(error);
});
```

## 정기 결제

스텝페이에서 구독 갱신이 성공하면 주문 웹훅을 통해 결과를 전달합니다. 
구독 상품을 이용하는 경우 주문 웹훅을 등록해야 실시간으로 결제 성공 이벤트를 받아보실 수 있습니다.

![recurring_payment.png](https://docs-image-translator-steppay.vercel.app/api/localize?dir=07_payment&name=recurring_payment.png)


### 정기 결제 단계

1. 스텝페이에서 구독 갱신 일자에 맞춰 정기결제를 진행합니다.
2. 갱신 성공 시 주문 웹훅을 전송합니다.
3. 주문 웹훅이 올바른지 검증하기 위해 주문 조회 API를 요청합니다.
4. 응답받은 주문 조회 결과로 전달받은 주문 웹훅을 검증합니다.

</br>
