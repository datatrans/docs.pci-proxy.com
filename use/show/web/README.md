---
description: Read here how to reveal sensitive cardholder data in web applications
---

# Web

### Process overview

Process description of how PCI Proxy Show API works

![Show process](<../../../.gitbook/assets/Show process.png>)

1. The backend of your application receives a request to display card data
2. Check if the cardholder is allowed to see plain text card data
3. Assemble the request with the card or cvv tokens mapped to the cardholder and submit the request to PCI Proxy
4. PCI Proxy returns a `transactionId` which is **valid for 30 minutes** and can be **consumed one time** to your backend
5. Pass on the `transactionId` to your web application
6. Load and render the SecureFields.js into your HTML
7. Inject the SecureFields.js with the `transactionId`
8. The JavaScript's `SecureFields.init` operation requests the card data
9. Card data and buttons will be injected into the HTML and can be displayed to the user

{% hint style="info" %}
TransactionId's obtained via Show API allow access to sensitive data. Please do not store them anywhere unless absolutely necessary and consume them as soon as possible.&#x20;
{% endhint %}

### 1. Request access

Before you start with the technical integration, please make sure to request access to the feature. Login to our Dashboard and navigate to the Settings menu in the Project settings.&#x20;

![Request Show API access within the PCI Proxy Dashboard.](<../../../.gitbook/assets/Request Show access.png>)

Open the form `Request Show API access` , complete the fields and submit it. Our team will review your request and reach out to you once the access is granted or more information are needed.&#x20;

{% hint style="info" %}
Please note that you need request access for both environments, Sandbox and Production separately.&#x20;
{% endhint %}

### 2. Obtain a transactionId

Start with requesting a `transactionId` by calling the Show API.

{% swagger method="post" path="/v1/transactions/secureFields/show" baseUrl="https://api.sandbox.datatrans.com" summary="Init call" %}
{% swagger-description %}
Initial Server-to-Server call to retrieve transactionId which is needed to initiate the SecureFields.js in step 4

The parameters marked with \* are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" required="true" name="Authorization" %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==

see API Authentication data
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Content-Type" %}
API consumes application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="alias" required="false" %}
PCI Proxy credit card number token
{% endswagger-parameter %}

{% swagger-parameter in="body" name="aliasCVV" %}
PCI Proxy CVV token
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="transactionId successfully created" %}
```json
{
    "transactionId": "-ccRvWgLEVwDECfBSCvww2EhsTnc"
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Something went wrong" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

#### Example init call

{% tabs %}
{% tab title="Request" %}
```javascript
curl --location --request POST 'https://api.sandbox.datatrans.com/v1/transactions/secureFields/show'
--header 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr'
--header 'Content-Type: application/json'
--data-raw 
'{ 
    "alias": "rN5IABEiAAEAAAGB8QcMWHYu8SeGACOZ", 
    "aliasCVV": "qOr2SX3sQm2e8SazhFNssOkJ" 
}'

```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "transactionId": "pY8Pt-lWIpkDECioNQVFJvNifCeM"
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Consider sending only `alias` or `aliasCVV`, depending on whether you intend to reveal just one of these values at a time.
{% endhint %}

### 3. Frontend integration

Integrate Secure Fields in your frontend application where the card data should be displayed.&#x20;

#### 3.1 Setup SecureFields.js

To get started include the following script on your page. Make sure to use the latest version.&#x20;

{% tabs %}
{% tab title="Secure Fields Script" %}
```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js"></script>
```
{% endtab %}

{% tab title="Minified version" %}
```javascript
<script src="https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.min.js"></script>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js)
{% endhint %}

#### 3.2 Create the Show form and optional copy-to-clipboard buttons

In order for Secure Fields to insert the card number and CVV iframes at the right place, create empty DOM elements and assign them unique IDs. In the example below those are:

* `card-number-placeholder`
* `cvv-placeholder`
* `copy-card-number`
* `copy-cvv`

{% tabs %}
{% tab title="Card Number / CVV / Copy buttons" %}
```html
<form>
    <div>
        <div>
            <label for="card-number-placeholder">Card Number</label>
            <!-- card number container -->
            <div id="card-number-placeholder" style="width: 250px; height: 20px;"></div>
            <!-- card number copy-to-clipboard -->
            <div id="copy-card-number" style="width: 50px; height: 20px"></div>
        </div>
        <div>
            <label for="cvv-placeholder">Cvv</label>
            <!-- cvv container -->
            <div id="cvv-placeholder" style="width: 90px; height: 20px"></div>
            <!-- cvv copy-to-clipboard -->
            <div id="copy-cvv" style="width: 50px; height: 20px"></div>
        </div>

        <button type="button" id="go">Get Token!</button>
    </div>
</form>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Copying the card data to the clipboard might increase the risk of any abuse for the cardholder. It's more secure when left in the iframes.&#x20;
{% endhint %}

#### 3.3 Initialize Secure Fields using a transactionId

Create a new Secure Fields instance:

```java
var secureFields = new SecureFields();

// Multiple instances might be created and used independently:
// e.g. var secureFields2 = new SecureFields();
```

Initialize it with a `transactionId` you obtained during [step 2](./#2.-initializing-transactionid) and specify which DOM element containers should be used to inject the iframes:

```java
secureFields.init(
  'pY8Pt-lWIpkDECioNQVFJvNifCeM',
  {
    cardNumber: {
       placeholderElementId: 'card-number-placeholder',
       inputType: 'tel'
    },
    cvv:  {
       placeholderElementId: 'cvv-placeholder',
       inputType: 'tel'
    },
    // optionally render buttons with copy-to-clipboard functionality
    copyToClipboard: {
      cardNumber: {
        placeholderElementId: 'copy-card-number',
        label: 'Copy'
      },
      cvv: {
        placeholderElementId: 'copy-cvv',
        label: 'Copy'
      }
    }
  }
);
```

### Example

An example implementation can be found here: [https://datatrans.github.io/secure-fields-sample/pciproxy-examples/show.html](https://datatrans.github.io/secure-fields-sample/pciproxy-examples/show.html)

##
