# Vault \(alias gateway\)

The Alias Gateway allows you to pass credit card data directly to the PCI Proxy vault to create tokens. This can be interesting if you want to migrate existing credit card data that is currently stored somewhere else to store it within the PCI Proxy vault. 

{% api-method method="post" host="https://api.sandbox.datatrans.com/" path="upp/jsp/XML\_AliasGateway.jsp" %}
{% api-method-summary %}
XML Alias Gateway
{% endapi-method-summary %}

{% api-method-description %}
The XML Alias Gateway converts credit card data into tokens. The service allows bulk tokenization, allowing multiple `<alias>` elements, so it is possible to tokenize a card and a cvv at the same time. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=false %}
API consumes text/xml
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="merchantId" type="string" required=false %}
Your unique account id at PCI Proxy \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="cardno" type="string" required=false %}
Credit card number \(PAN\) to be tokenized
{% endapi-method-parameter %}

{% api-method-parameter name="cvv" type="string" required=false %}
Security code \(CVV/CVC\) to be tokenized
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
You receive a credit card token \(aliasCC\) and CVV token \(aliasCVV\).
{% endapi-method-response-example-description %}

```markup
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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid value passed for one of the attributes \(e.g. merchantId\).
{% endapi-method-response-example-description %}

```markup
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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

| XSD schema | [https://api.sandbox.datatrans.com/upp/schema/aliasCC.xsd](https://api.sandbox.datatrans.com/upp/schema/aliasCC.xsd) |
| :--- | :--- |


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
```markup
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
```markup
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
```markup
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

| errorCode | errorMessage | Explanation |
| :--- | :--- | :--- |
| 1004 | CC number not valid | Luhn check failed |
| 2000 | access denied | XML alias service not enabled by Datatrans |
| 2001 | no input document | Request body does not contain XML payload |
| 2002 | error building document | Wrong XML payload in request |
| 2011 | root element invalid | Root element is not `<aliasCCService>` |
| 2012 | body element missing | `<body>` element in request is missing |
| 2013 | merchantId missing | `<body>` element does not have a merchantId attribute |
| 2014 | element missing | Element is missing. For example `<alias>` |
| 2022 | invalid value | Invalid value passed for an attribute. \(e.g. `merchantId`\) |
| -889 | CC-alias error | Input paramter\(s\) missing. For example `<cardno>` |

## Next up

{% page-ref page="../use-stored-cards/" %}



