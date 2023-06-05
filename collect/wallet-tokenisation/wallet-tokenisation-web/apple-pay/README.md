---
description: Step-by-step implementation guide for Apple Pay direct integration
---

# Apple Pay

### 1. **Integrate Apple Pay API & Payment button**

Before you can request Apple Pay tokens, please [set up and configure Apple Pay](apple-pay-setup.md)[.](apple-pay-setup.md)

#### Apple Pay payment button implementation

{% hint style="info" %}
When you have completed the Apple Pay setup and requested a payment, integrate the Apple Pay button according the Apple brand guidelines ([https://developer.apple.com/design/human-interface-guidelines/technologies/apple-pay/buttons-and-marks](https://developer.apple.com/design/human-interface-guidelines/technologies/apple-pay/buttons-and-marks)) on your checkout page to collect cards stored in the Apple wallet.
{% endhint %}

### **2. Convert Apple Pay token into a PCI Proxy alias**

Look for the `ApplePayPaymentToken` object. You will find it in the `ApplePayPaymentAuthorizedEvent` object in the `onpaymentauthorized` event handler of the Apple Pay API. It contains the encrypted Apple Pay token and is called after the cardholder has authorized the Apple Pay payment with Touch ID, Face ID, or a passcode.

Submit the Apple Pay token to the PCI Proxy Vault endpoint to convert the Apple Pay token into a PCI Proxy token.

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

`APPLE_PAY`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" type="string" required="true" %}
Encrypted Apple Pay token returned by the Apple API
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
    {
  "requests": [
    {
      "type": "APPLE_PAY",
      "token": "{\"data\":\"xbvylStxG+RF5i1YukbZxhcKa4UIxkDCQed/hdfEnhptSkiSZcPeth8CcuxR2cU2xS2DPtO+sCKx5meY9cprZLsMNTu8YQ7ebPGBw43E07+BLjQc/0xeY09gMEqn50MsIjgDaSD4q/LjXtNNFsmB3nMBy4elNlo4AbS6ifqzpkVT6O3SPfg3iwih8DfTbbSIHcnfumPdb4p6I79cui9reMBjR6wD80GJT6VXi/FxkhoMkWbdFCxQFhn99fzCYBj/dSdZ/x8n3qITfg7m8FShJlxObtraNb8MRrfyW9jysIHrZI4OuEGc/X5DGEjlJUvoZSyatr151tRQp5SqQiKSV874b3o9ZMsMC6TlUaqJ22hpRzqddZbnD3S1gXs/i5r/1VCDOZjQXNdK3D2kS6MB9sU4MvJ64RcImj535HaZIQ==\",\"signature\":\"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\",\"header\":{\"publicKeyHash\":\"b9zDmQ+FYzEZJw9+q8idpA8fPtsSJ5+OpGiQDhCISQ0=\",\"ephemeralPublicKey\":\"MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEGZBfM5CWPdoTLorTKtVQDEeSu9bVdyxcYt0aAzR4HObZMqT98XlISVy2qjbg7Sq3kVLTHmhuIa6LW1nhyvy8PA==\",\"transactionId\":\"b1609bb088bd2995e043fcc2aeb6efad5545e55476bd933d0f3d75c1bfff7903\"},\"version\":\"EC_v1\"}" 
    }
  ]
}
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

Finally, use the alias and call the [Alias Status AP](../../../../store/manage/status.md)[I](../../../../store/manage/status.md) to obtain card meta data and 3D-Secure related information.&#x20;

Check the `walletIndicator` parameter to see the original wallet provider of the returned token.\
For Apple Pay it returns `APL`.&#x20;

**Strong customer authentication / liability shift**

{% hint style="warning" %}
Apple Pay tokens come with inbuilt 3D-Secure data such as `cavv` and `eci` value.

Please note, that the `eci` value is not always present. It is returned only for tokens on the Visa card network.

We still recommend to check with your payment provider directly if Apple Pay transactions grant liability shift by default as this can vary based on issuer country and card scheme brand.&#x20;
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

{% tab title="Response" %}
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
        "3D": {
          "cavv": "Y2WKsWYAEJFrtcP4DnTJMAACAAA=",
          "eci": "5"
    }
        "walletIndicator": "APL"
    }
}
```
{% endtab %}
{% endtabs %}

### Testing / Example

Visit [https://paymentbutton.datatrans.dev/](https://paymentbutton.datatrans.dev/) to see an example and test the Apple Pay integration (only works with Safari browser).

{% hint style="info" %}
Make sure to toggle `Output Token Data` and ignore the rest of the options available.&#x20;
{% endhint %}
