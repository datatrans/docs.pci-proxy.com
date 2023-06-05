# Full API Reference

## PULL Request

The parameters will be sent as HTTP headers.

| PCI Proxy PULL Endpoint:              |
| ------------------------------------- |
| https://sandbox.pci-proxy.com/v1/pull |

* **Mandatory Input Parameters:**

| HTTP Header                      | Description                           | Example value                    |
| -------------------------------- | ------------------------------------- | -------------------------------- |
| `x-cc-merchant-id`               | Your unique merchant id at PCI Proxy  | 1000011011                       |
| `pci-proxy-api-key`              | Configured API key                    | MxdPtKaeDLfkhK7rdz4nmmx5dg10ufRR |
| `x-cc-url`                       | API endpoint                          | https://api.channel.com/         |

* **Example POST:**

```markup
curl https://sandbox.pci-proxy.com/v1/pull \
-H "Content-Type: text/xml" \
-H "pci-proxy-api-key: ynTIoCUuUnlHkbW460eZb0zr4WBL0ntg" \
-H "x-cc-merchant-id: 1000011011" \
-H "x-cc-url: https://pciproxy.mockable.io/secure-supply-xml-booking-com" \
-d '<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
      <request>
          <username>pci-proxy</username>
          <password>xGdk1Pco8</password>
          <hotel_id>181337</hotel_id>
          <id>731337</id>
      </request>'
```

## PULL Response

On the response, PCI Proxy will return these HTTP headers:

<table><thead><tr><th width="251">HTTP Header                                                              </th><th>Description</th></tr></thead><tbody><tr><td><code>x-cc-error-code</code></td><td>Returned by PCI Proxy in case of error only. See the error table below.</td></tr><tr><td><code>x-cc-error</code></td><td>Returned by PCI Proxy in case of error only. See the error table below.</td></tr><tr><td><code>x-cc-matches</code></td><td>Returned by PCI Proxy in case of success. The value represents the number of total (card to alias / alias to card) replacements that were made.</td></tr><tr><td><code>x-cc-matches-ca</code></td><td>The number of card to alias replacements.</td></tr><tr><td><code>x-cc-matches-ac</code></td><td>The number of alias to card replacements.</td></tr><tr><td><code>x-cvv-matches</code></td><td>The total number of cvv to alias and alias to cvv replacements. </td></tr><tr><td><code>x-cvv-matches-acvv</code></td><td>The number of alias to cvv replacements.</td></tr><tr><td><code>x-cvv-matches-cvva</code></td><td>The number of cvv to alias replacements.</td></tr><tr><td><code>x-custom-matches</code></td><td>Returned by PCI Proxy in case of a successful replacement. The value represents the number of total (custom value to alias/ alias to custom value) replacements that were made. </td></tr><tr><td><code>pci-proxy-masked-aliases</code></td><td>Contains the masked card alias format (411111ABCDEF1111).</td></tr><tr><td><code>x-cc-proxy-action-id</code></td><td>Unique request identifier.</td></tr></tbody></table>

### PUSH Request

PCI Proxy forwards the following HTTP headers to your endpoint:&#x20;

| HTTP Header                                                                                            | Description                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `x-cc-error-code`                                                                                      | Returned by PCI Proxy in case of error only. See the error table below.                                                                                                           |
| `x-cc-error`                                                                                           | Returned by PCI Proxy in case of error only. See the error table below.                                                                                                           |
| `x-cc-matches`                                                                                         | Returned by PCI Proxy in case of success. The value represents the number of total (card to alias / alias to card) replacements that were made.                                   |
| `x-cc-matches-ca`                                                                                      | The number of card to alias replacements.                                                                                                                                         |
| `x-cc-matches-ac`                                                                                      | The number of alias to card replacements.                                                                                                                                         |
| `x-cvv-matches`                                                                                        | The total number of cvv to alias and alias to cvv replacements.                                                                                                                   |
| `x-cvv-matches-acvv`                                                                                   | The number of alias to cvv replacements.                                                                                                                                          |
| `x-cvv-matches-cvva`                                                                                   | The number of cvv to alias replacements.                                                                                                                                          |
| `x-custom-matches`                                                                                     | Returned by PCI Proxy in case of a successful replacement. The value represents the number of total (custom value to alias / alias to custom value) replacements that were made.  |
| `pci-proxy-masked-aliases`                                                                             | Contains the masked card alias format (411111ABCDEF1111)                                                                                                                          |
| `x-cc-forwarded-for`                                                                                   | Returns the IP address of the origin caller of the Push integration.                                                                                                              |
| `x-cc-proxy-action-id`                                                                                 | Unique request identifier.                                                                                                                                                        |

### Special Error Cases

{% hint style="danger" %}
In case of XML requests/response bodies, the charset must be specified in the Content-type header, to be able to know it before actually reading the body. If not specified, PCI Proxy defaults to ISO-885901.
{% endhint %}

If PCI Proxy is able to parse and correctly match the replacement targets, but an error occurs during the tokenization or detokenization, the match will be replaced with the following possible constants (length 16):

| Possible Constants | (X-CC-ERROR)                             | Description                                                                                         |
| ------------------ | ---------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `0000000000000000` | Invalid card number                      | The card number/cvv was matched but was invalid.                                                    |
| `0000000000000001` | Internal error                           | The card number/cvv was matched, but an internal error occurred during the transformation to alias. |

For instance: If a channel response contains three card numbers and one of them fails to validate or convert, the two successful replacement tokens will be present in the returned body and the failed card number will be replaced with one of the two special constants above. No `X-CC-ERROR` or `X-CC-ERROR-CODE` headers will be returned and `X-CC-MATCHES` will have value “2”.

### Error Codes

Error cases (returned with the headers X-CC-ERROR-CODE and X-CC-ERROR):

<table><thead><tr><th width="150">Error code</th><th>Error message</th><th>Cause/explanation</th></tr></thead><tbody><tr><td><code>1</code></td><td>Missing header: <code>&#x3C;HEADER-NAME></code></td><td>One or more required headers are missing.</td></tr><tr><td><code>2</code></td><td>Invalid merchantId</td><td>Merchant not found, disabled or not properly configured. Please contact Datatrans support.</td></tr><tr><td><code>3</code></td><td>Target host not allowed: <code>X-CC-URL</code></td><td>The target URL is not allowed. Please contact Datatrans Support.</td></tr><tr><td><code>4</code></td><td>Invalid merchant setup - security sign was not defined</td><td>Merchant did not define the security sign.</td></tr><tr><td><code>5</code></td><td>Invalid authentication (api-key or sign)</td><td>Either <code>pci-proxy-api-key</code> or <code>sign</code> value is wrong. </td></tr><tr><td><code>9</code></td><td>Invalid proxy type: <code>&#x3C;PROXY_TYPE_NAME></code></td><td>The provided merchant/url headers did not match to a valid known proxy type. Please contact Datatrans Support.</td></tr><tr><td><code>50</code></td><td>Missing parameter: <code>&#x3C;PARAMETER-NAME></code></td><td>PUSH request parameter missing.</td></tr><tr><td><code>100</code></td><td>Unsupported method: <code>&#x3C;METHOD-NAME></code></td><td>Unsupported HTTP method</td></tr><tr><td><code>200</code></td><td>Could not apply xPath on xml response: <code>&#x3C;XPATH-EXPRESSION></code></td><td>There was an error applying the xpath expression</td></tr><tr><td><code>201</code></td><td>Denied by velocity check</td><td>Sent during alias to card conversion (if such case) if there were too many attempts to convert bad aliases to cards.  You can do 20 bad aliases requests in a 15 minutes window, afterwards the IP is blocked. As soon as you stop sending bad aliases, it takes a maximum of 15 minutes to get unblocked.</td></tr><tr><td><code>202</code></td><td>Denied by parallel connection checker</td><td>Security measure for too many parallel requests.</td></tr><tr><td><code>203</code></td><td>Denied by whitelist</td><td>The IP is not whitelisted on PCI Proxy. Please contact PCI Proxy Support.</td></tr><tr><td><code>300</code></td><td>Unknown content type in 3rd party response: <code>&#x3C;CONTENT-TYPE></code></td><td>The proxy is not able to parse the 3rd party response.</td></tr><tr><td><code>301</code></td><td>Unknown content type in source request: <code>&#x3C;CONTENT-TYPE></code></td><td>Proxy cannot parse the source request.</td></tr><tr><td><code>400</code></td><td>Pull not configured</td><td>There is no pull configuration for the specified merchant. Please contact Datatrans Support.</td></tr><tr><td><code>401</code></td><td>Missing push configuration for: <code>&#x3C;REASON></code></td><td>Wrong merchant configuration. Please contact Datatrans Support.</td></tr><tr><td><code>800</code></td><td>Connection error</td><td>Proxy could not connect to 3rd party / error that cause no response (read timeout or DNS error). Proxy returns HTTP status 504 (Gateway Timeout) and an empty response.</td></tr><tr><td><code>900</code></td><td>Proxy error</td><td>Uncategorized system error</td></tr></tbody></table>

## Status / Health Check

Please use the following endpoints for status/health checks. Please bear in mind that third-party systems are not included in this check. If our platform is operational we will return a status 200 and the string `ok`.

<table><thead><tr><th width="150"> </th><th>Sandbox</th><th>Production</th></tr></thead><tbody><tr><td>Filter/Forward APIs</td><td><a href="https://sandbox.pci-proxy.com/health">https://sandbox.pci-proxy.com/health</a></td><td><a href="https://api.pci-proxy.com/health">https://api.pci-proxy.com/health</a></td></tr><tr><td>Show API, Secure Fields</td><td><a href="https://pay.sandbox.datatrans.com/upp/jsonp-health-check?callback=foo">https://pay.sandbox.datatrans.com/upp/jsonp-health-check?callback=foo</a></td><td><a href="https://pay.datatrans.com/upp/jsonp-health-check?callback=foo">https://pay.datatrans.com/upp/jsonp-health-check?callback=foo</a></td></tr><tr><td>3D API</td><td><a href="https://api.sandbox.datatrans.com/upp/check">https://api.sandbox.datatrans.com/upp/check</a></td><td><a href="https://api.datatrans.com/upp/check">https://api.datatrans.com/upp/check</a></td></tr></tbody></table>

