---
description: Mobile SDKs for native Android and iOS apps.
---

# Mobile SDK

Securely collect sensitive cardholder data such as card number and cvv code in your native iOS or Android app with our new mobile SDKs. Completely outsource your tokenisation processes to our libraries and benefit from a simple, fully PCI DSS compliant integration and features such as: 

* Smart, secure and state of the art UI components
* Card brand identification and input validation
* Card scanner
* Theme support: Style various items according to your CI
* Dark mode support 

{% hint style="warning" %}
This section covers credit card number and cvv code tokenization only. \
If you need to process 3D-Secure authentication within your SDKs please refer to our [SDK 3D integration](../3d-secure-v2/authentication-only/mobile-sdk-3d.md). 
{% endhint %}

## 1. Distribution & Download

Access the latest version of our SDKs by following the links below and link the latest release to your app projects.

| OS      | Link                                                                                                                                                                                                                                                                  | Supported version |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| iOS     | <p>Github: <a href="https://github.com/datatrans/ios-sdk">Link</a></p><p>iOS SDK Reference: <a href="https://datatrans.github.io/ios-sdk/Classes/TokenizationRequest.html">Link</a></p>                                                                               | 11 +              |
| Android | <p>JFrog Repository: <a href="https://datatrans.jfrog.io/artifactory/mobile-sdk">Link</a></p><p>Android SDK Reference: <a href="https://datatrans.github.io/android-sdk/-datatrans%20-android%20-s-d-k/ch.datatrans.payment.api.tokenization/index.html">Link</a></p> | 5.0 +             |

## 2. Integration

As a next step, continue with the initialization of our iOS or Android SDK.

For iOS, you can add the SDK to your project by adding a new package dependency in Xcode. For Android, you can link the dependency with `implementation 'ch.datatrans:android-sdk:x.x.x'` and the repository with `maven { url "repositoryUrl" }`.

Create a tokenization object with your `merchantId` and `paymentMethodTypes` to start a tokenisation. Below is an example of the suggested minimum options to start a tokenisation with iOS (Swift) and Android (Kotlin, Java). Please read our detailed classes description for [iOS](https://datatrans.github.io/ios-sdk/Classes/TokenizationRequest.html) and [Android](https://datatrans.github.io/android-sdk/-datatrans%20-android%20-s-d-k/ch.datatrans.payment.api.tokenization/index.html) to discover more initialization options.

{% tabs %}
{% tab title="Swift" %}
```swift
let tokenizationRequest = TokenizationRequest(merchantId: merchantId, paymentMethodTypes: [.Visa, .MasterCard]) 
tokenizationRequest.delegate = self
tokenizationRequest.start(presentingController: navigationController)
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val tokenizationRequest = TokenizationRequest(merchantId, [VISA, MASTER_CARD])
tokenizationRequest.listener = this
TransactionRegistry.startTokenizationRequest(this, tokenizationRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
TokenizationRequest tokenizationRequest = new TokenizationRequest(merchantId, [VISA, MASTER_CARD]);
tokenizationRequest.setListener(this);
TransactionRegistry.INSTANCE.startTokenizationRequest(this, tokenizationRequest);
```
{% endtab %}
{% endtabs %}

After the tokenisation has been completed, `TokenizationRequestDelegate` will contain the `tokenizationId` and also tell you if a tokenization process was successful, canceled or resulted in an error.

#### Additional requirement for iOS

For the card scanner to work, a usage description for the camera use will be required in your .plist file. If you do not provide a description for the camera use, the app will crash when starting the card scanner.

{% code title=".plist File" %}
```markup
Key    :  Privacy - Camera Usage Description   
Value  :  $(PRODUCT_NAME) requires camera access to scan cards.
```
{% endcode %}

## 3. Obtain tokens

To obtain the tokenized values, you first need to submit the `tokenizationId` returned by the SDK to your server. 

Subsequently call the GET Token API from your **server** together with the `tokenizationId` to obtain a token for the card number and the cvv code. Additionally, the API returns the expiry dates, the fingerprint of the card number as well as the `cardInfo` object. 

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/tokenizations/{tokenizationId}" method="get" summary="GET Token" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="tokenizationId" type="integer" %}
`tokenizationId`

 returned from the library
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="string" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```javascript
{
    "alias": "AAABeO_NX9LssdexyrAAAQCsDugEAKc5",
    "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
    "maskedCard": "424242xxxxxx4242",
    "aliasCVV": "MnzXPMHJQYebRpmz-WZycWHG",
    "expiryYear": "21",
    "expiryMonth": "09",
    "cardInfo": {
        "brand": "VISA CREDIT",
        "type": "credit",
        "usage": "consumer",
        "country": "GB",
        "issuer": "DATATRANS"
    }
}
```
{% endswagger-response %}
{% endswagger %}

#### Examples

{% tabs %}
{% tab title="Request" %}
```java
curl -L -X GET 'https://api.sandbox.datatrans.com/v1/tokenizations/210329160815401747' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json'
```
{% endtab %}

{% tab title="Response" %}
```java
{
    "alias": "AAABeO_NX9LssdexyrAAAQCsDugEAKc5",
    "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
    "maskedCard": "424242xxxxxx4242",
    "aliasCVV": "MnzXPMHJQYebRpmz-WZycWHG",
    "expiryYear": "21",
    "expiryMonth": "09",
    "cardInfo": {
        "brand": "VISA CREDIT",
        "type": "credit",
        "usage": "consumer",
        "country": "GB",
        "issuer": "DATATRANS"
    }
}
```
{% endtab %}
{% endtabs %}

## Styling the Theme

You can style various options in our Mobile SDKs. Refer to the class `ThemeConfiguration` to adapt various colours to your corporate identity.

## Language Support

Our iOS and Android Mobile SDK integrations are currently translated and supported in the following languages:

English `en`German `de`French `fr`Italian `it`

Please get in touch should you need an additional language to be added for your checkout or if you find a translation error.
