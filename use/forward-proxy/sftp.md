# SFTP

SFTP PCI Proxy allows you to securely transmit files containing sensitive cardholder data between you and a third-party server. Businesses could, for example, run batch processes for reconciliation, payment (e.g. HOT files), or card update use-cases with non-compliant third-party providers.

## Process flow <a href="#process-flow" id="process-flow"></a>

PCI Proxy SFTP-to-SFTP flow

![](https://files.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MhOSTnvt-br-2EmFGhA%2F-MiaDeao-coa5nDjI9pz%2F-MiaDuOkgNDrgrnQT5st%2FSFTP%20tokenize.drawio.svg?alt=media\&token=60851ff7-fad7-46df-a58b-d1aa8deff9a6)

## Setup <a href="#setup" id="setup"></a>

To set up a new SFTP connection please send us an email to [support@pci-proxy.com](mailto:%20support@pci-proxy.com) and follow the below guide.

1. Tell us about the file type and data format by sending an example file
2. Determine process flow (are you sending the file or does PCI Proxy grab the file)
3. Exchange of IP address and TCP port
4. Exchange of SSH-Key and username
5. Determine directories where the files can be down- and uploaded to

{% hint style="danger" %}
Businesses that are sending sensitive cardholder data in plain text must be compliant according to PCI DSS.
{% endhint %}
