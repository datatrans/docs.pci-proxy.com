# Authorize / Settle

Using this API allows you to simply send a json request with a token to just **authorize** (**reserve)** or **settle (charge)** an amount.&#x20;

### 1. Authorize

When you <mark style="color:blue;">**reserve**</mark> an amount on a stored card, the monthly allowance of the cardholder is reduced by the authorized amount, no matter whether the transaction will be settled later or not. The authorized amount is reserved for the merchant and should be settled within the period agreed with the acquirer. The issuer returns an authorization code that serves as the reference of the authorization. Once a transaction has been successfully authorized it can be settled. Important: the cardholder will not be charged without settlement. Authorization and settlement can also be processed in one single step. Please continue here with deferred settlement API if you just authorized the transaction.

### 2. Settle

When you <mark style="color:blue;">**charge**</mark> a stored card, the authorization and settlement will be processed in one single step. The settlement is often also referred to as “capture” or “clearing”. Once you sent a charge request, the authorized amount is reduced from the monthly allowance of the cardholder and will be automatically settled, which means that the cardholder will be actually charged.

{% hint style="info" %}
For both options, you need an existing acquiring contract and we will have to add this acquirer to your account. You can choose from our list of [Supported Acquirers](supported-acquirers.md) and contact us at [support@pci-proxy.com](mailto:support@pci-proxy.com).
{% endhint %}

{% hint style="info" %}
Stored tokens can be used multiple times for <mark style="color:blue;">**Recurring**</mark> or <mark style="color:blue;">**One-Click Payments**</mark>.&#x20;
{% endhint %}

### Authorize / Settle an amount

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../../resources/pci-proxy-dashboard/api-authentication-data.md) for more information.&#x20;
{% endhint %}

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/authorize" method="post" summary="AUTHORIZE Method" %}
{% swagger-description %}
The parameters marked with * are mandatory.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==

\


see Setup
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="true" %}
3 letter ISO-4217 character code. E.g. 

`EUR`

 or 

`USD`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refno" type="string" required="true" %}
Your unique reference number (AN 1..20)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" required="true" %}
The amount of the transaction in the currency's smallest unit. For example use 1000 for EUR 10.00. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="autoSettle" type="boolean" %}
Whether to automatically settle the transaction after an authorization or not. Default is 

`false`

. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card" type="object" required="true" %}
Card object must contain following parameters below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="alias" type="string" required="true" %}
Token received from a previous PCI Proxy integration
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryMonth" type="string" required="true" %}
The expiry month of the token (2 characters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" type="string" required="true" %}
The expiry year of the token (2 characters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="3D" type="object" %}
If 3D authentication data is available, the 3D object can be used to send the relevant 3D parameters. 
{% endswagger-parameter %}

{% swagger-response status="200" description="Successful authorization response" %}
```javascript
{
  "transactionId": "191023102544373504",
  "acquirerAuthorizationCode": "102544",
  "card": {
    "masked": "424242xxxxxx4242"
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description=" Failed authorization response
" %}
```bash
{
  "error": {
    "code": "see table below for detailed error messages",
    "message": "see table below for detailed error messages"
  },
  "transactionId": "191023112022175523"
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="warning" %}
In test mode, only [test credit cards](broken-reference) are allowed.
{% endhint %}

### Examples

{% tabs %}
{% tab title="Authorize" %}
{% code title="Request" %}
```bash
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions/authorize \
  -H 'Authorization: Basic MTAwMDAwMTExMTpwWUU4bFE2TlBiM2thRXpR' \
  -H 'Content-Type: application/json; charset=UTF-8' \
  -d '{
    "currency": "EUR",
    "refno": "vptJ07xyr",
    "amount": 1000,
    "card": {
        "alias": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
        "expiryMonth": "12",
        "expiryYear": "21"
    }
}
```
{% endcode %}

{% code title="Response (successful)" %}
```bash
{
  "transactionId": "191023111742635093",
  "acquirerAuthorizationCode": "111742",
  "card": {
    "masked": "490000xxxxxx0086"
  }
}
```
{% endcode %}
{% endtab %}

{% tab title="Authorize and Settle" %}
{% code title="Charge" %}
```bash
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions/authorize \
  -H 'Authorization: Basic MTAwMDAwMTExMTpwWUU4bFE2TlBiM2thRXpR' \
  -H 'Content-Type: application/json; charset=UTF-8' \
  -d '{
    "currency": "EUR",
    "refno": "vptJ07xyr",
    "amount": 1000,
    "autoSettle": "true",
    "card": {
        "alias": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
        "expiryMonth": "12",
        "expiryYear": "21"
    }
}
```
{% endcode %}

{% code title="Response (successful)" %}
```bash
{
  "transactionId": "191023113146339569",
  "acquirerAuthorizationCode": "113146",
  "card": {
    "masked": "424242xxxxxx4242"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Error Table

If the authorization failed, you receive one of the following error codes.&#x20;

> `"UNKNOWN_ERROR"`, `"UNRECOGNIZED_PROPERTY"`, `"INVALID_PROPERTY"`, `"INVALID_TRANSACTION_STATUS"`, `"TRANSACTION_NOT_FOUND"`, `"INVALID_JSON_PAYLOAD"`, `"UNAUTHORIZED"`, `"EXPIRED_CARD"`, `"INVALID_CARD"`, `"UNSUPPORTED_CARD"`, `"DUPLICATED_REFNO"`, `"DECLINED"`, `"BLOCKED_BY_VELOCITY_CHECKER"`, `"CLIENT_ERROR"` , `"SERVER_ERROR"`
