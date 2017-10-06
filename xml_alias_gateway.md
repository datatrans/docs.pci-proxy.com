# XML Alias Gateway

Let us assume you want to create a token for a credit card number via web service.

`By using our XML Alias Gateway`, you can easily convert a credit card number \(cardno\) into a token \(alias\).

> **Attention:** This XML Alias Gateway is only for PCI DSS certified companies as you get in contact with full credit card numbers.

## How to start

> [Sign up](https://www.pci-proxy.com/#/signup) for a free developer test account.

As the XML Alias Gateway is **only** for PCI DSS certified companies, please contact our support to active XML Alias Gateway functionality on your developer test account first.

## Tokenize a credit card

In order to generate a token, use the following example request.

| **PCI Proxy PULL Endpoint:** |
| --- |
| [https://api.sandbox.datatrans.com/upp/jsp/XML\_AliasGateway.jsp](https://api.sandbox.datatrans.com/upp/jsp/XML_AliasGateway.jsp) |

* **XSD schema locations:**

| Schema | Location |
| --- | --- |
| `base.xsd` | [https://api.sandbox.datatrans.com/upp/schema/base.xsd](https://api.sandbox.datatrans.com/upp/schema/base.xsd) |
| `aliasCC.xsd` | [https://api.sandbox.datatrans.com/upp/schema/aliasCC.xsd](https://api.sandbox.datatrans.com/upp/schema/aliasCC.xsd) |

* **Example request:**

```xml
curl "https://api.sandbox.datatrans.com/upp/jsp/XML_AliasGateway.jsp" -X POST -H "Content-Type: text/xml" -d '
<?xml version="1.0" encoding="UTF-8"?>
 <aliasCCService version="1">
   <body merchantId="1000011011">
     <alias>
        <request>
            <cardno>375811111111115</cardno>
        </request>
     </alias>
     <alias>
        <request>
            <cvv>123</cvv>
        </request>
     </alias>
   </body>
 </aliasCCService>
```

* **Example response:**

```xml
<?xml version='1.0' encoding='UTF-8'?>
<aliasCCService version='1'>
    <body merchantId='1000011011' status='accepted'>
        <alias aliasStatus='response'>
            <request>
                <cardno>375811111111115</cardno>
            </request>
            <response>
                <aliasCC>375811OMTYEE115</aliasCC>
                <cardno>375811111111115</cardno>
                <maskedCC>375811xxxxx1115</maskedCC>
            </response>
        </alias>
        <alias aliasStatus='response'>
            <request>
                <cvv>123</cvv>
            </request>
            <response>
                <aliasCVV>EicQYIP6QA69Or_6DqBOLNQf</aliasCVV>
                <uppCvvExpiryDate>2017-03-28</uppCvvExpiryDate>
            </response>
        </alias>
    </body>
</aliasCCService>
```

> Note: In test mode, only test credit cards are allowed. For testing purposes, you will need our [test credit cards](live_mode-test.html). Learn more about [live mode and testing](live_mode-test.html).

### Error Case

* **Example request:**

```xml
curl "https://api.sandbox.datatrans.com/upp/jsp/XML_AliasGateway.jsp" -X POST -H "Content-Type: text/xml" -d '
<?xml version="1.0" encoding="UTF-8"?>
 <aliasCCService version="1">
   <body merchantId="1000011011">
     <alias>
        <request>
            <cardno>000</cardno>
        </request>
     </alias>
     <alias>
        <request>
            <cvv>a</cvv>
        </request>
     </alias>
   </body>
 </aliasCCService>'
```

* **Example response:**

```xml
<?xml version='1.0' encoding='UTF-8'?>
<aliasCCService version='1'>
    <body merchantId='1000011011' status='accepted'>
        <alias aliasStatus='error'>
            <request>
                <cardno>000</cardno>
            </request>
            <error>
                <errorCode>1004</errorCode>
                <errorMessage>CC number is not valid</errorMessage>
                <errorDetail>check modulo-10 failed</errorDetail>
            </error>
        </alias>
        <alias aliasStatus='error'>
            <request>
                <cvv>a</cvv>
            </request>
            <error>
                <errorCode>2022</errorCode>
                <errorMessage>invalid value</errorMessage>
                <errorDetail>cvv</errorDetail>
            </error>
        </alias>
    </body>
</aliasCCService>
```

#### Possible error cases

| errorCode | errorMessage | Explanation |
| --- | --- | --- |
| 1004 | CC number is not valid | Luhn check failed |
| 2000 | access denied | XML alias service not enabled by Datatrans |
| 2001 | no input document | Request body does not contain XML payload |
| 2002 | error building document | Wrong XML payload in request |
| 2011 | root element invalid | Root element is not `<aliasCCService>` |
| 2012 | body element missing | `<body>` element in request is missing |
| 2013 | merchantId missing | `<body>` element does not have a merchantId attribute |
| 2014 | element missing | Element is missing. For example `<alias>` |
| 2022 | invalid value | Invalid value passed for one of the attributes. For example `merchantId` |
| -889 | CC-alias error | Input paramter\(s\) missing. For example `<cardno>` |



