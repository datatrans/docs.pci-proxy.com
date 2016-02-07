# Forward payment data to 3rd party

Let us assume you send requests with sensitive payment data via API to a 3rd party.

PCI Proxy allows you to forward vaulted payment data to PCI compliant third parties (e.g. online travel agency, payment processor, hotel, airline, car rental, etc.). 

`By switching PCI Proxy between you and the 3rd party`, you invoke requests having PCI Proxy as endpoint. In your request, you simply use the token that you received when you collected the payment data. PCI Proxy replaces the token with payment data and forwards the record to the 3rd party. Any responses from the 3rd party are passed back to you. 

## How to start

Before you can forward payment data to a 3rd party, we need proof of PCI compliance of the 3rd party.

For testing purposes, it is not necessary to have the Attestation of Compliance for 3rd party ready.

**Consider a business that needs this ability:**

*You are a travel technology company and process reservations on behalf on your clients against global distribution systems.*

#### Quick Start Guide:

1. Add a pull channel to your account
2. POST your XML/SOAP request having PCI Proxy as endpoint.
2. Add HTTP header to your request.


| Test PCI Proxy PULL Endpoint: |
| -- |
| https://pilot.datatrans.biz/upp/proxy/pull/|

- Required HTTP header:


| HTTP Header      | Description                                                        | Example value
| -------------- | -------------------------------------------------------------------| ---
| `X-CC-URL` | Specifies the target (channel) URL that will be called | https://api.partner.com/
| `X-CC-MERCHANT-ID` | Your merchant ID | 1000011011
| `X-CC-SIGN` | Configured security sign | 130709090849785405
            

```java
    $ curl "https://pilot.datatrans.biz/upp/proxy/pull" 
        -X POST 
        -H "Content-Type: text/xml" 
        -H "X-CC-MERCHANT-ID: 1100005433" 
        -H "X-CC-URL: https://api.partner.com/" 
        -H "X-CC-SIGN: 160203112421662698" 
        -d 'yourRequest.xml'
```

> Note: In test mode, only test credit cards are allowed. For testing purposes, you will need our [test credit cards](https://www.datatrans.ch/showcase/test-cc-numbers). Learn more about [live mode and testing](live_mode-test.html).



| General Information                                                               |
| --------------------------------------------------------------------------------- |
| Merchant ID - Once you [register an account][3] you receive your merchant ID. |
| Company name and website of third party                                           |
| AOC document of third party as proof of PCI compliance                            |

| Technical Details         | Description                                                                 |
| ------------------------- | --------------------------------------------------------------------------- |
| Target URL                | The URL where we should forward the populated request to (3rd party).       |
| Sample Request & Response | Please include API name, required headers, auth fields, and request method. |
| IP Address                | IP address of your server                                                   |

Please send this information to setup@datatrans.ch.