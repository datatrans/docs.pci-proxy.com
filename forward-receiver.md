# Quickstart: Forward card data to a Receiver

PCI Proxy allows you to retain your existing data communication with PCI-compliant Receiver. This can be online travel agencies, payment gateways, hotels, airlines, car rentals, etc.

Simply `redirect requests containing tokens through PCI Proxy` to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for tokens and replaces located tokens with sensitive card data and forwards the populated request to the PCI-compliant Receiver. The message structure of your request always remains the same. Any responses from the Receiver are passed back to you and sensitive card data is tokenized if needed.

PCI Proxy provides you two different ways forwarding data to a Receiver.

1. [Forward data by using our PULL or PUSH API](https://www.gitbook.com/book/dtrx/pci-proxy/edit#/edit/changes/8/forward-receiver/api.md?_k=8fla9h)
2. [Forward data by using our SFTP service](https://www.gitbook.com/book/dtrx/pci-proxy/edit#/edit/changes/8/forward-receiver/sftp.md?_k=lkyccp)

### **Watch out!**

**Your requests are populated with sensitive card data after they left your systems to keep you out of PCI scope.**

> **Using Receivers not listed on **[**supported Receivers \(Gateways\)**](/supported_receivers.md)** requires a valid AOC \(Attestation of Compliance\) and either a letter of Acknowledgment  or an extract of the terms and conditions which proves the PCI DSS compliance of the Receiver. **

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



