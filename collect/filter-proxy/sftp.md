# SFTP

PCI Proxy allows you to securely transmit files containing sensitive cardholder data between you and a third-party server. Businesses could, for example, run batch processes for reconciliation, payment (e.g. HOT files), or card update use-cases with non-compliant third-party provider.&#x20;

## Process flow

![PCI Proxy SFTP-to-SFTP flow](<../../.gitbook/assets/SFTP tokenize.drawio.svg>)



## Setup

To set up a new SFTP connection please send us an email to [support@pci-proxy.com](mailto:%20support@pci-proxy.com) and follow the below guide.

1. Tell us about the file type and data format by sending an example file
2. Determine process flow (are you sending the file or does PCI Proxy grab the file)
3. Exchange of IP address and TCP port
4. Exchange of SSH-Key and username
5. Determine directories where the files can be down- and uploaded to

{% hint style="danger" %}
Businesses who are sending sensitive cardholder data in plain text must be compliant according to PCI DSS.&#x20;
{% endhint %}
