## 1. Add SFTP-Receiver to your account

Adding Receivers is easy. You can either pick from our list of [supported Receivers \(Gateways\)](/supported_receivers.md) or add new ones:

| Click to [**Add Receivers**](https://admin.sandbox.datatrans.com/showcase/pci-proxy/add-receiver.html) |
| :--- |
| _Learn more about _[_**Request Types**_](/request-types.md)_._ |

---

## 2a. Use simple POST

```
$curl 'https://api.sandbox.datatrans.com/upp/services/v1/proxy/ft?merchantId=XXX&sign=XXX&url=sftp://username@127.0.0.1/folder/test-filename.txt&password=XXX'
    -X POST \
    -H "Accept: appplication/json" \
    -H "type: BTA or TAMARA" \ // please choose between BTA or TAMARA
    -H "Cache-Control: no-cache" \
    -H "Content-Type: text/plain; charset=UTF-8" \
    -d '0000080915K...'
```

## 2b\) x-www-form-urlencoded

```
$curl https://pilot.datatrans.biz/upp/services/v1/proxy/ft \
    -X POST \
    -H "Accept: text/plain"
    -H "type: BTA or TAMARA" // please choose between BTA or TAMARA
    -H "Cache-Control: no-cache"
    -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8"
    -d 'merchantId=1000011011&sign=30916165706580013&url=sftp%3A%2F%2Fint-tests%40193.16.220.99%2FBTATEST%2Ftest.txt&file=SOME+FILE+CONTENT&password=...'
```



