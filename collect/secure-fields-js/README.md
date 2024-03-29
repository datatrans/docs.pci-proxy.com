---
description: The only payment form you’ll ever need
---

# Secure Fields (JS)

Secure Fields allow you to securely collect credit, debit and virtual cards as well as bank account data by injecting iframes to your DOM. A separate iframe for all sensitive values is used. Thereby, the data never touches your server and allows you to capture all the other related payment data such as cardholder name, expiry date, etc. directly by yourself.

{% hint style="success" %}
**Using Secure Fields qualifies you for **<mark style="color:blue;">**SAQ A.**</mark>
{% endhint %}

| Browser                                       | Version      |
| --------------------------------------------- | ------------ |
| Chrome \| Chrome Mobile                       | >=28 \| >=28 |
| Firefox \| Firefox Mobile                     | >=31 \| >=31 |
| Internet Explorer \| Internet Explorer Mobile | >=9 \| >= 9  |
| Safari \| Safari Mobile                       | =6 \| >=6    |
| Opera \| Opera Mobile                         | >=24 \| >=22 |
| Blackberry Browser                            | =8           |
| Android Browser                               | >=4          |

## 1. Setup Secure Fields

To get started include the following script on your page.

{% tabs %}
{% tab title="Secure Fields Script" %}
```html
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js"></script>
```
{% endtab %}

{% tab title="Minified Version" %}
```html
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js"></script>
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js)
{% endhint %}

## 2. Create the **P**ayment Form

In order for Secure Fields to insert the card number and CVV iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:

* `card-number-placeholder`
* `cvv-placeholder`

For the bank account example they are:

* `iban-placeholder`
* `account-number-placeholder`
* `branch-number-placeholder`

{% tabs %}
{% tab title="Card Number / CVV" %}
```html
<form>
    <div>
        <div>
            <label for="card-number-placeholder">Card Number</label>
            <!-- card number container -->
            <div id="card-number-placeholder" style="width: 250px;"></div>
        </div>
        <div>
            <label for="cvv-placeholder">Cvv</label>
            <!-- cvv container -->
            <div id="cvv-placeholder" style="width: 90px;"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```
{% endtab %}

{% tab title="IBAN " %}
```html
<form>
    <div>
        <div>
            <label for="iban-placeholder">IBAN</label>
            <!-- IBAN container -->
            <div id="iban-placeholder" style="width: 250px;"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```
{% endtab %}

{% tab title="Account Number / Branch Code" %}
```html
<form>
    <div>
        <div>
            <label for="account-number-placeholder">account number</label>
            <!-- account number container -->
            <div id="account-number-placeholder" style="width: 90px;"></div>
        </div>
        <div>
            <label for="branch-code-placeholder">branch code</label>
            <!-- branch code container -->
            <div id="branch-code-placeholder" style="width: 90px;"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
In test mode, only [test credentials](../../resources/test-credentials.md) are allowed.
{% endhint %}

## 3. Retrieve a Transaction ID

Start with creating a new Secure Fields instance:

```javascript
var secureFields = new SecureFields();

// Multiple instances might be created and used independently:
// e.g. var secureFields2 = new SecureFields();
```

Initialize it with your `merchantId` and specify which DOM element containers should be used to inject the iframes:

{% tabs %}
{% tab title="Card number / CVV" %}
```javascript
secureFields.initTokenize( "1100007006", {
  cardNumber: "card-number-placeholder", 
  cvv: "cvv-placeholder"                
});
```
{% endtab %}

{% tab title="IBAN" %}
```javascript
secureFields.initTokenize( "1100007006", {
  iban: "iban-placeholder"               
});
```
{% endtab %}

{% tab title="Account number / Branch Code" %}
```javascript
secureFields.initTokenize( "1100007006", {
  accountNumber: "account-number-placeholder",
  branchCode: "branch-code-placeholder"               
});
```
{% endtab %}
{% endtabs %}

Afterwards, add **optional** `expm` and `expy`, submit the form and listen for the success event:

```javascript
$(function() {
  $("#go").click( function() {
      secureFields.submit({ // submit the "form"
        expm: 12,
        expy: 26
      });
   });
});

secureFields.on("success", function(data) {
  if(data.transactionId) {
    // transmit data.transactionId and the rest
    // of the form to your server    
  }
});
```

Instances can be destroyed if no longer used:

```
secureFields.destroy();
```

## 4. Obtain the tokens

Once you've transmitted the `transactionId` to your server (together with the the rest of your form) you have to execute a **server to server** `POST` request to retrieve the tokenized card or bank account values.

{% hint style="danger" %}
This service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../../resources/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information.
{% endhint %}

{% swagger method="post" path="v1/tokenizations/{transactionId}" baseUrl="https://api.sandbox.datatrans.com/" summary="Token" %}
{% swagger-description %}
This endpoint returns the tokenized card or bank account data corresponding to the `transactionId.`

Pease note that this is a **server to server** API call and cannot be called from the browser directly.
{% endswagger-description %}

{% swagger-parameter in="query" name="transactionId" required="true" %}
The transactionId obtained via the

`secureFields.submit()`

operation.
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-type" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Idempotency-Key" %}
Unique UUID v4 Idempotency-Key
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
  "aliasCC": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
  "aliasCVV": "mVHJkLRrRX-vb9uUzEM40RUN",
  "maskedCard": "424242xxxxxx4242"
}
```
{% endswagger-response %}
{% endswagger %}

### Token API Examples

{% tabs %}
{% tab title="Request" %}
```
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/tokenizations/220112095131012129' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json' \
-H 'Idempotency-Key: e75d621b-0e56-4b71-b889-1acec3e9d870'
```
{% endtab %}

{% tab title="Response Card" %}
```json
{
    "paymentMethod": "VIS",
    "alias": "7LHXscqwAAEAAAGCq4LyxV20zPAFABWx",
    "fingerprint": "F-dV5V8dE0SZLoTurWbq2HZp",
    "maskedCard": "424242xxxxxx4242",
    "aliasCVV": "ISlRs6QoSOyzdFl8t-hiW_-4",
    "expiryYear": "25",
    "expiryMonth": "06",
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

{% tab title="Response IBAN" %}
```json
{
    "aliasIban": "AAABeKaD2UbssdexyrAAAUN24QvOZg3n",
    "maskedIban": "DE85xxxxxxxxxxxxxx2345"
}
```
{% endtab %}

{% tab title="Response Account number & Branch code" %}
```json
{
    "aliasAccountNumber": "AAABeKahwGDssdexyrAAAV8w_R0dlq9b",
    "maskedAccountNumber": "xxxx0604",
    "aliasBranchCode": "AAABeKahwGDssdexyrAAAadGCQEwl6MZ"
}
```
{% endtab %}
{% endtabs %}

### Error table&#x20;

| Error message            | Cause / Explanation                                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| `Tokenization expired`   | The `transactionId` has expired. Please note that it is valid for 30 minutes only                                |
| `Tokenization not found` | The merchant id used for the transaction id creation does not match the merchant id used for the GET Token call. |

## Examples

Please visit our GitHub [repository](https://github.com/datatrans/secure-fields-sample) for additional examples of integration versions: \
\
Demo Basic: [https://datatrans.github.io/secure-fields-sample/](https://datatrans.github.io/secure-fields-sample/index.html)\
Demo with horizontal fields: [https://datatrans.github.io/secure-fields-sample/pciproxy-examples/inline-example.html](https://datatrans.github.io/secure-fields-sample/pciproxy-examples/inline-example.html)\
Demo with floating labels: [https://datatrans.github.io/secure-fields-sample/pciproxy-examples/floating-label.html](https://datatrans.github.io/secure-fields-sample/pciproxy-examples/floating-label.html)

An example of how to implement this behaviour in modern web applications can be found [here](https://github.com/datatrans/secure-fields-sample/tree/master/react-example-initTokenize)

{% hint style="warning" %}
In test mode, only [test credentials](broken-reference) are allowed.
{% endhint %}

Please also have a look at [Styling](initialization-and-styling.md) and [Events](events.md) references.
