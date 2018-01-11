## 1. Add SFTP-Receiver to your account

Adding a SFTP-Receiver is easy. You can either pick from our list of supported SFTP-Receivers or add new ones:

| Click to Add** **[**SFTP-Receivers**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) |
| :--- |


---

## 2. Firewall changes

Adding SFTP-Reicever requires changes on our firewall. Please complete the form [here](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) to let us know concerned IP-addresses.

---

## 3. Redirect a SFTP-Receiver through PCI Proxy

If you have added a SFTP-Receiver to your account, you can easily redirect requests to that SFTP-Receiver via the PCI Proxy. Requests can be sent as follows:

### 3a. Use simple Post

1. Put `token` instead of `sensitive card data` into your request

2. Use [`PCI Proxy Endpoint`](#reference) as HOST with following paramters `merchantId` , `sign` , `url` , `password` and define `type` with `BTA` or `TAMARA`

3. Add required [`X-CC HTTP`](#reference) header to your request

```
$curl 'https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft?merchantId=XXX&sign=XXX&url=sftp://username@127.0.0.1/folder/test-filename.txt&password=XXX&type=BTA'
    -X POST                                                     // Request Method POST

    -H "X-CC-Authorization: xxxxxx"                             // Basic-Auth
    -H "X-CC-Cache-Control: no-cache"                           // Cache-Control
    -H "X-CC-Content-Type: text/plain; charset=UTF-8"           // Accepted: 'text/plan'; 'application/json'; 'application/xml'
    -d '0000080915K...'                                         // define the content
```

The service responds based on the _accept header_: Supported are_text/plain, application/json _\(default\) and _application/xml_

### 3b. Use x-www-form-url encoded

1. Put `token` instead of `sensitive card data` into your request

2. Use [`PCI Proxy Endpoint`](#reference) as `HOST`

3. Add required [`parameter`](#reference) to your request

4. Add required POST data: `merchantID`, `sign`, `url`, `file` and `password`

```
$curl https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft                           // HOST: PCI Proxy Endpoint
    -X POST                                                                                // Request Method POST
    -H "X-CC-Accept: text/plain"                                                           // NEW HEADER: Please choose text/plain
    -H "X-CC-Cache-Control: no-cache"                                                      // NEW HEADER: Please choose no-cache
    -H "X-CC-Content-Type: application/x-www-form-urlencoded; charset=UTF-8"               // NEW HEADER: application/x-www-form-urlencoded; charset=UTF-8

    -d 'merchantId=1000011011                                                              // Merchant ID you received during Signup
    &sign=30916165706580013                                                                // Security Sign you created in Step 1 
    &url=sftp%3A%2F%2Fint-tests%40127.0.0.1%2Ffolder%2Ftest.txt                            // SFTP Endpoint
    &file=SOME+FILE+CONTENT                                                                // Your File
    &password=XXX                                                                          // Your password
    &type=BTA'                                                                             // BTA or TAMARA
```

You have securely forwarded sensitive card data without ever touching your servers. Your request had been populated with sensitive card data while it was routed through PCI Proxy. Thereby, your Receiver obtained full credit card data.

_Note: In test mode, only test credit cards are allowed!_

---

## Reference

| **PCI Proxy SFTP Endpoint:** |
| :--- |
| [https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft](/`https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft) |

| Required parameter | Description | Example Value |
| :--- | :--- | :--- |
| merchantId | Your Merchant ID | 1000011011 |
| sign | Configured Security Sign \(see [Step 1\)](/step-1-signup-and-setup.md) | 130709090849785405 |
| url | Your SFTP endpoint | url=sftp%test%xxx.txt |
| file | The file you want to upload | some+file+content |
| password | Your password | asdfölksdjfasjdh |
| type | Filetype, choose between BTA or TAMARA | BTA or TAMARA |

---

> ## Great job**: You have successfully integrated PCI Proxy! **
>
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



