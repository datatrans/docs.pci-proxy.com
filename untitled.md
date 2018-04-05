# Untitled

{% api-method method="get" host="https://api.sandbox.datatrans.com/upp/services" path="/v1/inline/token" %}
{% api-method-summary %}
Get Token
{% endapi-method-summary %}

{% api-method-description %}
This endpoint returns credit card number token and CVV token for transactionId.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="returnPaymentMethod" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="transactionId" type="number" required=true %}
The transaction id obtained via the `Inline.submit()` operation.
{% endapi-method-parameter %}

{% api-method-parameter name="mandatoryAliasCVV" type="boolean" %}
Whether the cake should be gluten-free or not.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Tokens successfully retrieved.
{% endapi-method-response-example-description %}

```bash
{
  "aliasCC" : "424242SKMPRI4242",
  "aliasCVV" : "rBC5XHRRRKeq2gTfDTVP1rCA"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid transactionId used
{% endapi-method-response-example-description %}

```javascript
Tokenization not found
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid username:password
{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



