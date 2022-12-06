---
description: Read here how to reveal sensitive card data in native mobile applications
---

# Native mobile apps

### Process overview

Process description of how PCI Proxy Show API works for native mobile applications.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2022-08-24 at 11.13.03.png" alt=""><figcaption><p>Show process for native mobile applications</p></figcaption></figure>

1. The backend of your application receives a request to display card data
2. [Check](security-and-compliance.md) if the user is allowed to see plain text card data
3. Assemble the request with the card and/or cvv tokens mapped to the user and submit the request to PCI Proxy
4. PCI Proxy returns a `transactionId` to your backend. It is **valid for 30 minutes** and can be **consumed once**
5. Pass on the `transactionId` to your mobile application
6. Call the [Reveal](native-mobile-apps.md#reveal-api) endpoint with the `transactionId` in the body from the mobile application
7. The Reveal API returns plain text card number and CVV code to the mobile application

{% hint style="info" %}
TransactionIDs obtained via Show API allow access to sensitive data. Please do not store them anywhere unless absolutely necessary and consume them as soon as possible.
{% endhint %}

#### Endpoints

{% tabs %}
{% tab title="Sandbox" %}
[https://api.sandbox.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}

{% tab title="Production" %}
[https://api.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}
{% endtabs %}

#### Endpoints

{% tabs %}
{% tab title="Sandbox" %}
[https://api.sandbox.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}

{% tab title="Production" %}
[https://api.datatrans.com](https://api.sandbox.datatrans.com)
{% endtab %}
{% endtabs %}

### 1. Request access

Before you start with the technical integration, you need to request access to the feature. Log into our Dashboard and navigate to the Settings menu in Project settings.&#x20;

{% hint style="info" %}
If Show API access is already granted please continue with [step 2](native-mobile-apps.md#2.-obtain-a-transactionid)
{% endhint %}

![Request Show API access within the PCI Proxy Dashboard.](<../../.gitbook/assets/Request Show access.png>)

Click `Request access` in the `Request Show API access` section to open the form. Fill in your data and submit it. Our team will review your request and reach out to you once the access is granted or more information are needed.

### 2. Obtain a transactionId

Start with requesting a `transactionId` by calling the Show API from your server.&#x20;

{% swagger method="post" path="/v1/transactions/secureFields/show" baseUrl="https://api.sandbox.datatrans.com" summary="Init call" %}
{% swagger-description %}
Initial Server-to-Server call to retrieve transactionId which is required for step 3.&#x20;

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

To display the requested card data, call the following Reveal API directly from the native mobile app with the transactionId obtained in step 2. &#x20;

{% hint style="danger" %}
The Reveal API is only supported for native mobile apps. Make sure to not call it from web browsers.&#x20;
{% endhint %}

{% swagger method="post" path="/v1/transactions/secureFields/show/reveal" baseUrl="https://api.sandbox.datatrans.com" summary="Reveal API" %}
{% swagger-description %}
Call the Reveal endpoint from the native mobile app to receive plain card data
{% endswagger-description %}

{% swagger-parameter in="body" name="transactionId" required="true" %}
`transactionId`

 obtained in step 2
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" required="true" %}
API consumes application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Plain card data successfully returned" %}
```javascript
{
    // Response
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

#### Example Reveal call

{% tabs %}
{% tab title="Request" %}
```javascript
curl --location --request POST 'https://api.sandbox.datatrans.com/v1/transactions/secureFields/show/reveal' \
--header 'Content-Type: application/json' \
--data-raw '{
    "transactionId": "W0ZcW8zvzQ0DEISV0UafKeT8eFmC"
}'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "cardNumber": "4242424242424242",
    "cvv": "123"
}
```
{% endtab %}
{% endtabs %}

#### Alternative integration

You can as well embed the [iframes](web/) in a web view to your mobile application to show card data.&#x20;

##
