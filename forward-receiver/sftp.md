## 1. Add SFTP-Receiver to your account

Adding SFTP-Receivers is easy. You can either pick from our list of supported Receivers or add new ones:

| Click to [**Add Receivers**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) |
| :--- |


---

## 2. Firewall changes

Adding a SFTP-Reicever requires changes on our Firewall. Please complete the form [here](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) to let us know concerned IP-addresses.

---

## 3a. Use simple POST

```
$curl 'https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft?merchantId=XXX&sign=XXX&url=sftp://username@127.0.0.1/folder/test-filename.txt&password=XXX'
    -X POST \
    -H "Accept: appplication/json" \
    -H "type: BTA or TAMARA" \ // please choose between BTA or TAMARA
    -H "Cache-Control: no-cache" \
    -H "Content-Type: text/plain; charset=UTF-8" \
    -d '0000080915K...'
```

## 3b. Use x-www-form-url encoded

```
$curl https://pilot.datatrans.biz/upp/services/v1/proxy/ft                         // HOST: PCI Proxy Endpoint
    -X POST                                                                        // Request Method POST
    -H "Accept: text/plain"                                                        // NEW HEADER: Please choose test/plain
    -H "type: BTA or TAMARA"                                                       // NEW HEADER: Please choose between BTA or TAMARA
    -H "Cache-Control: no-cache"                                                   // NEW HEADER: Please choose no-cache
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8"            // NEW HEADER: application/x-www-form-urlencoded; charset=UTF-8

    -d 'merchantId=1000011011&sign=30916165706580013&url=sftp%3A%2F%2Fint-tests%40193.16.220.99%2FBTATEST%2Ftest.txt&file=SOME+FILE+CONTENT&password=...'
```



