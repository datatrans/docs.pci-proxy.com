# Quickstart: Forward card data to a Receiver

PCI Proxy allows you to retain your existing data communication with PCI-compliant Receiver. This can be online travel agencies, payment gateways, hotels, airlines, car rentals, etc.

> **Forwarding card data to a Receiver works the same way as collecting card data via web service.**

Simply `redirect requests containing tokens through PCI Proxy` to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for tokens and replaces located tokens with sensitive card data and forwards the populated request to the PCI-compliant Receiver. The message structure of your request always remains the same. Any responses from the Receiver are passed back to you and sensitive card data is tokenized if needed.

**Your requests are populated with sensitive card data after they left your systems to keep you out of PCI scope.**

> **Using Receivers not listed on **[**supported Receivers \(Gateways\)**](/supported_receivers.md)** requires a valid AOC \(Attestation of Compliance\)**

---

## Great job**: You have successfully integrated PCI Proxy! **

> You have securely forwarded sensitive card data without ever touching your servers. **Your systems never record, transmit or store real credit card data, only the token. Thus, you are out of PCI scope. **
>
> Enjoy PCI compliance in a risk-free environment. Keep in mind that you can use stored data as often as you need it.
>
> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



