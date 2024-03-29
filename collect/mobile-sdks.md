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

| OS                                                                                                                                                                                                                        | Link                                                                                                                                                                                                                                                                                                                                                               | Supported version |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------- |
| <p><img src="https://www.datatrans.ch/media/filer_public/27/69/2769efa5-24be-49a5-adf1-449486ed10c7/apple-logo.svg" alt=""><br><img src="https://img.shields.io/github/v/tag/datatrans/ios-sdk?label=ios-sdk" alt=""></p> | <p>Release notes: <a href="https://github.com/datatrans/ios-sdk/releases/">Link</a><br>iOS SDK Reference: <a href="https://datatrans.github.io/ios-sdk/Classes/PCIPTokenization.html">Link</a><br>Integration Link (Github): <a href="https://github.com/datatrans/ios-sdk">Link</a></p><p></p>                                                                    | 11 +              |
| ![](https://www.datatrans.ch/media/filer\_public/7e/76/7e76be9b-dc33-4551-8911-180db284a7d4/android-logo.svg)![](https://img.shields.io/github/v/tag/datatrans/android-sdk?label=android-sdk)                             | <p>Release notes: <a href="https://github.com/datatrans/android-sdk/releases/">Link</a><br>Android SDK Reference: <a href="https://datatrans.github.io/android-sdk/-datatrans%20-android%20-s-d-k/ch.datatrans.payment.api.tokenization/index.html">Link</a><br>Integration Link (JFrog): <a href="https://datatrans.jfrog.io/artifactory/mobile-sdk">Link</a></p> | 5.0 +             |

## 2. Integration

As a next step, continue with the initialization of our iOS or Android SDK.

### iOS

For iOS, you can add the SDK to your project by adding a new Swift package dependency in Xcode and pointing to the github repository `datatrans.github.io/ios-sdk`. By default, enable all packages presented in the package selection. If you are building an App Clip project, you may select only your required packages, which will depend on your payment methods and flows. Please reach out to our support if you are unsure about what packages you required. Besides adding the packages via a Swift package dependency, you can also add the SDK via Cocoapods with `pod 'Datatrans'`.

#### Additional requirement for iOS

For the card scanner to work, a usage description for the camera use will be required in your `.plist` file. If you do not provide a description for the camera use, the app will crash when starting the card scanner.

{% code title=".plist File" %}
```markup
Key    :  Privacy - Camera Usage Description   
Value  :  $(PRODUCT_NAME) requires camera access to scan cards.
```
{% endcode %}

### Android

For Android projects, you can link the repo and dependencies as demonstrated here:

{% code title="Android implementation" %}
```java
repositories {
	...
	maven { url 'https://datatrans.jfrog.io/artifactory/mobile-sdk/' }
}

dependencies {
	...
	implementation 'ch.datatrans:android-sdk:2.3.0' // check release notes for latest version
}
```
{% endcode %}

If you are building an Instant app, you may exclude specific packages that are not required in your project. This will depend on your tokenisation process, however by default you should be able to exclude all components. Please reach out to our support if you are unsure about what packages you can exclude.

{% code title="Excluding Dependencies" %}
```java
dependencies {
	...
	implementation ('ch.datatrans:android-sdk:2.3.1') {  // Check release notes for latest version
		exclude group: 'io.card', module: 'android-sdk'
	}
}
```
{% endcode %}

The table below lists all the dependencies which can be excluded.

| Feature             | Group                     | Module                 |
| ------------------- | ------------------------- | ---------------------- |
| Credit Card Scanner | `io.card`                 | `android-sdk`          |
| Google Pay          | `com.google.android.gms`  | `play-services-wallet` |
| Samsung Pay         | `com.samsung.android.sdk` | `samsungpay`           |

## 3. SDK initialisation&#x20;

Create a tokenization object with your `merchantId` and `paymentMethodTypes` to start a tokenisation. Below is an example of the suggested minimum options to start a tokenisation with iOS (Swift) and Android (Kotlin, Java). Please read our detailed classes description for [iOS](https://datatrans.github.io/ios-sdk/Classes/PCIPTokenization.html) and [Android](https://datatrans.github.io/android-sdk/-datatrans%20-android%20-s-d-k/ch.datatrans.payment.api.tokenization/index.html) to discover more initialization options.

{% tabs %}
{% tab title="Swift" %}
```swift
let tokenizationRequest = PCIPTokenization(merchantId: merchantId, paymentMethodTypes: [.Visa, .MasterCard]) 
tokenizationRequest.delegate = self
tokenizationRequest.start(presentingController: navigationController)
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val tokenizationRequest = PCIPTokenization(merchantId, [VISA, MASTER_CARD])
tokenizationRequest.listener = this
TransactionRegistry.startTokenizationRequest(this, tokenizationRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
PCIPTokenizationRequest tokenizationRequest = new PCIPTokenization(merchantId, [VISA, MASTER_CARD]);
tokenizationRequest.setListener(this);
TransactionRegistry.INSTANCE.startTokenizationRequest(this, tokenizationRequest);
```
{% endtab %}
{% endtabs %}

After the tokenization has been completed, your `PCIPTokenizationDelegate` (iOS) or `PCIPTokenizationListener` (Android) is notified about the success, error or cancel state of the processed tokenization. The `tokenizationId` as well as additional card meta data are returned in `PCIPTokenizationSuccess` class.

{% hint style="info" %}
It is possible to only collect the CVV code of a card. Please check`init(merchantId:cvvOnlyCard:)` for iOS and `PCIPTokenization(merchantId: String, cvvOnlyCard: CvvOnlyCard)` for Android in the respective API reference to learn more.&#x20;
{% endhint %}

## 4. Obtain tokens

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
    "paymentMethod": "VIS",
    "alias": "7LHXscqwAAEAAAGCpe2M7PXWj2StAOG6",
    "fingerprint": "F-fgxnFwN-gsIw7y80T-kpBB",
    "maskedCard": "489537xxxxxx6287",
    "aliasCVV": "aYsIbb_KTQSbmWDrqlPp7hXM",
    "expiryYear": "23",
    "expiryMonth": "02",
    "cardInfo": {
        "brand": "VISA",
        "type": "debit",
        "usage": "consumer",
        "country": "US",
        "issuer": "U.S. REGION"
    }
}
```
{% endtab %}
{% endtabs %}

## Styling the Theme

You can style various colors in our Mobile SDKs to match your corporate identity. Check the graphic below to see what color properties can be defined. \
On iOS, you can define your preferred colors within the class `ThemeConfiguration`. On Android you can set theming options in your project’s color XML resource file, typically colors.xml. Use the color key names as defined in the table below.

![](../.gitbook/assets/colorslib.jpeg)

<table><thead><tr><th width="180">Property</th><th>Description</th><th width="219">Android</th><th>iOS</th></tr></thead><tbody><tr><td><strong>Background Color</strong>¹</td><td>Background color of the navigation bars. If this is not specified, the navigation bars will be transparent.</td><td><code>barBackgroundColor</code></td><td><code>dtpl_bar_background_color</code></td></tr><tr><td><strong>Bar Link Color</strong>²</td><td>Color of the buttons in the navigation bars. If this is not specified, the color will be the color set in Link Color.</td><td><code>barLinkColor</code></td><td><code>dtpl_bar_link_color</code></td></tr><tr><td><strong>Bar Title Color</strong>³</td><td>Color of the title within the navigation bars. If this is not specified, the color will be the text color. The text color is either white or black and cannot be customized.</td><td><code>barTitleColor</code></td><td><code>dtpl_bar_title_color</code></td></tr><tr><td><strong>Button Color</strong>⁴</td><td>Background color of large buttons, such as the Pay button. If this is not specified, the color will be the color set in Link Color.</td><td><code>buttonColor</code></td><td><code>dtpl_button_color</code></td></tr><tr><td><strong>Button Text Color</strong>⁵</td><td>Text color of large buttons, such as the Pay button. If this is not specified, the color will be set to white.</td><td><code>buttonTextColor</code></td><td><code>dtpl_button_text_color</code></td></tr><tr><td><strong>Link Color</strong>⁶</td><td>Color of text-only buttons or links and the text cursor. If this is not specified, the link color will be in a blue tone.</td><td><code>linkColor</code></td><td><code>dtpl_link_color</code></td></tr></tbody></table>

## Language Support

Our iOS and Android Mobile SDK integrations are currently translated and supported in the following languages:

* English `en`
* German `de`
* French `fr`
* Italian `it`

Please get in touch should you need an additional language to be added for your checkout or if you find a translation error.
