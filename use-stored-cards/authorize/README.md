# Authorize/Settle

Using this API allows you to simply send a json request with a token to just **reserve** \(authorize\) or **charge** \(settle\) an amount. 

{% tabs %}
{% tab title="Reserve an amount" %}
When you [**reserve an amount**](./#examples) on a stored card, the monthly allowance of the cardholder is reduced by the authorised amount, no matter whether the transaction will be settled later or not. The authorised amount is reserved for the merchant and should be settled within the period agreed with the acquirer. The issuer returns an authorisation code which serves as the reference of the authorisation. Once a transaction has been successfully authorised it can be settled.

**Important:** the cardholder will not be charged without settlement. Authorisation and settlement can also be processed in one single step. Please continue [here ](defered-settlement.md)with deferred settlement API if you just authorized the transaction.
{% endtab %}

{% tab title="Charge cardholder" %}
When you [**charge a stored card**](./#examples), the authorization and settlement will be processed in one single step. The settlement is often also referred to as “capture” or “clearing”. Once you sent a charge request, the authorized amount is reduced from the monthly allowance of the cardholder and will be automatically settled, which means that the cardholder will be actually charged.
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Stored cards can be used multiple times for **recurring transactions** or **One-Click payments**. 
{% endhint %}

## 1. Add acquirer to your account

{% hint style="warning" %}
For this feature, you need an existing acquiring contract.
{% endhint %}

| You can choose from a list of [**Supported Acquirer**](../../resources/supported-acquirer.md) and contact us at [setup@pci-proxy.com](mailto:setup@pci-proxy.com) |  |
| :--- | :--- |


## 2. Authorize a stored card

{% hint style="warning" %}
The service requires HTTP Basic Authentication.  Provide your `merchantId` as the basic authentication username value. The password can be found in the [Web Admin Tool](https://admin.sandbox.datatrans.com/) under _UPP Administration &gt; Security &gt; Server-to-Server services security_.
{% endhint %}

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions/authorize" %}
{% api-method-summary %}
AUTH method
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==  
see Setup
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character code. E.g. `EUR` or `USD`
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
Your unique reference number \(AN 1..20\)
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="integer" required=true %}
The amount of the transaction in the currency's smallest unit. For example use 1000 for EUR 10.00. 
{% endapi-method-parameter %}

{% api-method-parameter name="autoSettle" type="boolean" required=false %}
Wheter to automatically settle the transaction after an authorization or not. Default is `false`. 
{% endapi-method-parameter %}

{% api-method-parameter name="card" type="object" required=true %}
Card object must contain following parameters below
{% endapi-method-parameter %}

{% api-method-parameter name="alias" type="string" required=true %}
Token received from a previous PCI Proxy integration
{% endapi-method-parameter %}

{% api-method-parameter name="expiryMonth" type="string" required=true %}
The expiry month of the token \(2 characters\)
{% endapi-method-parameter %}

{% api-method-parameter name="expiryYear" type="string" required=true %}
The expiry year of the token \(2 characters\)
{% endapi-method-parameter %}

{% api-method-parameter name="3D" type="object" required=false %}
If 3D authentication data is available, the 3D object can be used to send the relevant 3D paramters. 
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Successful authorization response
{% endapi-method-response-example-description %}

```javascript
{
  "transactionId": "191023102544373504",
  "acquirerAuthorizationCode": "102544",
  "card": {
    "masked": "424242xxxxxx4242"
  }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
 Failed authorization response  
{% endapi-method-response-example-description %}

```bash
{
  "error": {
    "code": "see table below for detailed error messages",
    "message": "see table below for detailed error messages"
  },
  "transactionId": "191023112022175523"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

### Examples

{% tabs %}
{% tab title="Reserve amount \(authorize\)" %}
{% code-tabs %}
{% code-tabs-item title="Request" %}
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
        "alias": "424242SKMPRI4242",
        "expiryMonth": "12",
        "expiryYear": "21"
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(successful\)" %}
```bash
{
  "transactionId": "191023111742635093",
  "acquirerAuthorizationCode": "111742",
  "card": {
    "masked": "490000xxxxxx0086"
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}

{% tab title="Charge amount \(auth+settle\)" %}
{% code-tabs %}
{% code-tabs-item title="Charge" %}
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
        "alias": "424242SKMPRI4242",
        "expiryMonth": "12",
        "expiryYear": "21"
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(successful\)" %}
```bash
{
  "transactionId": "191023113146339569",
  "acquirerAuthorizationCode": "113146",
  "card": {
    "masked": "424242xxxxxx4242"
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}
{% endtabs %}

### Error table

If the authorisation failed, you receive one of the of the following error codes. 

> `"UNKNOWN_ERROR"`, `"UNRECOGNIZED_PROPERTY"`, `"INVALID_PROPERTY"`, `"INVALID_TRANSACTION_STATUS"`, `"TRANSACTION_NOT_FOUND"`, `"INVALID_JSON_PAYLOAD"`, `"UNAUTHORIZED"`, `"EXPIRED_CARD"`, `"INVALID_CARD"`, `"UNSUPPORTED_CARD"`, `"DUPLICATED_REFNO"`, `"DECLINED"`, `"BLOCKED_BY_VELOCITY_CHECKER"`, `"CLIENT_ERROR"` , `"SERVER_ERROR"`

#### 



