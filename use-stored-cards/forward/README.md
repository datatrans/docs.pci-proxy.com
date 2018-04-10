---
description: Share stored card data with your partners or payment gateways.
---

# Forward

PCI Proxy allows you to retain your existing data communication with PCI-compliant Receiver. This can be online travel agencies, payment gateways, hotels, airlines, car rentals, etc.

Simply `redirect requests containing tokens through PCI Proxy` to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for tokens and replaces located tokens with sensitive card data and forwards the populated request to the PCI-compliant Receiver. The message structure of your request always remains the same. Any responses from the Receiver are passed back to you and sensitive card data is tokenized if needed.

PCI Proxy provides you two different ways forwarding data to a Receiver.

1. [Forward data by using our PULL or PUSH API](https://docs.pci-proxy.com/forward-receiver/api.html)
2. [Forward data to a SFTP server](https://docs.pci-proxy.com/forward-receiver/sftp.html)

{% hint style="warning" %}
**Your requests are populated with sensitive card data after they leave your systems to keep you out of PCI scope.**

Using Receivers not listed on [supported Receivers \(Gateways\)](../../pci-proxy/resources/supported-receivers.md) requires a valid AOC \(Attestation of Compliance\) and either a letter of Acknowledgment or an extract of the terms and conditions which proves the PCI DSS compliance of the Receiver. 
{% endhint %}



