# Forward payment data to 3rd party

Let us assume you send requests with sensitive payment data via API to a 3rd party.

PCI Proxy allows you to forward vaulted payment data to PCI compliant third parties (e.g. online travel agency, payment processor, hotel, airline, car rental, etc.). 

`By switching PCI Proxy between you and the 3rd party`, you invoke requests having PCI Proxy as endpoint. In your request, you simply use the token that you received when you collected the payment data. PCI Proxy replaces the token with payment data and forwards the record to the 3rd party. Any responses from the 3rd party are passed back to you. 

## How to start

Before you can forward payment data to a 3rd party, we need proof of PCI compliance of the 3rd party.

For testing purposes, it is not necessary to have the Attestation of Compliance for 3rd party ready.

**Consider a business that needs this ability:**

*You are a travel technology company and process reservations on behalf on your clients against global distribution systems.*


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