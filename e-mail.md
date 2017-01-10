# Collect credit cards via Email

Let us assume you have an offer for your customers and you want to collect the card data directly via email. Just generate a payment link and copy it into your email. Your customers can click on the link and our payment page is opened. They can choose their favorite payment method and pay directly.

## How to start

> [Sign up](https://www.pci-proxy.com/#/signup) for a free developer test account.

Our PayByEmailService allows you to generate Pay-by-Email payment links.

### Generate payment links

| **PayByEmailService Endpoint:** |
| --- |
| [https://pilot.datatrans.biz/upp/jsp/XML\_PayByEmail](https://pilot.datatrans.biz/upp/jsp/XML_PayByEmail) |

**Just send the following payload to our PayByEmailService Endpoint:**

```xml
<?xml version="1.0" encoding="UTF-8" ?>
  <payByEmailService version="1">
    <body merchantId="1000011011">
      <language>en</language>
      <currency>eur</currency>
      <amount>400</amount>
      <refno>XML test</refno>
      <duedate>20151231</duedate>
    </body>
  </payByEmailService>
```

_Duedate should be in the yyyymmdd format._

**As a response you receive the payment link:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
  <payByEmailService version="1">
    <body merchantId="1000011011">
      <payByEmailURL>https://pilot.datatrans.biz/upp/jsp/upStartFromTemplate?paymentTemplateId=021935b9-
54fb-f8f8-0000-015191015e03</payByEmailURL>
    </body>
  </payByEmailService>
```



