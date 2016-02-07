# Forward payment data to 3rd party provider

Once you collect and extract sensitive payment data to shield your server and minimize your PCI scope, you will most likely want to use the stored payment data to process, forward or retrieve payment data for several business cases.

PCI Proxy allows you to forward vaulted payment data to PCI compliant third parties. This can be any 3rd party that is PCI compliant them self (e.g. online travel agency, payment processor, hotel, airline, car rental, etc.).

### Set up a new third party receiver

Before you can forward payment data to PCI compliant third parties, we need the following information to approve and whitelist the new third party:

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