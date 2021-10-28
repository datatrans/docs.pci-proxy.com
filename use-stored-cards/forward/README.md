# Forward

PCI Proxy allows you to retain your existing data communication with your PCI-compliant plain text credit cards Receiver. This can be online travel agencies, payment gateways, hotels, airlines, car rentals, etc.

Simply redirect requests containing tokens through PCI Proxy to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for tokens and replaces located tokens with sensitive card data and forwards the populated request to the PCI-compliant Receiver. The message structure of your request always remains the same. Any responses from the Receiver are passed back to you and sensitive card data is tokenized if needed.

PCI Proxy supports various communication methods to forward sensitive card data to a Receiver:

{% content-ref url="https/" %}
[https](https/)
{% endcontent-ref %}

{% content-ref url="sftp.md" %}
[sftp.md](sftp.md)
{% endcontent-ref %}

{% hint style="success" %}
**Your requests are populated with sensitive card data after they leave your systems to keep you out of PCI scope.**

Using Receivers not already listed in the Dashboard [Integrations ](../../guides/pci-proxy-dashboard/add-integrations.md)overview must be PCI DSS compliant. Thus, a valid AOC is required to configure a new requested 3rd party which receives sensitive credit card data. Please refer to [3rd-Party Receiver Validation](../../guides/3rd-party-receiver-validation.md) guideline for more details.
{% endhint %}
