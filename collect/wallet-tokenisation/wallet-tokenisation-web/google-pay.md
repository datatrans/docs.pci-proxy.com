---
description: Step-by-step implementation guide for Google Pay direct integration
---

# Google Pay

### 1. **Integrate Google Pay API & Payment button**

Start with implementing the Google Pay API to receive encrypted Google Pay tokens. Follow this step-by-step integration tutorial of [Google](https://developers.google.com/pay/api/web/guides/tutorial)  to learn how it works.&#x20;

{% hint style="info" %}
**Google setup (**[**https://developers.google.com/pay/api/web/guides/setup**](https://developers.google.com/pay/api/web/guides/setup)**)**\
\
Before you can start, you need to create a **Google developer account** and select `datatrans` as your payment gateway in the sign-up process. Additionally make sure to whitelist all domains (including subdomains) from which you intend to call the Google Pay API in your Google developer account.
{% endhint %}

When you submit a payment request to the Google Pay API, make sure to specify `datatrans` as a PSP.

**Example**

```javascript
const tokenizationSpecification = {
  type: 'PAYMENT_GATEWAY',
  parameters: {
    'gateway': 'datatrans',
    'gatewayMerchantId': 'PCIP_merchantId' // You find this value in the PCIP dashboard
  }
};
```

#### Payment button implementation

{% hint style="info" %}
To collect cards stored in the Google wallet, integrate the Google Pay button according the Google brand guidelines ([https://developers.google.com/pay/api/web/guides/brand-guidelines](https://developers.google.com/pay/api/web/guides/brand-guidelines)) on your checkout page.&#x20;
{% endhint %}

### **2. Convert Google Pay token into a PCI Proxy alias**

Look for the `PaymentMethodTokenizationData` under the property`PaymentMethodData` in the Google API response. You find the encrypted Google Pay token and related card information here.\
\
Submit the Google Pay token to the PCI Proxy Vault endpoint to convert the Google Pay token into a PCI Proxy token.

{% swagger method="post" path="/v1/aliases/tokenize" baseUrl="https://api.sandbox.datatrans.com" summary="Tokenisation request" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" type="string" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="true" type="string" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="requests" type="array" %}
Array of objects. List of tokenisation requests. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" required="true" %}
Type of wallet provider. 

`GOOGLE_PAY`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" type="string" required="true" %}
Encrypted Google Pay token returned by the Google API
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Successful tokenization" %}

{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid request: Returns an error object with an error code and error message." %}
```
{
  "error": {
    "code": Enum: "INVALID_PLAIN_VALUE" "INVALID_EXPIRATION" "CLIENT_ERROR" "INVALID_JSON_PAYLOAD" "ALIAS_NOT_FOUND" "INVALID_CVV" "UNKNOWN_ERROR" "UNRECOGNIZED_PROPERTY" "INVALID_ALIAS" "SERVER_ERROR" "ILLEGAL_ARGUMENT" "UNAUTHORIZED" "INVALID_PROPERTY" "MAX_REQUESTS_PER_CALL_EXCEEDED" "VELOCITY_ERROR",
    "message": "A human readable message indicating what went wrong."
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Request" %}
```json
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/aliases/tokenize' \
-H 'Content-Type: application/json' \
-H 'Authorization: {merchantId}:{password}' \
--data-raw '{
    "requests": [        
    {            
     "type": "GOOGLE_PAY",
     "token": "{\"signature\":\"MEYCIQD559RrzAfNW3mfmehndtSlAXcC+lOWUg6RBc0dOtmdxgIhAIdv0miM/oRQ8xfPa/p3uovbs+27tOMXaaAACLwobZf1\",\"intermediateSigningKey\":{\"signedKey\":\"{\\\"keyValue\\\":\\\"MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEf4SyX8QQbT/Wo3ZnMyjIL6bFh5Nr66im3+kdbYj1y0DfkTvzJpE9HNkjDqqSgJhs62DdZImKKobGStRy54RAmA\\\\u003d\\\\u003d\\\",\\\"keyExpiration\\\":\\\"1679120930439\\\"}\",\"signatures\":[\"MEUCIF0ap1buoWm9Y2CuekBLkAdYHD5OFq76cSZr8l1W/VHKAiEAgpbalaMOCVZ3/A9hmamMoX3KSLDtL4f/nu2FE5MzVm0\\u003d\"]},\"protocolVersion\":\"ECv2\",\"signedMessage\":\"{\\\"encryptedMessage\\\":\\\"MgYeSvqF2bOGjSksSOnQh4CYHpLOcMOMfltgLzypmWN/BU4kgso7wbxW9p1qjlzLaRx5cZfH9SbsLn7n3AJroW/Qak/iyAp8iPw803Kb3HnSHBFRdOkMeaxv2FvrORwjaSbxSnvWVIT/ZiEap0Q2xhwT+o0+YYr5KVJ+kDGYYK0wCEyl3wb4p+p/e7yCoNiCBrW8TIgNmwhnHV9uB9nmPw/7XVMqCr+pmoxQke7aVR0ee6Zdw16Rqnbpf4Cn4Vy7lwk7r2PNMmtsxMo9NLkcE3ntcbC+QIJxuOMXjFcNY3WTbeKZV5sQx/CuBJSaxpHczyL9hoATm7rcqw3GuSOsjRo71xr9Kl7irC3HEcal3aYqvT+tcTwubEg7UlY444pZPPluSSrwYIkRlH5TpjXTqMBKzpFuBklLRaYIp39mWvYlfSy+y414uIg0ukE9odqQBTdtVhB627KGXqrlibv2CfG1SwQ+A5XM7ysIt2DlNYFy+VVubmcQ/JzEXvCE0huZzqyYx43V+KF3zkyEwO5KQe31c2Bk0nj8YN7r8/9fkA\\\\u003d\\\\u003d\\\",\\\"ephemeralPublicKey\\\":\\\"BHvkCpwm78DpTI0WhyTPTj++Wt5hvcBdH4Q1xEVSSa/535/iKoXu9viS40MAuXXEu1GG8NdZcZ4sU5i8I/XHnKs\\\\u003d\\\",\\\"tag\\\":\\\"Qm4JzZw4it2SAx2CRfc0Texiwfmlgxst0urfrX8bdKk\\\\u003d\\\"}\"}"
    }    
  ]
}'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "overview": {
        "total": 1,
        "successful": 1,
        "failed": 0
    },
    "responses": [
        {
            "type": "CARD",
            "alias": "7LHXscqwAAEAAAGEiwgfM8CBTPrzACwH",
            "maskedCC": "489537xxxxxx6287",
            "fingerprint": "F-fgxnFwN-gsIw7y80T-kpBB"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### **3. Obtain card meta data and 3D relevant information**

Finally, use the alias and call the [Alias Status AP](../../../store/manage/status.md)[I](../../../store/manage/status.md) to obtain card meta data. It also returns 3D-Secure related information if available.&#x20;

Check the `walletIndicator` parameter to see the original wallet provider of the returned token. \
For Google Pay it returns `PAY`. \


**Strong customer authentication / liability shift**

{% hint style="warning" %}
The Google Pay API might return cards on file on Google.com (`PAN_ONLY`) or a device token on an Android-powered device authenticated with a 3D-Secure cryptogram (`CRYPTOGRAM_3DS`).&#x20;

In case of a `CRYPTOGRAM_3DS` enabled card, 3D-Secure related data such as `eci` and `cavv` value will be present in the response of the Alias Status API. \
Please note that, the `eci` value is not always present. It is returned only for tokens on the Visa card network.



For cards with authentication method `PAN_ONLY` no 3D object is returned and a separate 3D-Secure authentication step-up might be required. Please refer to [Authenticate](../../../authenticate/3d-secure-api.md) if you want to process 3D-Secure with PCI Proxy. \


The Google PAY API allows you to control which authentication method you want to offer to your customers with the following option in the Google Pay API:

```
const allowedCardAuthMethods = ["PAN_ONLY", "CRYPTOGRAM_3DS"];
```
{% endhint %}

**Example Alias Status API**

{% tabs %}
{% tab title="Request" %}
```javascript
curl -L -X GET 'https://api.sandbox.datatrans.com/v1/aliases/7LHXscqwAAEAAAGHLZMxjcu65Ep6AAhH' \
-H 'Authorization: {merchantId}:{password}' \
-H 'Content-Type: application/json' \
--data-raw ''
```
{% endtab %}

{% tab title="Response PAN_ONLY" %}
```javascript
{
    "alias": "7LHXscqwAAEAAAGHLZMxjcu65Ep6AAhH",
    "fingerprint": "F-fkO8WHlN03g-bhs44wFI9J",
    "type": "CARD",
    "masked": "412374xxxxxx0013",
    "dateCreated": "2023-03-28T13:33:53Z",
    "card": {
        "panRemoved": false,
        "expiryMonth": "06",
        "expiryYear": "25",
        "cardInfo": {
            "brand": "VISA",
            "type": "credit",
            "usage": "consumer",
            "country": "US",
            "issuer": ""
        },
        "walletIndicator": "PAY"
    }
}
```
{% endtab %}

{% tab title="Response CRYPTOGRAM_3DS" %}
```javascript
{
    "alias": "7LHXscqwAAEAAAGHLZ1mxzlxFJc6AEcT",
    "fingerprint": "F-fkO8WHlN03g-bhs44wFI9J",
    "type": "CARD",
    "masked": "412374xxxxxx0013",
    "dateCreated": "2023-03-29T13:45:02Z",
    "card": {
        "panRemoved": false,
        "expiryMonth": "06",
        "expiryYear": "25",
        "cardInfo": {
            "brand": "VISA",
            "type": "credit",
            "usage": "consumer",
            "country": "US",
            "issuer": ""
        },
        "3D": {
            "cavv": "AgAAAAAABk4DWZ4C28yUQAAAAAA=",
            "eci": "07"
        },
        "walletIndicator": "PAY"
    }
}
```
{% endtab %}
{% endtabs %}

### Testing / Example

Visit [https://paymentbutton.datatrans.dev/](https://paymentbutton.datatrans.dev/) to see an example and test the Google Pay integration.

{% hint style="info" %}
Make sure to toggle `Output Token Data` and ignore the rest of the options available.

You can use real cards stored in the Google Pay wallet. Google will replace them by their own testcards. &#x20;
{% endhint %}
