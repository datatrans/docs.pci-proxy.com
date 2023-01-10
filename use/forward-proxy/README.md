# Forward Proxy

PCI Proxy allows you to maintain your existing business processes as before. As we connect every stored credit card number to a specific credit card token, you simply use the token to tell PCI Proxy what you want to do with the underlying credit card data.

The existing data communication with your PCI-compliant partners is maintained. These third-party Receivers can be online travel agencies, payment gateways, fraud prevention partners, hotels, airlines, car rentals, etc.&#x20;

Simply redirect the requests containing tokens through PCI Proxy to avoid sensitive data hitting your servers. PCI Proxy automatically scans the requests for tokens and replaces located tokens with sensitive card data and forwards the populated request to the PCI-compliant Receiver. The message structure of your request always remains the same. Any responses from the Receiver are passed back to you and sensitive card data is tokenized if needed.&#x20;

PCI Proxy supports various communication methods to forward sensitive card data to a Receiver:

{% content-ref url="https/" %}
[https](https/)
{% endcontent-ref %}

{% content-ref url="https-to-sftp.md" %}
[https-to-sftp.md](https-to-sftp.md)
{% endcontent-ref %}

{% content-ref url="sftp.md" %}
[sftp.md](sftp.md)
{% endcontent-ref %}

{% hint style="success" %}
Using Receivers not already listed in the Dashboard [Integrations](../../resources/pci-proxy-dashboard/add-integrations.md) overview must be PCI DSS compliant. Thus, a valid AOC is required to configure a new requested 3rd party that receives sensitive credit card data. Please refer to [PCI DSS Validation](../../resources/pci-dss-validation.md) for more details.
{% endhint %}

{% hint style="warning" %}
Please note the allowed TCP ports for HTTP endpoints:

**Sandbox** Port`80`and`443`

**Production** Port`443`
{% endhint %}
