---
description: Keep your PCI Proxy token up to date
---

# Account Lifecycle management

In general, PCI Proxy ensures that your token is always up to date if a Network Token has been provisioned for the underlying card number. That means, you don't need to worry about declined authorisations due to expired card credentials anymore. We automatically update the PCI Proxy/Network Token if anything changes on the underlying card number. \
\
If you instead work with the PAN because your receiver does not support Network Tokens, you can still benefit out of the Network Tokenization solution. For example check if the expiry date has changed - simply call the Alias Status API to access the latest PAN expiry date.&#x20;

#### Alias Status API

{% swagger method="get" path="/v1/aliases/{alias}" baseUrl="https://api.sandbox.datatrans.com" summary="Alias status" %}
{% swagger-description %}
Check the expiry date and if a Network Taken has been created. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==


{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Content-Type" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="path" name="alias" required="true" %}
PCI Proxy alias
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Status successfully returned" %}
```json
{
    "alias": "7LHXscqwAAEAAAGEFDW3rEmNoLVdAAZE",
    "fingerprint": "F-fgxnFwN-gsIw7y80T-kpBB",
    "type": "CARD",
    "masked": "489537xxxxxx6287",
    "dateCreated": "2022-10-26T12:13:00Z",
    "card": {
        "expiryMonth": "02",
        "expiryYear": "23",
        "cardInfo": {
            "brand": "VISA",
            "type": "debit",
            "usage": "consumer",
            "country": "US",
            "issuer": "U.S. REGION"
        },
        "tokenInfo": {
            "expiryMonth": "02",
            "expiryYear": "23"
        }
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Invalid request" %}
```json
{
  "error": {
    "code": "ALIAS_NOT_FOUND"
  }
```
{% endswagger-response %}
{% endswagger %}

Furthermore, the response body will tell you if a Network Token has been provisioned successfully or not. To know that, check if the `tokenInfo` object is available in the response. If not, we were not able to create a Network Token as for instance the issuer does not yet support it or the card is not enrolled for it. In such cases, please continue with the PAN value mapped to the PCI Proxy token.&#x20;

{% hint style="info" %}
We are currently working on delivering enhanced Account lifecycle management features and Network Token related information. This includes returning the token status, card meta data as well as card art.\
\
Furthermore, we're also working on new notification APIs to trigger webhooks for specific events around Network Tokenisation.&#x20;
{% endhint %}

\
