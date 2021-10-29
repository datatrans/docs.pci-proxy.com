# Authorize/Settle

Using this API allows you to simply send a json request with a token to just **reserve **(authorize) or **charge **(settle) an amount.

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

| You can choose from a list of [**Supported Acquirer**](../../resources/supported-acquirer.md) and contact us at [support@pci-proxy.com](mailto:support@pci-proxy.com) |   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | - |

## 2. Authorize a stored card

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information.
{% endhint %}

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/authorize" method="post" summary="AUTHORIZE method" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" required="false" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==

\\

see Setup
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="false" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="false" %}
3 letter ISO-4217 character code. E.g.

`EUR`

or

`USD`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refno" type="string" required="false" %}
Your unique reference number (AN 1..20)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" required="false" %}
The amount of the transaction in the currency's smallest unit. For example use 1000 for EUR 10.00.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="autoSettle" type="boolean" required="false" %}
Whether to automatically settle the transaction after an authorization or not. Default is

`false`

.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="card" type="object" required="false" %}
Card object must contain following parameters below
{% endswagger-parameter %}

{% swagger-parameter in="body" name="alias" type="string" required="false" %}
Token received from a previous PCI Proxy integration
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryMonth" type="string" required="false" %}
The expiry month of the token (2 characters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="expiryYear" type="string" required="false" %}
The expiry year of the token (2 characters)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="3D" type="object" required="false" %}
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
{% endswagger %}

{% hint style="warning" %}
In test mode, only [test credit cards](../../test-card-data.md) are allowed.
{% endhint %}

### Examples

{% tabs %}
{% tab title="Reserve amount (authorize)" %}
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
```json
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

{% tab title="Charge amount (auth+settle)" %}
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
```json
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

### Error table

If the authorisation failed, you receive one of the of the following error codes.

> `"UNKNOWN_ERROR"`, `"UNRECOGNIZED_PROPERTY"`, `"INVALID_PROPERTY"`, `"INVALID_TRANSACTION_STATUS"`, `"TRANSACTION_NOT_FOUND"`, `"INVALID_JSON_PAYLOAD"`, `"UNAUTHORIZED"`, `"EXPIRED_CARD"`, `"INVALID_CARD"`, `"UNSUPPORTED_CARD"`, `"DUPLICATED_REFNO"`, `"DECLINED"`, `"BLOCKED_BY_VELOCITY_CHECKER"`, `"CLIENT_ERROR"` , `"SERVER_ERROR"`

####
