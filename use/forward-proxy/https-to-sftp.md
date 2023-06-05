# HTTPS to SFTP

## 1. Add a SFTP-Receiver to your account <a href="#1.-add-a-sftp-receiver-to-your-account" id="1.-add-a-sftp-receiver-to-your-account"></a>

PCI Proxy's SFTP service currently supports the following filetypes `BTA`, `TAMARA`, `DINERSMINERVA`, `TACS`, `MASTERCARDTAED`, `VISAIBERIA` or `VISABBVA`.

Before sending a request to a PCI compliant 3rd party you have to add the SFTP server as an integration to your account.

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration&#x20;

2\) Check the endpoint of the integration and press **Install**&#x20;

3\) Check if the payload fits your example and press again **Install** to activate the integration

Continue here if you miss an integration, if the payload or an endpoint doesn't match your requirements.

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration&#x20;

2\) Press **Request new Integration** button and complete the form (please add the source IP of the new Receiver in the comment field)&#x20;

3\) You will get notified once the requested integration is ready for you.

## 2. Redirect a SFTP-Receiver through PCI Proxy <a href="#2.-redirect-a-sftp-receiver-through-pci-proxy" id="2.-redirect-a-sftp-receiver-through-pci-proxy"></a>

If you have added a SFTP-Receiver to your account, you can easily redirect requests to that SFTP-Receiver via PCI Proxy. The requests can be sent as follows:

### 2a. Use simple Post <a href="#2a.-use-simple-post" id="2a.-use-simple-post"></a>

1. Replace sensitive card data with the token in your request
2. Use the PCI Proxy Endpoint as HOST with the following parameters `merchantId`, `sign`, `url`, `password`and define `type`with `BTA`, `TAMARA`, `DINERSMINERVA`, `TACS`, `MASTERCARDTAED`, `VISAIBERIA` or `VISABBVA`
3. Add the required HTTP headers and POST data to your request

```
curl 'https://sandbox.pci-proxy.com/v1/ft?merchantId=XXX&sign=XXX&url=sftp://username@127.0.0.1/folder/test-filename.txt&password=XXX&type=BTA'
    -X POST                                                // Request Method POST
    -H "Content-Type: text/plain; charset=UTF-8"           // Accepted: 'text/plain'; 'application/json'; 'application/xml'
    -d '0000080915K...'
```



The service responds based on the Accept header: Supported are text/plain, application/json (default) and application/xml

### 2b. Use x-www-form-url encoded

* Replace sensitive card data with the token in your request
* Use the PCI Proxy Endpoint as HOST
* Add the required HTTP headers to your request
* Add the required POST data: merchantID, sign, url, file password and type

```
curl https://sandbox.pci-proxy.com/v1/ft                                                   // HOST: PCI Proxy Endpoint
    -X POST                                                                                // Request Method POST
    -H "Accept: text/plain"                                                                // NEW HEADER: Please choose text/plain
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8"                    // NEW HEADER: application/x-www-form-urlencoded; charset=UTF-8

    -d 'merchantId=1000011011                                                              // Merchant ID from PCI Proxy Dashboard
    &sign=30916165706580013                                                                // Security Sign from PCI Proxy Dashboard
    &url=sftp%3A%2F%2Fint-tests%40127.0.0.1%2Ffolder%2Ftest.txt                            // SFTP Endpoint
    &file=SOME+FILE+CONTENT                                                                // Your File
    &password=XXX                                                                          // Your password
    &type=BTA 
```

You have securely forwarded sensitive card data without ever touching your servers. Your request has been populated with sensitive card data while it was routed through PCI Proxy. Thereby, your Receiver obtained full credit card data.

_Note: In test mode, only test credit cards are allowed!_

## Reference

| PCI Proxy SFTP Endpoint:            |
| ----------------------------------- |
| https://sandbox.pci-proxy.com/v1/ft |

<table><thead><tr><th width="189">Required parameter</th><th width="179">Description</th><th>Example Value</th></tr></thead><tbody><tr><td><code>merchantId</code></td><td>Your Merchant ID</td><td>1000011011</td></tr><tr><td><code>sign</code></td><td>Configured Security Sign </td><td>130709090849785405</td></tr><tr><td><code>url</code></td><td>Your SFTP endpoint</td><td>sftp://username@example.com/folder/test-filename.t</td></tr><tr><td><code>file</code></td><td>The file you want to upload</td><td>some+file+content</td></tr><tr><td><code>password</code></td><td>Your password</td><td>asdfölksdjfasjdh</td></tr><tr><td><code>type</code></td><td>Filetype of transmitted request</td><td><code>BTA</code>, <code>TAMARA</code>, <code>DINERSMINERVA</code>, <code>TACS</code>, <code>TAED</code>, <code>VISAIBERIA</code> or <code>VISABBVA</code></td></tr></tbody></table>

