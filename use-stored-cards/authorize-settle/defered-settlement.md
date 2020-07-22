# Defered settlement

The Settlement request is often also referred to as “Capture” or “Clearing”. It can be used for the settlement of previously authorized transactions. The `transactionId` is needed to settle an authorization. Note: This API call is not needed if `"autoSettle": true` was used when [authorizing a transaction](./).

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../../guides/pci-proxy-dashboard/api-authentication-data.md) for more information. 
{% endhint %}

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/v1/transactions/{transactionId}/settle" %}
{% api-method-summary %}
Defered settlement
{% endapi-method-summary %}

{% api-method-description %}
Settle a previously authorized transaction. Settled amount may not exceed initially authorized amount. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="transactionId" type="integer" required=true %}
The transactionId received after an authorization
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUklQ==
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="amount" type="integer" required=true %}
The amount of the transaction in the currency's smallest unit. For example use 1000 for EUR 10.00
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
3 letter ISO-4217 character code. E.g. `EUR` or `USD`
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
The merchants reference number. It should be unique for each transaction. 
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Transaction successfully settled
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid request
{% endapi-method-response-example-description %}

```bash
{
  "error": {
    "code": "see table below for detailed error messages",
    "message": "see table below for detailed error messages"
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

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

{% tab title="Response \(success\)" %}
```bash
204 Transaction successfully settled
```
{% endtab %}

{% tab title="Response \(error\)" %}
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

