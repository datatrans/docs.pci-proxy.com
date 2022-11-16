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

| HTTP Header                                                               | Description                                                                                                                                                                      |
| ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `x-cc-error-code`                                                         | Returned by PCI Proxy in case of error only. See the error table below.                                                                                                          |
| `x-cc-error`                                                              | Returned by PCI Proxy in case of error only. See the error table below.                                                                                                          |
| `x-cc-matches`                                                            | Returned by PCI Proxy in case of success. The value represents the number of total (card to alias / alias to card) replacements that were made.                                  |
| `x-cc-matches-ca`                                                         | The number of card to alias replacements.                                                                                                                                        |
| `x-cc-matches-ac`                                                         | The number of alias to card replacements.                                                                                                                                        |
| `x-cvv-matches`                                                           | The total number of cvv to alias and alias to cvv replacements.                                                                                                                  |
| `x-cvv-matches-acvv`                                                      | The number of alias to cvv replacements.                                                                                                                                         |
| `x-cvv-matches-cvva`                                                      | The number of cvv to alias replacements.                                                                                                                                         |
| `x-custom-matches`                                                        | Returned by PCI Proxy in case of a successful replacement. The value represents the number of total (custom value to alias/ alias to custom value) replacements that were made.  |
| `pci-proxy-masked-aliases`                                                | Contains the masked card alias format (411111ABCDEF1111).                                                                                                                        |
| `x-cc-proxy-action-id`                                                    | Unique request identifier.                                                                                                                                                       |

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

| Error code | Error message                                                | Cause/explanation                                                                                                                                                       |
| ---------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `1`        | Missing header: `<HEADER-NAME>`                              | One or more required headers are missing.                                                                                                                               |
| `2`        | Invalid merchantId                                           | Merchant not found, disabled or not properly configured. Please contact Datatrans support.                                                                              |
| `3`        | Target host not allowed: `X-CC-URL`                          | The target URL is not allowed. Please contact Datatrans Support.                                                                                                        |
| `4`        | Invalid merchant setup - security sign was not defined       | Merchant did not define the security sign.                                                                                                                              |
| `5`        | Invalid authentication (api-key or sign)                     | Either `pci-proxy-api-key` or `sign` value is wrong.                                                                                                                    |
| `9`        | Invalid proxy type: `<PROXY_TYPE_NAME>`                      | The provided merchant/url headers did not match to a valid known proxy type. Please contact Datatrans Support.                                                          |
| `50`       | Missing parameter: `<PARAMETER-NAME>`                        | PUSH request parameter missing.                                                                                                                                         |
| `100`      | Unsupported method: `<METHOD-NAME>`                          | Unsupported HTTP method                                                                                                                                                 |
| `200`      | Could not apply xPath on xml response: `<XPATH-EXPRESSION>`  | There was an error applying the xpath expression                                                                                                                        |
| `201`      | Denied by velocity check                                     | Sent during alias to card conversion (if such case) if there were too many attempts to convert bad aliases to cards.                                                    |
| `202`      | Denied by parallel connection checker                        | Security measure for too many parallel requests.                                                                                                                        |
| `203`      | Denied by whitelist                                          | The IP is not whitelisted on PCI Proxy. Please contact PCI Proxy Support.                                                                                               |
| `300`      | Unknown content type in 3rd party response: `<CONTENT-TYPE>` | The proxy is not able to parse the 3rd party response.                                                                                                                  |
| `301`      | Unknown content type in source request: `<CONTENT-TYPE>`     | Proxy cannot parse the source request.                                                                                                                                  |
| `400`      | Pull not configured                                          | There is no pull configuration for the specified merchant. Please contact Datatrans Support.                                                                            |
| `401`      | Missing push configuration for: `<REASON>`                   | Wrong merchant configuration. Please contact Datatrans Support.                                                                                                         |
| `800`      | Connection error                                             | Proxy could not connect to 3rd party / error that cause no response (read timeout or DNS error). Proxy returns HTTP status 504 (Gateway Timeout) and an empty response. |
| `900`      | Proxy error                                                  | Uncategorized system error                                                                                                                                              |

## Status / Health Check

Please use the following endpoints for status/health checks. Please bear in mind that third-party systems are not included in this check. If our platform is operational we will return a status 200 and the string `ok`.

|                         | Sandbox                                                                                                                                        | Production                                                                                                                     |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Filter/Forward APIs     | [https://sandbox.pci-proxy.com/health](https://sandbox.pci-proxy.com/health)                                                                   | [https://api.pci-proxy.com/health](https://api.pci-proxy.com/health)                                                           |
| Show API, Secure Fields | [https://pay.sandbox.datatrans.com/upp/jsonp-health-check?callback=foo](https://pay.sandbox.datatrans.com/upp/jsonp-health-check?callback=foo) | [https://pay.datatrans.com/upp/jsonp-health-check?callback=foo](https://pay.datatrans.com/upp/jsonp-health-check?callback=foo) |
| 3D API                  | [https://api.sandbox.datatrans.com/upp/check](https://api.sandbox.datatrans.com/upp/check)                                                     | [https://api.datatrans.com/upp/check](https://api.datatrans.com/upp/check)                                                     |

