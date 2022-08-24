---
description: Read here how to reveal sensitive card data in web applications
---

# Web

### Process overview

Process description of how PCI Proxy Show API works in web applications.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2022-08-24 at 11.01.59.png" alt=""><figcaption><p>Show process for web applications</p></figcaption></figure>

1. The backend of your application receives a request to display card data
2. [Check](../security-and-compliance.md) if the user is allowed to see plain text card data
3. Assemble the request with the card and/or cvv tokens mapped to the user and submit the request to PCI Proxy
4. PCI Proxy returns a `transactionId` to your backend, **valid for 30 minutes** and can be **consumed once**
5. Pass on the `transactionId` to your web application
6. Load and render SecureFields.js into your HTML
7. The JavaScript's `SecureFields.init(transactionId)` operation requests the card data
8. Card data and buttons will be injected into the HTML and can be displayed to the user

{% hint style="info" %}
TransactionIDs obtained via Show API allow access to sensitive data. Please do not store them anywhere unless absolutely necessary and consume them as soon as possible.
{% endhint %}

### 1. Request access

Before you start with the technical integration, you need to request access to the feature. Log into our Dashboard and navigate to the Settings menu in Project settings.&#x20;

![Request Show API access within the PCI Proxy Dashboard.](<../../../.gitbook/assets/Request Show access.png>)

Click `Request access` in the `Request Show API access` section to open the form. Fill in your data and submit it. Our team will review your request and reach out to you once the access is granted or more information are needed.

### 2. Obtain a transactionId

Start with requesting a `transactionId` by calling the Show API from your server.&#x20;

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
--header 'Authorization: Basic {basicAuth}'
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

#### 3.1 Set up SecureFields.js

To get started include the following script on your page.&#x20;

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
Please make sure to always load it directly from [https://pay.sandbox.datatrans.com](https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-2.0.0.js) for Sandbox and [https://pay.datatrans.com ](https://pay.datatrans.com)for Production environment.&#x20;
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

#### 3.3 Initialize Secure Fields using a transactionId

Create a new Secure Fields instance:

```java
var secureFields = new SecureFields();

// Multiple instances might be created and used independently:
// e.g. var secureFields2 = new SecureFields();
```

Initialize it with a `transactionId` you obtained during [step 2](./#2.-obtain-a-transactionid) and specify which DOM element containers should be used to inject the iframes:

```java
secureFields.init(
  transactionId,
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

Or visit the GitHub repo directly [here](https://github.com/datatrans/secure-fields-sample/blob/master/pciproxy-examples/show.html)

##
