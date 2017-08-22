#Token API

|Parameter||Description|
| :--- |
|`transactionId`|mandatory|The transaction id obtained via the `Inline.submit()` operation.|
|`returnPaymentMethod`|optional|Instructs the API to additionally return the `paymentMethod` used with this transaction.|
|`mandatoryAliasCVV`|optional|Triggers a behaviour that returns no tokens at all if a CVV was not entered.| 

###Examples

Basic usage example:

```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170419151426624571" \
       -u 'merchantId:password'
```
Response:
```json
{
  "aliasCC" : "424242SKMPRI4242",
  "aliasCVV" : "gOnsckLxRMO67W_Wz89RYFyW"
}
```

---

Example using `returnPaymentMethod=true` and obtaining `paymentMethod`:

```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170419151426624571&returnPaymentMethod=true" \
       -u 'merchantId:password'
```
Response:      
```json
{
    "aliasCC": "424242SKMPRI4242",
    "aliasCVV": "4F1zjRYITiW8JrqgNxE5o4cM",
    "paymentMethod": "VIS"
}
```
---
Example using `mandatoryAliasCVV=true` given a transactionId that has no CVV token available:

```bash
$ curl "https://api.sandbox.datatrans.com/upp/services/v1/inline/token?transactionId=170822090245534063&mandatoryAliasCVV=true" \
       -u 'merchantId:password'
```

Response:
```
400 Bad Request
Tokenization with CVV not found
```