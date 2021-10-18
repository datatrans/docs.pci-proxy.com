# Defered settlement

The Settlement request is often also referred to as “Capture” or “Clearing”. It can be used for the settlement of previously authorized transactions. The `transactionId` is needed to settle an authorization. Note: This API call is not needed if `"autoSettle": true` was used when [authorizing a transaction](./).

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information. 
{% endhint %}

{% swagger baseUrl="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}/settle" method="post" summary="Defered settlement" %}
{% swagger-description %}
Settle a previously authorized transaction. Settled amount may not exceed initially authorized amount. 
{% endswagger-description %}

{% swagger-parameter in="path" name="transactionId" type="integer" %}
The transactionId received after an authorization
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUklQ==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="integer" %}
The amount of the transaction in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" %}
3 letter ISO-4217 character code. E.g. 

`EUR `

or 

`USD`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="refno" type="string" %}
The merchants reference number. It should be unique for each transaction. 
{% endswagger-parameter %}

{% swagger-response status="204" description="Transaction successfully settled" %}
```
```
{% endswagger-response %}

{% swagger-response status="400" description="Invalid request" %}
```bash
{
  "error": {
    "code": "see table below for detailed error messages",
    "message": "see table below for detailed error messages"
  }
}
```
{% endswagger-response %}
{% endswagger %}

### Example

{% tabs %}
{% tab title="Request" %}
```bash
curl -X POST \
  https://api.sandbox.datatrans.com/v1/transactions/191023125905647521/settle \
  -H 'Authorization: Basic MTAwMDAwMTExMTpwWUU4bFE2TlBiM2thRXpR' \
  -H 'Content-Type: application/json; charset=UTF-8' \
  -d '{
    "amount": 1000,
    "currency": "EUR",
    "refno": "49raer8TC"
}'
```
{% endtab %}

{% tab title="Response (success)" %}
```bash
204 Transaction successfully settled
```
{% endtab %}

{% tab title="Response (error)" %}
```bash
{
  "error": {
    "code": "INVALID_PROPERTY",
    "message": "exceeded authorization amount"
  }
}
```
{% endtab %}
{% endtabs %}

### Error table

If the settlement failed, you receive one of the of the following error codes. 

> `"UNKNOWN_ERROR"`, `"UNRECOGNIZED_PROPERTY"`, `"INVALID_PROPERTY"`, `"INVALID_TRANSACTION_STATUS"`, `"TRANSACTION_NOT_FOUND"`, `"INVALID_JSON_PAYLOAD"`, `"UNAUTHORIZED"`, `"EXPIRED_CARD"`, `"INVALID_CARD"`, `"UNSUPPORTED_CARD"`, `"DUPLICATED_REFNO"`, `"DECLINED"`, `"BLOCKED_BY_VELOCITY_CHECKER"`, `"CLIENT_ERROR"` , `"SERVER_ERROR"`
