# Webservice API Reference

This API can be used to collect/extract credit cards via webservice \(XML/SOAP/JSON\) or to forward credit cards to receivers \(3rd parties\).

## Pull Request

The parameters will be sent as HTTP headers.

| **PCI Proxy PULL Endpoint:** |
| --- |
| [https://pilot.datatrans.biz/upp/proxy/pull/](https://pilot.datatrans.biz/upp/proxy/pull/) |

* **Mandatory input parameters:**

| HTTP header | Description | Example value |
| --- | --- | --- |
| `X-CC-URL` | Specifies the target URL that will be called | [https://api.receiver.com/](https://api.receiver.com/) |
| `X-CC-MERCHANT-ID` | Your merchant ID | 1000011011 |
| `X-CC-SIGN` | Configured security sign | 130709090849785405 |

* **Optional input paramter:**

| HTTP Header | Description | Example value |
| --- | --- | --- |
| `X-CC-TRUST-CERT` | If target URL server has invalid certificate, this parameter can be used to ignore the certificate. Useful for tests when implementing partners use self signed certificates on URLs simulating receivers. Header should be avoided \(not sent\) in production environments! | yes/no/true/false/on/off |
| `X-CC-ITEM` | Xpath expression pointing to “record” | /reservations/reservation |
| `X-CC-NUMBER` | XPath expression relative to “record” to locate card number | customer/cc\_number |

* **Example POST:**

```java
$ curl "https://pilot.datatrans.biz/upp/proxy/pull" 
        -X POST 
        -H "Content-Type: text/xml" 
        -H "X-CC-MERCHANT-ID: 1100005433" 
        -H "X-CC-URL: https://api.thirdparty.com/" 
        -H "X-CC-SIGN: 160203112421662698" 
        -d 'yourRequest.xml'
```

## Response

In turn, the proxy will return HTTP headers:

| HTTP Header | Description |
| --- | --- |
| `X-CC-ERROR-CODE` | Returned by the proxy in case of error only. See the error table below. |
| `X-CC-ERROR` | Returned by the proxy in case of error only. See the error table below. |
| `X-CC-MATCHES` | Returned by the proxy in case of success. The value represents the number of total \(card to alias / alias to card\) replacements that were made. |
| `X-CC-MATCHES-CA` | Returned number of card to alias replacements. |
| `X-CC-MATCHES-AC` | Returned number of alias to card replacements. |

### Special error case:

If the proxy is able to parse and correctly match the replacement targets, but an error occurs during the tokenization or detokenization, the match will be replaced with the following possible constants \(length  16\):

| Possible Constants | Error message \(X-CC-ERROR\) | Cause/explanation |
| --- | --- | --- |
| 0000000000000000 | Invalid card number | The card number was matched but was invalid. |
| 0000000000000001 | Internal error | The card number was matched, but internal error occurred during transformation to alias. |

For instance: If a channel response contains three card numbers and one of them fails to validate or convert, the two successful replacement tokens will be present in the returned document and the failed card number will be replaced with one of the two special constants above. No `X-CC-ERROR` or `X-CC-ERROR-CODE` headers will be returned and `X-CC-MATCHES` will have value “2”.

### Error Codes

Error cases \(returned with headers X-CC-ERROR-CODE and X-CC-ERROR\):

| Error code | Error message | Cause/explanation |
| --- | --- | --- |
| 1 | Missing header: `<HEADER-NAME>` | Missing required header in request. |
| 2 | Invalid merchantId | Merchant not found, disabled or not properly configured. Please contact Datatrans support. |
| 3 | Target host not allowed: `X-CC-URL` | The target URL is not allowed. Please contact Datatrans Support. |
| 4 | Invalid merchant setup - security sign was not defined | Merchant did not define the security sign. |
| 5 | Invalid sign | The provided `X-CC-SIGN` is wrong. |
| 6 | Invalid proxy type: `<PROXY_TYPE_NAME>` | The provided merchant/url headers did not match to a valid known proxy type. Please contact Datatrans Support. |
| 7 | Invalid XPath: `<X-CC-ITEM>` or `<X-CC-NUMBER>` | Invalid XPath expression in request. |
| 50 | Missing parameter: `<PARAMETER-NAME>` | PUSH request parameter missing. |
| 100 | Unsupported method: `<METHOD-NAME>` | Unsupported HTTP method |
| 200 | Could not apply xPath on xml response: `<XPATH-EXPRESSION>` | There was an error applying the xpath expression |
| 201 | Denied by velocity check | Sent during alias to card conversion \(if such case\) if there were too many attempts to convert bad aliases to cards. |
| 300 | Unknown content type in 3rd party response: `<CONTENT-TYPE>` | The proxy is not able to parse the 3rd party response as xml or html. |
| 301 | Unknown content type in source request: `<CONTENT-TYPE>` | Proxy cannot parse source response as xml or html. |
| 400 | Pull not configured | There is no pull configuration for the specified merchant. Please contact Datatrans Support. |
| 401 | Missing push configuration for: `<REASON>` | Wrong merchant configuration. Please contact Datatrans Support. |
| 800 | Connection error | Proxy could not connect to 3rd party / error that cause no response \(read timeout or DNS error\). Proxy returns HTTP status 504 \(Gateway Timeout\) and an empty response. |
| 900 | Proxy error | Uncategorized system error |



