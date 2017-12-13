## 1. Add SFTP-Receiver to your account

Adding SFTP-Receivers is easy. You can either pick from our list of supported SFTP-Receivers or add new ones:

| Click to [**Add Receivers**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) |
| :--- |


---

## 2. Firewall changes

Adding a SFTP-Reicever requires changes on our Firewall. Please complete the form [here](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) to let us know concerned IP-addresses.

---

## 3. Redirect a SFTP-Receiver through PCI Proxy

If you have added a SFTP-Receiver to your account, you can easily redirect requests to that SFTP-Receiver via the PCI Proxy.

1. ##### Put `token` instead of `sensitive card data` into your request
2. ##### Use [`PCI Proxy Endpoint`](#reference) as `HOST`
3. ##### Add required [`X-CC HTTP header`](#reference) to your request
4. ##### Keep all other parameters of your request as always

## 3a. Use x-www-form-url encoded

```
$curl https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft                               // HOST: PCI Proxy Endpoint
    -X POST                                                                                    // Request Method POST
    -H "Accept: text/plain"                                                                    // NEW HEADER: Please choose text/plain
    -H "type: BTA or TAMARA"                                                                   // NEW HEADER: Please choose between BTA or TAMARA
    -H "Cache-Control: no-cache"                                                               // NEW HEADER: Please choose no-cache
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8"                        // NEW HEADER: application/x-www-form-urlencoded; charset=UTF-8

    -d 'merchantId=1000011011                                                                  // Merchant ID you received during Signup
    &sign=30916165706580013                                                                    // Security Sign you created in Step 1 
    &url=sftp%3A%2F%2Fint-tests%40193.16.220.99%2FBTATEST%2Ftest.txt                           // SFTP Endpoint
    &file=SOME+FILE+CONTENT                                                                    // Your File
    &password=...'                                                                             // Your password
```

## 3b. Use simple Post

1. ##### Put `token` instead of `sensitive card data` into your request
2. ##### Use [`PCI Proxy Endpoint`](#reference) as HOST with following paramters `merchantID` , `sign` , `url` , `password` and define `type` with `BTA` or `TAMARA`
3. ##### Add required `X-CC HTTP` header

```
$curl 'https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft?merchantId=XXX&sign=XXX&url=sftp://username@127.0.0.1/folder/test-filename.txt&password=XXX&type=BTA'
    -X POST                                                     // Request Method POST

    -H "X-CC-Authorization: xxxxxx"                             // Basic-Auth
    -H "X-CC-Cache-Control: no-cache"                           // Cache-Control
    -H "X-CC-Content-Type: text/plain; charset=UTF-8"           // Accepted: 'text/plan'; 'application/json'; 'application/xml'
    -d '0000080915K...'
```

The service responds based on the_accept header_: Supported are_text/plain, application/json _\(default\) and _application/xml_

---

#### Reference

| **PCI Proxy SFTP Endpoint:** |
| :--- |
| [https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft](/`https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft) |

| Required HTTP header | Description | Example value |
| :--- | :--- | :--- |
| `X-CC-URL` | SFTP Endpoint - Specifies the SFTP-Receiver URL that will be called | [https://api.receiver.com/](https://www.gitbook.com/book/dtrx/pci-proxy/edit#) |
| `X-CC-MERCHANT-ID` | Your Merchant ID | 1000011011 |
| `X-CC-SIGN` | Configured Security Sign \(see [**Step1**](/step-1-signup-and-setup.md)\) | 130709090849785405 |

> ---
>
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



