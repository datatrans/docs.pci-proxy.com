# HTTPS  to SFTP

## 1. Add SFTP-Receiver to your account

PCI Proxy SFTP service currently supports the following filetypes `BTA`, `TAMARA`, `DINERSMINERVA`, `TACS`, `TAED`, `VISAIBERIA` or `VISABBVA`.

Before you can send request to a PCI compliant 3rd party you have to add the SFTP server as an integration to your account. 

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration  
2\) Check the endpoint of the integration and press **Install**  
3\) Check if the payload fits your example and press again **Install** to activate the integration

Continue here if you miss an integration, if the payload or an endpoint doesn't match your requirements.

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration  
2\) Press **Request new Integration** button and complete the form \(please add the source IP of the new Receiver in the comment field\)  
3\) You get notified once the requested integration is ready for you

## 2. Redirect a SFTP-Receiver through PCI Proxy

If you have added a SFTP-Receiver to your account, you can easily redirect requests to that SFTP-Receiver via the PCI Proxy. Requests can be sent as follows:

### 2a. Use simple Post

1. Replace sensitive card data with the token in your request
2. Use PCI Proxy Endpoint as HOST with following parameters `merchantId`, `sign`, `url`, `password`and define `type`with `BTA`, `TAMARA`, `DINERSMINERVA`, `TACS`, `TAED`, `VISAIBERIA` or `VISABBVA`
3. Add required HTTP headers and POST data to your request

```bash
curl 'https://sandbox.pci-proxy.com/v1/ft?merchantId=XXX&sign=XXX&url=sftp://username@127.0.0.1/folder/test-filename.txt&password=XXX&type=BTA'
    -X POST                                                // Request Method POST
    -H "Content-Type: text/plain; charset=UTF-8"           // Accepted: 'text/plan'; 'application/json'; 'application/xml'
    -d '0000080915K...'                                    // define the content
```

The service responds based on the _Accept header_: Supported are _text/plain, application/json_ \(default\) and _application/xml_

### 2b. Use x-www-form-url encoded

1. Replace sensitive card data with the token in your request
2. Use PCI Proxy Endpoint as HOST
3. Add required HTTP headers to your request
4. Add required POST data: merchantID, sign, url, file password and type

```bash
curl https://sandbox.pci-proxy.com/v1/ft                                                   // HOST: PCI Proxy Endpoint
    -X POST                                                                                // Request Method POST
    -H "Accept: text/plain"                                                                // NEW HEADER: Please choose text/plain
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8"                    // NEW HEADER: application/x-www-form-urlencoded; charset=UTF-8

    -d 'merchantId=1000011011                                                              // Merchant ID from PCI Proxy Dashboard
    &sign=30916165706580013                                                                // Security Sign from PCI Proxy Dashboard
    &url=sftp%3A%2F%2Fint-tests%40127.0.0.1%2Ffolder%2Ftest.txt                            // SFTP Endpoint
    &file=SOME+FILE+CONTENT                                                                // Your File
    &password=XXX                                                                          // Your password
    &type=BTA                                                                              // BTA, TAMARA, DINERSMINERVA, TACS, TAED, VISAIBERIA or VISABBVA' 
```

You have securely forwarded sensitive card data without ever touching your servers. Your request has been populated with sensitive card data while it was routed through PCI Proxy. Thereby, your Receiver obtained full credit card data.

_Note: In test mode, only test credit cards are allowed!_

## Reference

| **PCI Proxy SFTP Endpoint:** |
| :--- |
| [https://sandbox.pci-proxy.com/v1/ft](https://sandbox.pci-proxy.com/v1/ft) |

| Required parameter | Description | Example Value |
| :--- | :--- | :--- |
| merchantId | Your Merchant ID | 1000011011 |
| sign | Configured Security Sign \(see [Step 1\)](../../setup.md) | 130709090849785405 |
| url | Your SFTP endpoint | url=sftp%test%xxx.txt |
| file | The file you want to upload | some+file+content |
| password | Your password | asdfölksdjfasjdh |
| type | Filetype of transmitted request | `BTA`, `TAMARA`, `DINERSMINERVA`, `TACS`, `TAED`, `VISAIBERIA` or `VISABBVA` |

> ## Great job**: You have successfully integrated PCI Proxy!**
>
> You have securely forwarded sensitive card data without ever touching your servers. **Your systems never record, transmit or store real credit card data, only the token. Thus, you are out of PCI scope.**
>
> Enjoy PCI compliance in a risk-free environment. Keep in mind that you can use stored data as often as you need it.
>
> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [contact@pci-proxy.com](mailto:support@pci-proxy.com)

