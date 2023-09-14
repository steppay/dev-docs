# Get Started

스텝페이는 정기구독부터 소프트웨어 구독, 단건 상품까지 쉽게 생성하고 관리할 수 있는 구독 결제 플랫폼입니다.

![product.png](https://dev-vercel-steppay-kr.vercel.app/api/localize?dir=0_guide&name=product.png)


스텝페이는 상품과 플랜을 따로 관리합니다. 그러므로 다양한 가격 정책을 사용하더라도 재고 관리에 용이합니다.  
손쉽게 실물상품, 소프트웨어 상품, 번들 상품을 생성할 수 있으며 한 상품에 여러 개의 가격 플랜을 생성할 수 있습니다.  
이처럼 생성된 가격 플랜과 상품은 리스트로 한 눈에 확인할 수 있으며 각 상태별로도 확인 가능합니다.

모든 데이터는 스텝페이에서 관리하므로 데이터 저장이 따로 필요하지 않습니다.  
API 연동만으로 손쉽게 데이터를 호출하고 저장할 수 있습니다.

[상품 생성 API 보러 가기](https://docs.steppay.kr/reference/createproduct)

[가격 플랜 생성 API 보러 가기](https://docs.steppay.kr/reference/createproductprice)


# dd


![process.png](https://dev-vercel-steppay-kr.vercel.app/api/localize?dir=0_guide&name=process.png)

스텝페이에서 다음의 과정을 거쳐서 결제를 시작해볼 수 있습니다.

</br>

## STEP 1. 고객 생성

주문을 생성하기 위해서는 고객 데이터가 필요합니다.  
고객은 [고객 생성 API](https://docs.steppay.kr/reference/createcustomer)를 이용하여 추가, 생성할 수 있습니다.

<br />

## STEP 2. 상품 생성

마찬가지로 주문을 생성하기 위해서는 상품이 필요합니다.  
상품은 포탈에 있는 상품 빌더를 통해서 생성 가능합니다.

<br />

## STEP 3. 가격 플랜 생성

상품을 생성한 후 가격 플랜에 따라 실제 판매 가격과 판매 방식(단건, 정기 등)이 정해집니다.  
가격 플랜은 상품 빌더에서 상품 생성 후에 판매 가격 및 방식을 등록할 수 있습니다.

<br />

## STEP 4. 주문 생성

고객, 상품, 가격플랜이 있으면 주문을 생성할 수 있습니다.  
주문은 [주문 생성 API](https://docs.steppay.kr/reference/createorder)에서 생성할 수 있습니다.

<br />

## STEP 5. 결제 링크 생성

다음과 같은 형식의 주소를 통해 스텝페이 결제화면을 사용할 수 있습니다.  
[주문 생성 API](https://docs.steppay.kr/reference/createorder)를 이용해 주문을 생성한 후 주문 코드를 사용해서 결제 연동을 하실 수 있습니다.

파라미터로 콜백 URL을 넘겨서 결제 후 처리를 할 수 있습니다.

> 📘 결제 링크 형식
>
> - `https://api.steppay.kr/api/public/orders/${order_code}/pay`
> - 파라미터
    >   - successUrl: 결제 성공 시 해당 주소로 리다이렉트 됩니다.
>   - errorUrl: 에러 발생시 해당 주소로 리다이렉트 됩니다.
>   - cancelUrl: 결제 화면창의 닫기 버튼을 누를 시 해당 주소로 리다이렉트 됩니다.

<br />

## STEP 6. 결제 연동

결제 링크를 통해서 결제가 이루어지면, 파라미터로 전달된 URL을 통해서 결제 결과가 전달됩니다. 다음 세 가지 방식을 이용하여 결제를 연동할 수 있습니다.  
<br />

### 리다이렉트

결제주소로 직접 이동하여 처리하는 방식입니다.

#### 예제 코드

```javascript
function redirectPay() {
    var url = "https://api.steppay.kr/api/public/orders/order_abcd/pay?successUrl=https://your-site.com&errorUrl=https://your-site.com&cancelUrl=https://your-site.com";
    window.location.href = url;
}
```

### 팝업

팝업 형태로 결제 화면을 표시하는 방식입니다.

#### 예제 코드

```javascript
function popupPay () {
    var url = "https://api.steppay.kr/api/public/orders/order_abcd/pay?successUrl=https://your-site.com&errorUrl=https://your-site.com&cancelUrl=https://your-site.com";
    var name = "popup test";
    var option = "width = 425, height = 812, top = 100, left = 200, location = no";
    window.open(url,name,option);
}
```

### iframe

iframe으로 현재 화면에 결제 화면을 포함시키는 방식입니다.

#### 예제 코드

```javascript
function iframePay () {
    const iframe = document.createElement("iframe");
    iframe.id = "steppay__iframe";
    iframe.src = "https://api.steppay.kr/api/public/orders/order_abcd/pay?successUrl=https://your-site.com&errorUrl=https://your-site.com&cancelUrl=https://your-site.com";
    document.body.appendChild(iframe);
}
```

### 연동 파라미터

결제 연동시 파라미터로 전달된 주소로 결과가 전달될 때, 주문 코드가 파라미터로 전달됩니다.

> 📘 결과 전달 주소 예시(`https://your-site.com` 을 파라미터로 넘긴 경우)
>
> `https://your-site.com?order_code=order_abcd&status=[success> or error]`

전달 받은 order_code로 주문을 조회하여 상태를 확인하신 후, 주문 완료에 대한 후처리를 진행하시면 됩니다.

주문완료 상태는 [주문 상세 조회API](https://docs.steppay.kr/reference/getorderdetail)를 통해 주문 상태를 확인하시면 됩니다.

<br />

### 팝업과 iframe 사용 시 권장사항

- 결제 안정성을 위해서 인터랙션을 막는 것을 권장합니다.
- width: 425px, height: 812px 지정을 권장합니다.