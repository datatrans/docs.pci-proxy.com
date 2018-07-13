# Forward

PCI Proxy allows you to retain your existing data communication with PCI-compliant Receiver. This can be online travel agencies, payment gateways, hotels, airlines, car rentals, etc.

Simply redirect requests containing tokens through PCI Proxy to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for tokens and replaces located tokens with sensitive card data and forwards the populated request to the PCI-compliant Receiver. The message structure of your request always remains the same. Any responses from the Receiver are passed back to you and sensitive card data is tokenized if needed.

PCI Proxy supports various communication methods to forward sensitive card data to a Receiver:

{% page-ref page="https.md" %}

{% page-ref page="sftp.md" %}

{% hint style="success" %}
**Your requests are populated with sensitive card data after they leave your systems to keep you out of PCI scope.**

Using Receivers not listed on [supported Receivers \(Gateways\)](../../resources/supported-receivers.md) requires a valid AOC \(Attestation of Compliance\) and either a letter of Acknowledgment or an extract of the terms and conditions which proves the PCI DSS compliance of the Receiver. 
{% endhint %}



