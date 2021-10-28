# Vault (alias gateway)

The Alias Gateway allows you to pass credit card data directly to the PCI Proxy vault to create tokens. This can be interesting if you want to migrate existing credit card data that is currently stored somewhere else to store it within the PCI Proxy vault.

{% swagger baseUrl="https://api.sandbox.datatrans.com/" path="upp/jsp/XML_AliasGateway.jsp" method="post" summary="XML Alias Gateway" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" required="true" %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==
{% endswagger-parameter %}

{% swagger-parameter in="header" name="Content-Type" type="string" required="true" %}
API consumes text/xml
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchantId" type="string" required="true" %}
Your unique account id at PCI Proxy (e.g. 1000011011)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cardno" type="string" required="false" %}
Credit card number (PAN) to be tokenized
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cvv" type="string" required="false" %}
Security code (CVV/CVC) to be tokenized
{% endswagger-parameter %}

{% swagger-response status="200" description="You receive a credit card token (aliasCC) and CVV token (aliasCVV)." %}
```xml
<?xml version='1.0' encoding='UTF-8'?>
<aliasCCService version="1">
    <body merchantId="1000011011" status="accepted">
        <alias aliasStatus="response">
            <request>
                <cardno>375811111111115</cardno>
            </request>
            <response>
                <aliasCC>375811OMTYEE115</aliasCC>
                <cardno>375811111111115</cardno>
                <maskedCC>375811xxxxx1115</maskedCC>
            </response>
        </alias>
        <alias aliasStatus="response">
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
{% endswagger-response %}

{% swagger-response status="400" description="Invalid value passed for one of the attributes (e.g. merchantId)." %}
```xml
<?xml version='1.0' encoding='UTF-8'?>
<aliasCCService version="1">
    <body merchantId="1000011011" status="accepted">
        <alias aliasStatus="error">
            <request>
                <cardno>000</cardno>
            </request>
            <error>
                <errorCode>1004</errorCode>
                <errorMessage>CC number is not valid</errorMessage>
                <errorDetail>check modulo-10 failed</errorDetail>
            </error>
        </alias>
        <alias aliasStatus="error">
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
{% endswagger-response %}
{% endswagger %}



The XML Alias Gateway converts credit card data into tokens. The service allows bulk tokenization, allowing multiple  <`alias>`elements, so it is possible to tokenize a card and a cvv at the same time.

XSD Schema: [https://api.sandbox.datatrans.com/upp/schema/aliasCC.xsd](https://api.sandbox.datatrans.com/upp/schema/aliasCC.xsd)

{% hint style="warning" %}
The service requires HTTP basic authentication. The required credentials can be found in our dashboard. Please refer to [API authentication data](../guides/pci-proxy-dashboard/api-authentication-data.md#basic-authentication) for more information.
{% endhint %}

### Examples

{% tabs %}
{% tab title="Example Request" %}
```markup
curl -L -X POST 'https://api.sandbox.datatrans.com/upp/jsp/XML_AliasGateway.jsp' \
-H 'Content-Type: text/xml' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
--data-raw '       <aliasCCService version="3">
         <body merchantId="1100017789">
           <alias>
              <request>
                  <cardno>4242424242424242</cardno>
              </request>
           </alias>
           <alias>
              <request>
                  <cvv>123</cvv>
              </request>
           </alias>
         </body>
       </aliasCCService>'
```
{% endtab %}

{% tab title="Example Response" %}
```xml
<aliasCCService version='3'>
    <body merchantId='1100017789' status='accepted'>
        <alias aliasStatus='response'>
            <request>
                <cardno>4242424242424242</cardno>
            </request>
            <response>
                <aliasCC>AAABeM8o_izssdexyrAAAS7Q-uDnAMF_</aliasCC>
                <cardno>4242424242424242</cardno>
                <maskedCC>424242xxxxxx4242</maskedCC>
                <fingerprint>F-dV5V8dE0SZLoTurWbq2HZp</fingerprint>
            </response>
        </alias>
        <alias aliasStatus='response'>
            <request>
                <cvv>123</cvv>
            </request>
            <response>
                <aliasCVV>ybImDdgvT3KGAD0EGZhmRvYq</aliasCVV>
                <uppCvvExpiryDate>2022-12-05</uppCvvExpiryDate>
            </response>
        </alias>
    </body>
</aliasCCService>
```
{% endtab %}

{% tab title="Bad Request Error Case" %}
```xml
curl "https://api.sandbox.datatrans.com/upp/jsp/XML_AliasGateway.jsp" \
  -H "Content-Type: text/xml" \
  -d '<?xml version="1.0" encoding="UTF-8"?>
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
{% endtab %}

{% tab title="Error Case Response" %}
```xml
<?xml version='1.0' encoding='UTF-8'?>
<aliasCCService version="1">
    <body merchantId="1000011011" status="accepted">
        <alias aliasStatus="error">
            <request>
                <cardno>000</cardno>
            </request>
            <error>
                <errorCode>1004</errorCode>
                <errorMessage>CC number is not valid</errorMessage>
                <errorDetail>check modulo-10 failed</errorDetail>
            </error>
        </alias>
        <alias aliasStatus="error">
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
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
In test mode, only [test credit cards](../test-card-data.md) are allowed.
{% endhint %}

### Error cases

| **errorCode** | **errorMessage**        | **Explanation**                                            |
| ------------- | ----------------------- | ---------------------------------------------------------- |
| 1004          | CC number not valid     | Luhn check failed                                          |
| 2000          | access denied           | XML alias service not enabled by Datatrans                 |
| 2001          | no input document       | Request body does not contain XML payload                  |
| 2002          | error building document | Wrong XML payload in request                               |
| 2011          | root element invalid    | Root element is not `<aliasCCService>`                     |
| 2012          | body element missing    | `<body>` element in request is missing                     |
| 2013          | merchantId missing      | `<body>` element does not have a merchantId attribute      |
| 2014          | element missing         | Element is missing. For example `<alias>`                  |
| 2022          | invalid value           | Invalid value passed for an attribute. (e.g. `merchantId`) |
| -889          | CC-alias error          | Input paramter(s) missing. For example `<cardno>`          |

## Next up

{% content-ref url="../use-stored-cards/" %}
[use-stored-cards](../use-stored-cards/)
{% endcontent-ref %}
