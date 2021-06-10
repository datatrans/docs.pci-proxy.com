---
description: Mobile SDKs 3D for native Android and iOS apps.
---

# Mobile SDK 3D

Securely collect sensitive cardholder data such as card number and cvv code in your native iOS or Android app with our new mobile SDKs. Completely outsource your tokenisaton processes to our libraries and benefit from a simple, PCI DSS compliant integration and features such as: 

* 3D Secure / SCA Ready: The SDK takes over the complexity of the 3DS process
* Smart, secure and state of the art UI components
* Card brand identification and input validation
* Card scanner
* Store payment information for later use and fast checkout. Delegate the token selection to the library
* Theme support: Style various items according your CI / Dark mode support 

{% hint style="warning" %}
Please note that it's currently not possible to use this API while sending the 3D Acquiring data dynamically. We're expecting to release this feature later this year. 
{% endhint %}

## Distribution & Download

Access the latest version of our SDKs by following the links below and link the latest release to your app projects.

<table>
  <thead>
    <tr>
      <th style="text-align:left">OS</th>
      <th style="text-align:left">Link</th>
      <th style="text-align:left">Supported version</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">iOS</td>
      <td style="text-align:left">
        <p>Github: <a href="https://github.com/datatrans/ios-sdk">Link</a>
        </p>
        <p>iOS SDK Reference: <a href="https://datatrans.github.io/ios-sdk/index.html">Link</a>
        </p>
      </td>
      <td style="text-align:left">11 +</td>
    </tr>
    <tr>
      <td style="text-align:left">Android</td>
      <td style="text-align:left">
        <p>JFrog Repository: <a href="https://datatrans.jfrog.io/artifactory/mobile-sdk">Link</a>
        </p>
        <p>Android SDK Reference: <a href="https://datatrans.github.io/android-sdk">Link</a>
        </p>
      </td>
      <td style="text-align:left">5.0 +</td>
    </tr>
  </tbody>
</table>

## 1. Initial Server-to-Server call

To start a 3D mobile SDK tokenisation you have to call our init API from your server. The response returns a `mobileToken` which is required to initialise the libraries.

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions" %}
{% api-method-summary %}
Init API
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==   
see API Authentication data
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
API consumes application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="amount" type="string" required=true %}
Transaction amount in the currency's smallest unit. For example use 1000 for EU 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="string" required=true %}
3 letter ISO-4217 character. For example EUR or USD
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
\[1..20\] characters It should be unique each transaction
{% endapi-method-parameter %}

{% api-method-parameter name="paymentMethods" type="string" required=true %}
An array with one element: payment method short name `"AMX"` `"CUP"` `"ECA"` `"DIN"` `"DIS"` `"JCB"` `"VIS"`
{% endapi-method-parameter %}

{% api-method-parameter name="card" type="object" required=false %}
`card` object must contain the following parameter below
{% endapi-method-parameter %}

{% api-method-parameter name="createAliasCVV" type="boolean" required=false %}
Whether a CVV alias should be created or not. If set to true a CVV alias will be created.
{% endapi-method-parameter %}

{% api-method-parameter name="option" type="object" required=true %}
`option` object must contain the following parameter below
{% endapi-method-parameter %}

{% api-method-parameter name="authenticationOnly" type="boolean" required=true %}
`true`   
Indicates that an authentication should be triggered.
{% endapi-method-parameter %}

{% api-method-parameter name="createAlias" type="boolean" required=false %}
Wheter a card number alias should be created or not.   
 If set to `true` a card number alias will be created.
{% endapi-method-parameter %}

{% api-method-parameter name="returnMobileToken" type="boolean" required=true %}
`true`  
Indicates that a mobile token should be created.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

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

Now that you have retrieved a `mobileToken`, you can continue with the initialization of our iOS or Android SDK. Make sure to call the library with your mobile token to start a transaction. Below is an example of the suggested minimum options to start a transaction with iOS \(Swift, Objective-C\) and Android \(Kotlin, Java\). Please read our detailed classes description for [iOS](https://docs.datatrans.ch/docs/mobile-sdk-2) and [Android](https://docs.datatrans.ch/docs/mobile-sdk-2) to discover more initialization options.

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

Once the card details have been collected, the 3D process will be started automatically. If required, the cardholder will be redirected to the website or the banking app of the card issuer to complete a challenge. 

After the transaction has been completed, you can refer to the class `TransactionSuccess` that will return the details of the transaction. If the transaction failed, you will have to refer to the class `transactionError` for further details instead. You may also implement `TransactionDelegate` \(iOS\) and `TransactionListener` \(Android\) to be notified when a transaction is successfully finalized, encounters an error, or canceled by the user. 

#### Additional requirement for iOS

For the card scanner to work, a usage description for the camera use will be required in your .plist file. If you do not provide a description for the camera use, the app will crash when starting the card scanner.

{% code title=".plist File" %}
```markup
Key    :  Privacy - Camera Usage Description   
Value  :  $(PRODUCT_NAME) requires camera access to scan cards.
```
{% endcode %}

## Step 3: Obtain Tokens & 3D parameters

To obtain the tokens as well as the authentication result, you first need to submit the `transactionId` returned by the SDK to your server. 

Subsequently call the GET Status API from your **server** together with the `transactionId` to obtain a token for the card number and the cvv code. Additionally, the API returns a `3D` object which contains information about the result of the authentication process. 

{% api-method method="get" host="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}" %}
{% api-method-summary %}
Status API
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="transactionId" type="integer" required=true %}
transactionId obtained via `/v1/transactions`
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==  
see setup
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```java
{
    "transactionId": "190522141403888597",
    "type": "payment",
    "status": "authenticated",
    "currency": "EUR",
    "refno": "NIJ3OSelzyqp",
    "paymentMethod": "ECA",
    "detail": {
        "authorize": {
            "amount": 1000
        }
    },
    "history": [
        {
            "action": "init",
            "amount": 1000,
            "source": "api",
            "date": "2019-05-22T12:14:04.385+00:00",
            "success": true,
            "ip": "77.109.165.195"
        }
    ],
    "card": {
        "masked": "520000xxxxxx0080",
        "3D": {
            "eci": "02",
            "xid": "MDAxOTA1MjIxNDE0MDM4ODg1OTc=",
            "cavv": "OTkxOTA1MjIxNDE0MjMwMjg2Mjc=",
            "threeDSVersion": "1.0.2",
            "directoryResponse": "Y",
            "authenticationResponse": "Y"
        }
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Examples

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
  "transactionId": "190906151210861442",
  "type": "payment",
  "status": "authenticated",
  "currency": "EUR",
  "refno": "EVO-1564475113071",
  "paymentMethod": "ECA",
  "detail": {
    "authorize": {
      "amount": 1000
    }
  },
  "history": [
    {
      "action": "init",
      "amount": 1000,
      "source": "api",
      "date": "2019-09-06T13:12:11.915+00:00",
      "success": true,
      "ip": "77.109.165.195"
    },
    {
      "action": "authenticate",
      "amount": 1000,
      "source": "web",
      "date": "2019-09-06T13:12:21.915+00:00",
      "success": true,
      "ip": "77.109.165.195"
    }
  ],
  "card": {
    "masked": "520000xxxxxx0080",
    "expiryMonth": "12",
    "expiryYear": "21",
    "info": {
      "brand": "MCI CREDIT",
      "type": "credit",
      "usage": "consumer",
      "country": "MY",
      "issuer": "DATATRANS"
    },
    "3D": {
      "eci": "02",
      "xid": "MDAxOTA5MDYxNTEyMTA4NjE0NDI=",
      "cavv": "OTkxOTA5MDYxNTEyMjE3NTE0NjA=",
      "threeDSVersion": "1.0.2",
      "cavvAlgorithm": "1",
      "directoryResponse": "Y",
      "authenticationResponse": "Y",
      "cardHolderInfo": "Detailed issuer notification if available"
    }
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

