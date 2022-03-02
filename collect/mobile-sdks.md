# Mobile SDKs

Securely collect sensitive cardholder data such as the card number and the cvv code in your native iOS or Android app with our new mobile SDKs. Completely outsource your tokenisation processes to our libraries and benefit from a simple, fully PCI DSS compliant integration and features such as:&#x20;

* Smart, secure and state of the art UI components
* Card brand identification and input validation
* Card scanner
* Theme support: Style various items according to your CI
* Dark mode support&#x20;

{% hint style="warning" %}
This section covers the credit card number and cvv code tokenizations only. \
If you need to process 3D-Secure authentication within your SDKs please refer to our [SDK 3D integration](broken-reference).&#x20;
{% endhint %}

## 1. Distribution & Download

Access the latest version of our SDKs by following the links below and link the latest release to your app projects.

| OS      | Link                                                                                                                                                                                                                                                                  | Supported version |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| iOS     | <p>Github: <a href="https://github.com/datatrans/ios-sdk">Link</a></p><p>iOS SDK Reference: <a href="https://datatrans.github.io/ios-sdk/Classes/PCIPTokenizationRequest.html">Link</a></p>                                                                           | 11 +              |
| Android | <p>JFrog Repository: <a href="https://datatrans.jfrog.io/artifactory/mobile-sdk">Link</a></p><p>Android SDK Reference: <a href="https://datatrans.github.io/android-sdk/-datatrans%20-android%20-s-d-k/ch.datatrans.payment.api.tokenization/index.html">Link</a></p> | 5.0 +             |

## 2. Integration

As a next step, continue with the initialization of our iOS or Android SDK.

For iOS, you can add the SDK to your project by adding a new package dependency in Xcode or via Cocoapods with `pod 'Datatrans'`&#x20;

For Android projects, you can link the repo and dependencies as demonstrated here:

{% code title="Android implementation" %}
```java
repositories {
	...
	maven { url 'https://datatrans.jfrog.io/artifactory/mobile-sdk/' }
}

dependencies {
	...
	implementation 'ch.datatrans:android-sdk:1.4.2'
}
```
{% endcode %}

Create a tokenization object with your `merchantId` and `paymentMethodTypes` to start a tokenisation. Below is an example of the suggested minimum options to start a tokenisation with iOS (Swift) and Android (Kotlin, Java). Please read our detailed classes description for [iOS](https://datatrans.github.io/ios-sdk/Classes/PCIPTokenizationRequest.html) and [Android](https://datatrans.github.io/android-sdk/-datatrans%20-android%20-s-d-k/ch.datatrans.payment.api.tokenization/index.html) to discover more initialization options.

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

After the tokenization has been completed, `TokenizationRequestDelegate` will contain the `tokenizationId` and also tell you if a tokenization process was successful, cancelled, or resulted in an error.

#### Additional requirement for iOS

For the card scanner to work, a usage description for the camera use will be required in your `.plist` file. If you do not provide a description for the camera use, the app will crash when starting the card scanner.

{% code title=".plist File" %}
```markup
Key    :  Privacy - Camera Usage Description   
Value  :  $(PRODUCT_NAME) requires camera access to scan cards.
```
{% endcode %}

## 3. Obtain tokens

To obtain the tokenized values, you first need to submit the `tokenizationId` returned by the SDK to your server.&#x20;

Subsequently, call the GET Token API from your **server** together with the `tokenizationId` to obtain the tokens for the card number and the CVV code. Additionally, the API returns the expiry dates, the fingerprint of the card number as well as the `cardInfo` object.&#x20;

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/tokenizations/{tokenizationId}" method="post" summary="GET Token" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="path" name="tokenizationId" type="integer" required="true" %}
`tokenizationId`

 returned from the library
{% endswagger-parameter %}

{% swagger-parameter in="header" name="authorization" type="string" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```json
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
```
{% endswagger-response %}
{% endswagger %}

#### Examples&#x20;

{% tabs %}
{% tab title="Request" %}
```
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/tokenizations/210329160815401747' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json'
```
{% endtab %}

{% tab title="Response" %}
```json
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

You can style various colors in our Mobile SDKs to match your corporate identity. Check the graphic below to see what color properties can be defined. \
On iOS, you can define your preferred colors within the class `ThemeConfiguration`. On Android you can set theming options in your project’s color XML resource file, typically colors.xml. Use the color key names as defined in the table below.

![](../.gitbook/assets/colorslib.jpeg)

| Property               | Description                                                                                                                                                                  | Android              | iOS                         |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | --------------------------- |
| **Background Color**¹  | Background color of the navigation bars. If this is not specified, the navigation bars will be transparent.                                                                  | `barBackgroundColor` | `dtpl_bar_background_color` |
| **Bar Link Color**²    | Color of the buttons in the navigation bars. If this is not specified, the color will be the color set in Link Color.                                                        | `barLinkColor`       | `dtpl_bar_link_color`       |
| **Bar Title Color**³   | Color of the title within the navigation bars. If this is not specified, the color will be the text color. The text color is either white or black and cannot be customized. | `barTitleColor`      | `dtpl_bar_title_color`      |
| **Button Color**⁴      | Background color of large buttons, such as the Pay button. If this is not specified, the color will be the color set in Link Color.                                          | `buttonColor`        | `dtpl_button_color`         |
| **Button Text Color**⁵ | Text color of large buttons, such as the Pay button. If this is not specified, the color will be set to white.                                                               | `buttonTextColor`    | `dtpl_button_text_color`    |
| **Link Color**⁶        | Color of text-only buttons or links and the text cursor. If this is not specified, the link color will be in a blue tone.                                                    | `linkColor`          | `dtpl_link_color`           |

## Language Support

Our iOS and Android Mobile SDK integrations are currently translated and supported in the following languages:

* English `en`
* German `de`
* French `fr`
* Italian `it`

Please get in touch should you need an additional language to be added for your checkout or if you find a translation error.
