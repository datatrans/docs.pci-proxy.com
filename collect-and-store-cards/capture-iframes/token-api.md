# Token API

{% api-method method="get" host="https://api.sandbox.datatrans.com/upp/services" path="/v1/inline/token" %}
{% api-method-summary %}
Token
{% endapi-method-summary %}

{% api-method-description %}
This endpoint returns credit card number token and CVV token for transactionId.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==  
see Setup
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="transactionId" type="number" required=true %}
The transaction id obtained via the `Inline.submit()` operation.
{% endapi-method-parameter %}

{% api-method-parameter name="returnPaymentMethod" type="boolean" %}
Instructs the API to additionally return the paymentMethod used with this transaction.
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

{% hint style="info" %}
The service requires basic authentication. The password can be found in the [Web Admin Tool](https://admin.sandbox.datatrans.com/) under _UPP Administration &gt; Security &gt; Server-to-Server services security_.
{% endhint %}

### Examples

{% code-tabs %}
{% code-tabs-item title="Example: Basic usage" %}
```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170419151426624571" \ 
        -u 'merchantId:password'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```bash
{
  "aliasCC" : "424242SKMPRI4242",
  "aliasCVV" : "gOnsckLxRMO67W_Wz89RYFyW"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example: returnPaymentMethod=true returning paymentMethod" %}
```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170419151426624571&returnPaymentMethod=true" \
       -u 'merchantId:password'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```bash
{
    "aliasCC": "424242SKMPRI4242",
    "aliasCVV": "4F1zjRYITiW8JrqgNxE5o4cM",
    "paymentMethod": "VIS"
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Example: mandatoryAliasCVV=true w/ transactionId that has no CVV token" %}
```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170822090245534063&mandatoryAliasCVV=true" \
       -u 'merchantId:password'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response" %}
```bash
400 Bad Request
Tokenization with CVV not found
```
{% endcode-tabs-item %}
{% endcode-tabs %}



