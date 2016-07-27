# XML Alias Gateway

Let us assume you want to create a token for a credit card number.

```By using our XML Alias Gateway```, you can easily convert a credit card number (cardno) into a token (alias).


> **Attention:** This XML Alias Gateway is only for PCI DSS certified companies as you get in contact with full credit card numbers.

## How to start

> [Sign up](https://www.pci-proxy.com/#/signup) for a free developer test account.

As the XML Alias Gateway is **only** for PCI DSS certified companies, please contact our support to active XML Alias Gateway functionality on your developer test account first.


## Tokenize a credit card

In order to generate a token, use the following example request.

| **PCI Proxy PULL Endpoint:** |
| -- |
| https://pilot.datatrans.biz/upp/jsp/XML_AliasGateway.jsp|

- **XSD schema locations:**


| Schema     | Location                                                        | 
| -------------- | -------------------------------------------------------------------|
| `base.xsd` | https://pilot.datatrans.biz/upp/schema/base.xsd |
| `aliasCC.xsd` | https://pilot.datatrans.biz/upp/schema/aliasCC.xsd | 
            



- **Example request:**


```xml
    $ curl 
      -X POST 
      -H "Content-Type: text/xml; charset=utf8" 
        --data-binary @-https://pilot.datatrans.biz/upp/jsp/XML_AliasGateway.jsp 
          <?xml version="1.0" encoding="UTF8" ?>
            <aliasCCService version="1">
              <body merchantId="1000011011">
                <alias>
                  <request>
                    <cardno>4950000111111110</cardno>
                    <sign>30916165706580013</sign>
                  </request>
                </alias>
              </body>
            </aliasCCService>
```

- **Example response:**

```xml
<?xml version='1.0' encoding='UTF8'?>
  <aliasCCService version='1'>
    <body merchantId='1000011011' status='accepted'>
      <alias aliasStatus='response'>
        <request>
          <cardno>4950000111111110</cardno>
          <sign>30916165706580013</sign>
        </request>
        <response>
          <aliasCC>80205164913895528</aliasCC>
          <cardno>4950000111111110</cardno>
          <maskedCC>495000xxxxxx1110</maskedCC>
        </response>
      </alias>
    </body>
  </aliasCCService>
  
```

> Note: In test mode, only test credit cards are allowed. For testing purposes, you will need our [test credit cards](live_mode-test.html). Learn more about [live mode and testing](live_mode-test.html).


### Error Case

- **Example request:**

```xml
    $ curl 
      -X POST 
      -H "Content-Type: text/xml; charset=utf8" 
        --data-binary @-https://pilot.datatrans.biz/upp/jsp/XML_AliasGateway.jsp 
          <?xml version="1.0" encoding="UTF8" ?>
            <aliasCCService version="1">
              <body merchantId="1000011011">
                <alias>
                  <request>
                    <cardno>4950000111111110</cardno>
                    <sign>30916165706580013</sign>
                  </request>
                </alias>
              </body>
            </aliasCCService>

```

- **Example response:**

```xml
<?xml version='1.0' encoding='UTF8'?>
  <aliasCCService version='1'>
    <body merchantId='1000011011' status='accepted'>
      <alias aliasStatus='error'>
        <request>
          <cardno>49500001111110</cardno>
          <sign>30916165706580013</sign>
        </request>
        <error>
          <errorCode>1004</errorCode>
          <errorMessage>CC number is not valid</errorMessage>
          <errorDetail>check modulo10 failed</errorDetail>
        </error>
      </alias>
    </body>
  </aliasCCService>
  
```

#### Possible error cases

| errorCode | errorMessage | Explanation |
| -- | -- | -- | 
|1004 | CC number is not valid | Luhn check failed
|2000 | access denied | XML alias service not enabled by Datatrans
|2001 | no input document | Request body does not contain XML payload
|2002 | error building document | Wrong XML payload in request
|2011 | root element invalid | Root element is not ```<aliasCCService>```
|2012 | body element missing | ```<body>``` element in request is missing
|2013 | merchantId missing | ```<body>``` element does not have a merchantId attribute
|2014 | element missing | Element is missing. For example ```<alias>```
|2022 | invalid value | Invalid value passed for one of the attributes. For example ```merchantId```
| -889 | CC-alias error | Input paramter(s) missing. For example ```<cardno>``` |