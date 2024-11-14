---
stoplight-id: 1lr84j5dj2qyx
---

# Webhook 검증 (Signature)

웹훅 검증을 통해 Steppay에서 전송된 데이터가 실제로 Steppay에서 온 것인지 확인할 수 있습니다. 이 과정은 요청 헤더에 포함된 **`Steppay-Signature`** 값과 요청 본문을 비교하여 데이터를 검증하는 방식으로 이루어집니다.


## 사전 준비

### 웹훅 - `검증 KEY` 준비하기



서명 검증을 위해 필요한 검증 키를 Steppay 포탈에서 확인할 수 있습니다.

1. **[포탈 > 설정 > 결제 설정 > 웹훅 설정](https://portal.steppay.kr/setting/webhook)**으로 이동합니다.
2. 검증하고자 하는 웹훅의 상세 페이지에 들어갑니다.
3. 상세 페이지에서 "검증 KEY"를 복사합니다.


## 검증 단계

### 1. `Steppay-Signature` 헤더 구조 이해하기

```
timestamp=1706002316,key=BMFfPB/HjnZeJrwA4wC1csUDzkINZsaExF99X3/Q9phE=
```

**`Steppay-Signature`** 헤더는 다음과 같은 두 가지 정보를 포함합니다.

- **`timestamp`**: 웹훅이 발송된 시간 정보
- **`key`**: 검증을 위해 인코딩된 서명 값

### 2. `timestamp`와 요청 본문 결합하기

1. **`Steppay-Signature`** 헤더에서 **`timestamp`** 값을 추출합니다.
2. 추출한 **`timestamp`** 값과 웹훅 요청의 본문 데이터(**`requestBody`**)를 **`"timestamp.requestBody"`** 형식으로 결합합니다.

### 3. 결합된 문자열 암호화하기

1. 결합한 문자열을 Steppay 포탈에서 받은 검증 키와 함께 **`HmacSHA256`** 함수를 사용하여 암호화합니다.
    - 이 과정에서 결합된 문자열은 **`"timestamp.requestBody"`** 형식이어야 합니다.
    - 검증 키는 비밀 키로 사용됩니다.
2. 암호화된 결과값을 **Base64** 형식으로 인코딩합니다.

### 4. 헤더의 서명 값과 암호화 결과 비교하기

```
timestamp=1706002316,key=BMFfPB/HjnZeJrwA4wC1csUDzkINZsaExF99X3/Q9phE=;H3uZhieE19k/eF3ARNwjeQhdrJErf8Z8THV108mnC9w=
```

1. 인코딩된 결과값을 **`Steppay-Signature`** 헤더의 **`key`** 값과 비교합니다.
    - 헤더의 **`key`** 값이 여러 개일 경우 **`;`** 로 구분되며, 모든 **`key`** 값 중 하나라도 인코딩된 값과 일치하면 검증이 성공합니다.

## 검증 코드

검증 과정을 바로 사용하실 수 있도록 코드를 제공합니다.

- Javascript
    
    ```jsx
    const crypto = require('crypto');
    
    const SteppayWebhookUtil = {
        /**
         * Steppay-Signature 헤더 값과 요청 데이터, 비밀 키를 사용하여 서명을 검증합니다.
         *
         * @param {string} signature 수신받은 'Steppay-Signature' header 값
         * @param {string} payload 수신받은 request data 전문
         * @param {string} secret 포탈에서 발급받은 secret key
         * @throws {Error} 서명이 유효하지 않을 경우 에러를 발생시킵니다.
         */
        verifySignature: function(signature, payload, secret) {
            // timestamp, payload로 encodeKeys 생성
            const timestamp = signature.split(",", 2)
                .find(part => part.startsWith("timestamp="))
                .split("=")[1];
            const encodeKey = this.encodeHmacSha256(`${timestamp}.${payload}`, secret);
    
            // header의 encodeKeys 추출
            const headerEncodeKeys = signature.split(',')
                .find(part => part.startsWith('key='))
                .split('key=')[1]
                .split(';');
    
            // header의 encodeKeys와 생성한 encodeKeys 비교
            if (!headerEncodeKeys.some(headerEncodeKey => headerEncodeKey.includes(encodeKey))) {
                throw new Error("Invalid signature");
            }
        },
    
        /**
         * HmacSha256로 인코딩합니다.
         *
         * @param {string} payload
         * @param {string} secret
         * @return {string}
         */
        encodeHmacSha256: function(payload, secret) {
            const hmac = crypto.createHmac('sha256', secret);
            return hmac.update(payload).digest('base64');
        }
    };
    
    module.exports = SteppayWebhookUtil;
    ```
    
- Kotlin
    
    > 검증에 지속적으로 실패할 경우
    
    <aside> ⚠️ 만약 요청을 클래스로 받았을 때, 클래스를 문자열로 변환하는 방식에 따라 의도한대로 문자열 변환이 되지 않을 수 있습니다. 만약 검증 과정에서 지속적으로 문제가 생긴다면, 처음부터 데이터를 `String` 형태로 받는 것이 더 나을 수 있습니다.
    
    </aside>
    
    ```kotlin
    object SteppayWebhookUtil {
    
        /**
         * signature 검증합니다.
         *
         * @param signature 수신받은 'Steppay-Signature' header 값
         * @param payload 수신받은 request data 전문
         * @param secret 포탈에서 발급받은 secret key
         * @throws SteppaySignatureException Steppay 에서 발생하는 예외에 대한 custom exception을 재정의하는 것을 권장 드립니다.
         */
        fun verifySignature(
            signature: String,
            payload: String,
            secret: String,
        ) {
            // timestamp, payload로 encodeKeys 생성
            val timestamp = signature.split(",", limit = 2)[0].split("=")[1].toLong()
            val encodeKey = encodeHmacSha256("$timestamp.$payload", secret)
    
            // header의 encodeKeys 추출
            val headerEncodeKeys = signature.split(",")
                .map { it.split("=", limit = 2) }
                .filter { it[0] != "timestamp" }
                .map { it[1] }
    
            // header의 encodeKeys와 생성한 encodeKeys 비교
            if (headerEncodeKeys.none { headerEncodeKey -> headerEncodeKey.contains(encodeKey) }) {
                throw SteppaySignatureException("Invalid signature")
            }
        }
    
        /**
         * HmacSha256로 인코딩 합니다.
         *
         * @param payload String
         * @param secret String
         * @return String
         */
        private fun encodeHmacSha256(
            payload: String,
            secret: String,
        ): String {
            val sha256Hmac = Mac.getInstance("HmacSHA256")
            val secretKey = SecretKeySpec(secret.toByteArray(Charsets.UTF_8), "HmacSHA256")
            sha256Hmac.init(secretKey)
            return Base64.getEncoder().encodeToString(sha256Hmac.doFinal(payload.toByteArray(Charsets.UTF_8)))
        }
    }
    ```