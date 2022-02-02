# 3D Secure Mobile SDKs

<mark style="color:blue;">**3D Secure Mobile SDKs**</mark> allow you to securely collect and tokenize sensitive card data (card number and CVV code) in your native iOS or Android app while authenticating the cardholder via 3D Secure at the same time. Completely outsource your tokenizaton and authentication processes to our libraries and benefit from features such as:

* 3D Secure / SCA Ready: The SDK takes over the complexity of the 3DS process
* Smart, secure, and state of the art UI components
* Card brand identification and input validation
* Card scanner
* Store payment information for later use and fast checkout. Delegate the token selection to the library
* Theme support: Style various items according to your CI / Dark mode support&#x20;

{% hint style="warning" %}
Please note that it's currently not possible to use this API while sending the 3D Acquiring data dynamically. We're expecting to release this feature later this year.&#x20;
{% endhint %}

## Distribution & Download

Access the latest version of our SDKs by following the links below and linking the latest release to your app projects.

| OS      | Link                                                                                                                                                                                  | Supported version |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| iOS     | <p>Github: <a href="https://github.com/datatrans/ios-sdk">Link</a></p><p>iOS SDK Reference: <a href="https://datatrans.github.io/ios-sdk/index.html">Link</a></p>                     | 11 +              |
| Android | <p>JFrog Repository: <a href="https://datatrans.jfrog.io/artifactory/mobile-sdk">Link</a></p><p>Android SDK Reference: <a href="https://datatrans.github.io/android-sdk">Link</a></p> | 5.0 +             |

## 1. Initial Server-to-Server call

To start a 3D Secure Mobile SDK tokenization you have to call our init API from your server. The response returns a `mobileToken` which is required to initialize the libraries.

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions" method="post" summary="Init API" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA== 

\


see API Authentication data
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
API consumes application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" %}
Transaction amount in the currency's smallest unit. For example use 1000 for EU 10.00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="true" %}
3 letter ISO-4217 character. For example EUR or USD
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refno" type="string" %}
\[1..20] characters It should be unique each transaction
{% endswagger-parameter %}

{% swagger-parameter in="body" name="paymentMethods" type="string" required="true" %}
An array with one element: payment method short name 

`"AMX"`

 

`"CUP"`

 

`"ECA"`

 

`"DIN"`

 

`"DIS"`

 

`"JCB"`

 

`"VIS"`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card" type="object" %}
`card`

 object must contain the following parameter below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="createAliasCVV" type="boolean" %}
Whether a CVV alias should be created or not. If set to true a CVV alias will be created.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="option" type="object" %}
`option`

 object must contain the following parameters below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="authenticationOnly" type="boolean" %}
`true`

 

\


Indicates that an authentication should be triggered.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="createAlias" type="boolean" %}
Wheter a card number alias should be created or not. 

\


 If set to 

`true`

 a card number alias will be created.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="returnMobileToken" type="boolean" %}
`true`

\


Indicates that a mobile token should be created.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% tabs %}
{% tab title="Request" %}
```javascript
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/transactions' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json' \
--data-raw '{
    "amount": 1000,
    "currency": "EUR",
    "refno": "SDK 3D_test",
    "paymentMethods": [
        "ECA", "VIS"
    ],
    "card": {
        "createAliasCVV": true
    },
    "option": {
        "authenticationOnly": true,
        "createAlias": true,
        "returnMobileToken": true
    }
}'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "mobileToken": "cca3f978017a694e11e92c10d78e71f302eb982819eaa857"
}
```
{% endtab %}
{% endtabs %}

## 2. Integrate mobile SDK

Now that you have retrieved a `mobileToken`, you can continue with the initialization of our iOS or Android SDK. Make sure to call the library with your mobile token to start a transaction. Below is an example of the suggested minimum options to start a transaction with iOS (Swift, Objective-C) and Android (Kotlin, Java). Please read our detailed classes description for [iOS](https://docs.datatrans.ch/docs/mobile-sdk-2) and [Android](https://docs.datatrans.ch/docs/mobile-sdk-2) to discover more initialization options.

{% tabs %}
{% tab title="Java" %}
```java
Transaction transaction = new Transaction(mobileToken, aliasPaymentMethods);
transaction.setListener(this);
transaction.getOptions().setAppCallbackScheme("your_scheme");
transaction.getOptions().setTesting(true);
transaction.getOptions().setUseCertificatePinning(true);
TransactionRegistry.INSTANCE.startTransaction(this, transaction);
```
{% endtab %}

{% tab title="Swift" %}
```swift
let transaction = Transaction(mobileToken: mobile, aliasPaymentMethods: aliasPaymentMethods)
transaction.delegate = self
transaction.options.appCallbackScheme = "your_scheme"
transaction.options.testing = true
transaction.options.useCertificatePinning = true
transaction.start(presentingController: navigationController)
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
DTTransaction* transaction = [[DTTransaction alloc] initWithMobileToken:mobileToken aliasPaymentMethods:aliasPaymentMethods];
transaction.delegate = self;
transaction.options.appCallbackScheme = @"your_scheme";
transaction.options.testing = YES;
transaction.options.useCertificatePinning = YES;
[transaction startWithPresentingController:self.navigationController];
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val transaction = Transaction(mobileToken, aliasPaymentMethods)
transaction.listener = this
transaction.options.appCallbackScheme = "your_scheme"
transaction.options.isTesting = true
transaction.options.useCertificatePinning = true
TransactionRegistry.startTransaction(this, transaction)
```
{% endtab %}
{% endtabs %}

Once the card details have been collected, the 3D process will be started automatically. If required, the cardholder will be redirected to the website or the banking app of the card issuer to complete a challenge.&#x20;

After the transaction has been completed, you can refer to the class `TransactionSuccess` that will return the details of the transaction. If the transaction failed, you will have to refer to the class `transactionError` for further details instead. You may also implement `TransactionDelegate` (iOS) and `TransactionListener` (Android) to be notified when a transaction is successfully finalized, encounters an error, or is canceled by the user.&#x20;

#### Additional requirement for iOS

For the card scanner to work, a usage description for the camera use will be required in your .plist file. If you do not provide a description for the camera use, the app will crash when starting the card scanner.

{% code title=".plist File" %}
```markup
Key    :  Privacy - Camera Usage Description   
Value  :  $(PRODUCT_NAME) requires camera access to scan cards.
```
{% endcode %}

## Step 3: Obtain Tokens & 3D Secure data

To obtain the tokens as well as the authentication result, you first need to submit the `transactionId` returned by the SDK to your server.&#x20;

Subsequently, call the GET Status API from your **server** together with the `transactionId` to obtain a token for the card number and the CVV code. Additionally, the API returns an `3D` object which contains information about the result of the authentication process.&#x20;

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](broken-reference) for more information.&#x20;
{% endhint %}

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}" method="get" summary="Status API" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="transactionId" type="integer" required="true" %}
transactionId obtained via 

`/v1/transactions`
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "transactionId": "210609101239797372",
    "type": "payment",
    "status": "authenticated",
    "currency": "EUR",
    "refno": "SDK 3D_test",
    "paymentMethod": "ECA",
    "detail": {
        "authorize": {
            "amount": 1000
        }
    },
    "card": {
        "alias": "AAABee_Un5_ssdexyrAAAXULTeyzAAe1",
        "fingerprint": "F-c6FruvXTy36oJPosQUsRCf",
        "masked": "540400xxxxxx0001",
        "aliasCVV" : "HemcmX8TTB6Lipr_uF5IwG9M",
        "expiryMonth": "06",
        "expiryYear": "25",
        "3D": {
            "eci": "02",
            "xid": "MDAyMTA2MDkxMDEyMzk3OTczNzI=",
            "cavv": "OTkyMTA2MDkxMDEyNDkwOTc0MDY=",
            "threeDSVersion": "1.0.2",
            "cavvAlgorithm": "1",
            "directoryResponse": "Y",
            "authenticationResponse": "Y"
        }
    },
    "history": [
        {
            "action": "authenticate",
            "amount": 1000,
            "source": "api",
            "date": "2021-06-09T08:12:49Z",
            "success": true,
            "ip": "178.238.172.18"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Examples&#x20;

{% tabs %}
{% tab title="Request" %}
```java
curl -X GET \
  https://api.sandbox.datatrans.com/v1/transactions/190906151210861442 \
  -H 'Authorization: Basic MTEwMDAxNzY3NTpTejdodE5uSjdNM05YQ0lT' \

```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "transactionId": "210609101239797372",
    "type": "payment",
    "status": "authenticated",
    "currency": "EUR",
    "refno": "SDK 3D_test",
    "paymentMethod": "ECA",
    "detail": {
        "authorize": {
            "amount": 1000
        }
    },
    "card": {
        "alias": "AAABee_Un5_ssdexyrAAAXULTeyzAAe1",
        "fingerprint": "F-c6FruvXTy36oJPosQUsRCf",
        "masked": "540400xxxxxx0001",
        "aliasCVV" : "HemcmX8TTB6Lipr_uF5IwG9M",
        "expiryMonth": "06",
        "expiryYear": "25",
        "3D": {
            "eci": "02",
            "xid": "MDAyMTA2MDkxMDEyMzk3OTczNzI=",
            "cavv": "OTkyMTA2MDkxMDEyNDkwOTc0MDY=",
            "threeDSVersion": "1.0.2",
            "cavvAlgorithm": "1",
            "directoryResponse": "Y",
            "authenticationResponse": "Y"
        }
    },
    "history": [
        {
            "action": "authenticate",
            "amount": 1000,
            "source": "api",
            "date": "2021-06-09T08:12:49Z",
            "success": true,
            "ip": "178.238.172.18"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Styling the Theme

You can style various options in our Mobile SDKs. Refer to the class `ThemeConfiguration` to adapt various colours to your corporate identity.

## Language Support

Our iOS and Android Mobile SDK integrations are currently translated and supported in the following languages:

* English `en`
* German `de`
* French `fr`
* Italian `it`

Please get in touch should you need an additional language to be added for your checkout or if you find a translation error.
