---
description: Check or charge a stored credit card.
---

# Authorize

You can simply send an XML request with a token to check, reserve an amount, or charge a stored card.

{% hint style="warning" %}
_For this feature, you need an existing acquiring contract. Please see our _[_**Supported Acquirer**_](../resources/supported-acquirer.md)_._
{% endhint %}

## 1. Add acquirer to your account

| You can choose from a list of [**Supported Acquirer**](../resources/supported-acquirer.md) and contact us at [setup@pci-proxy.com](mailto:setup@pci-proxy.com) |
| :--- |


## 2. Authorize a stored card

When you authorize a stored credit card, you can choose between different process options:

{% tabs %}
{% tab title="Check validity" %}
When you [**check a stored card**](charge.md#examples), we run your query against the Visa & Mastercard network to check if the card is still valid. The authorization does not appear on the customer statement but still gives you the ability to test the validity of a stored credit card.
{% endtab %}

{% tab title="Reserve an amount" %}
When you [**reserve an amount**](charge.md#examples) on a stored card, the monthly allowance of the cardholder is reduced by the authorised amount, no matter whether the transaction will be settled later or not. The authorised amount is reserved for the merchant and should be settled within the period agreed with the acquirer. The issuer returns an authorisation code which serves as the reference of the authorisation. Once a transaction has been successfully authorised it can be settled.

**Important:** the cardholder will not be charged without settlement. Authorisation and settlement can also be processed in one single step \(see Charge amount\).
{% endtab %}

{% tab title="Charge cardholder" %}
When you [**charge a stored card**](charge.md#examples), the authorization and settlement will be processed in one single step. The settlement is often also referred to as “capture” or “clearing”. Once you sent a charge request, the authorized amount is reduced from the monthly allowance of the cardholder and will be automatically settled, which means that the cardholder will be actually charged.
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Stored cards can be used multiple times for **recurring transactions** or **One-Click payments**. 
{% endhint %}

{% api-method method="post" host="https://pilot.datatrans.biz" path="/upp/jsp/XML\_authorize.jsp" %}
{% api-method-summary %}
AUTH method
{% endapi-method-summary %}

{% api-method-description %}
The AUTH method allows you to authorize a stored credit card.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=false %}
Basic MTEwMDAwNzAwNjpLNnFYMXUkIQ==  
see 

[Setup](../setup/)
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=false %}
API consumes application/xml
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="merchantId" type="string" required=true %}
Your unique account id at PCI Proxy \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="string" required=true %}
Transaction amount in smallest unit \(e.g. 123.50 = 12350\)
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
Transaction currency – ISO character code \(EUR, etc.\)
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
Your unique reference number \(AN18\)
{% endapi-method-parameter %}

{% api-method-parameter name="aliasCC" type="string" required=true %}
Credit card token \(AN20\)
{% endapi-method-parameter %}

{% api-method-parameter name="aliasCVV" type="string" required=false %}
CVV token for CVV code \(base64\)
{% endapi-method-parameter %}

{% api-method-parameter name="expm" type="string" required=true %}
Expiration month \(MM\)
{% endapi-method-parameter %}

{% api-method-parameter name="expy" type="string" required=true %}
Expiration year \(YY\)
{% endapi-method-parameter %}

{% api-method-parameter name="uppCustomerIpAddress" type="string" required=false %}
Customer’s IP address \(source IP used by cardholder\)
{% endapi-method-parameter %}

{% api-method-parameter name="sign" type="string" required=false %}
Your security sign  
see 

[Setup](../setup/#create-security-sign)
{% endapi-method-parameter %}

{% api-method-parameter name="reqtype" type="string" required=false %}
_NOA_ – Authorisation only \(default\)  
_CAA_ – Authorisation and settlement
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Successful authorization response
{% endapi-method-response-example-description %}

```markup
<?xml version=”1.0” encoding=”UTF-8”?> 
    <authorizationService version=”2”> 
        <body merchantId=”1000011011” status=”accepted”> 
            <transaction refno=”1234987” trxStatus=”response”> 
                <request> 
                    <amount>1000</amount> 
                    <currency>CHF</currency> 
                    <aliasCC>424242SKMPRI4242</aliasCC> 
                    <expm>12</expm> 
                    <expy>15</expy> 
                    <uppCustomerDetails> 
                        <uppCustomerIpAddress>192.168.100.13</uppCustomerIpAddress> 
                    </uppCustomerDetails> 
                    <sign>30916165706580013</sign> 
                    <reqtype>NOA</reqtype> 
                </request> 

                <response> 
                    <responseCode>01</responseCode> 
                    <responseMessage>Authorized</responseMessage> 
                    <uppTransactionId>140813153050582536</uppTransactionId> 
                    <authorizationCode>950672542</authorizationCode> 
                    <acqAuthorizationCode>153050</acqAuthorizationCode> 
                    <maskedCC>375811xxxxx1115</maskedCC> 
                </response> 
            </transaction> 
        </body> 
    </authorizationService>
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
 Failed authorization response  
{% endapi-method-response-example-description %}

```markup
<?xml version=”1.0” encoding=”UTF-8”?> 
    <authorizationService version=”2”> 
        <body merchantId=”1000011011” status=”accepted”> 
            <transaction refno=”1234987” trxStatus=”response”> 
                <request> 
                    <amount>1000</amount> 
                    <currency>CHF</currency> 
                    <aliasCC>424242SKMPRI4242</aliasCC> 
                    <expm>12</expm> 
                    <expy>15</expy> 
                    <uppCustomerDetails> 
                        <uppCustomerIpAddress>192.168.100.13</uppCustomerIpAddress> 
                    </uppCustomerDetails> 
                    <sign>30916165706580013</sign> 
                    <reqtype>NOA</reqtype> 
                </request> 

                <error>
                    <errorCode>1403</errorCode>
                    <errorMessage>declined</errorMessage>
                    <errorDetail>Declined</errorDetail>
                    <uppTransactionId>140813155837703945</uppTransactionId>
                    <acqErrorCode>50</acqErrorCode>
                </error>
            </transaction> 
        </body> 
    </authorizationService>
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Examples

{% tabs %}
{% tab title="Check validity \(zeroAuth\)" %}
To check a stored card, simply send an authorization request with `amount=0`:

{% code-tabs %}
{% code-tabs-item title="Check" %}
```bash
curl https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp \
-H "Content-Type: application/xml" \
-d '<?xml version="1.0" encoding="UTF-8" ?>
           <authorizationService version="2">
               <body merchantId="1000011011">
                   <transaction refno="123abc">
                       <request>
                           <amount>0</amount>
                           <currency>CHF</currency>
                           <aliasCC>424242SKMPRI4242</aliasCC>
                           <expm>12</expm>
                           <expy>18</expy>
                           <sign>30916165706580013</sign>
                       </request>
                   </transaction>
               </body>
           </authorizationService>'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(card valid\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='response'>
      <request>
        <amount>0</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>NOA</reqtype>
      </request>
      <response>
        <responseCode>01</responseCode>
        <responseMessage>Authorized</responseMessage>
        <uppTransactionId>180413155912441269</uppTransactionId>
        <authorizationCode>912491270</authorizationCode>
        <acqAuthorizationCode>155912</acqAuthorizationCode>
        <maskedCC>424242xxxxxx4242</maskedCC>
        <cardnumber>4242424242424242</cardnumber>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </response>
    </transaction>
  </body>
</authorizationService>%
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(card not valid\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='error'>
      <request>
        <amount>9100</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>NOA</reqtype>
      </request>
      <error>
        <errorCode>1403</errorCode>
        <errorMessage>declined</errorMessage>
        <errorDetail>Declined</errorDetail>
        <uppTransactionId>180413160820154027</uppTransactionId>
        <acqErrorCode>50</acqErrorCode>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </error>
    </transaction>
  </body>
</authorizationService>
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}

{% tab title="Reserve amount \(authorize\)" %}
To reserve an amount, simply send an authorization request with an amount \(`amount=1000`\):

{% code-tabs %}
{% code-tabs-item title="Reserve" %}
```bash
curl https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp \
-H "Content-Type: application/xml" \
-d '<?xml version="1.0" encoding="UTF-8" ?>
           <authorizationService version="2">
               <body merchantId="1000011011">
                   <transaction refno="123abc">
                       <request>
                           <amount>1000</amount>
                           <currency>CHF</currency>
                           <aliasCC>424242SKMPRI4242</aliasCC>
                           <expm>12</expm>
                           <expy>18</expy>
                           <sign>30916165706580013</sign>
                       </request>
                   </transaction>
               </body>
           </authorizationService>'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(successful\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='response'>
      <request>
        <amount>1000</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>NOA</reqtype>
      </request>
      <response>
        <responseCode>01</responseCode>
        <responseMessage>Authorized</responseMessage>
        <uppTransactionId>180413160435542994</uppTransactionId>
        <authorizationCode>435582995</authorizationCode>
        <acqAuthorizationCode>160435</acqAuthorizationCode>
        <maskedCC>424242xxxxxx4242</maskedCC>
        <cardnumber>4242424242424242</cardnumber>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </response>
    </transaction>
  </body>
</authorizationService>
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(insufficient limit\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='error'>
      <request>
        <amount>9100</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>NOA</reqtype>
      </request>
      <error>
        <errorCode>1403</errorCode>
        <errorMessage>declined</errorMessage>
        <errorDetail>Declined</errorDetail>
        <uppTransactionId>180413160820154027</uppTransactionId>
        <acqErrorCode>50</acqErrorCode>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </error>
    </transaction>
  </body>
</authorizationService>
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(card blocked\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='error'>
      <request>
        <amount>12000</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>NOA</reqtype>
      </request>
      <error>
        <errorCode>1404</errorCode>
        <errorMessage>card blocked</errorMessage>
        <errorDetail>Declined - card blocked</errorDetail>
        <uppTransactionId>180413161144544837</uppTransactionId>
        <acqErrorCode>42</acqErrorCode>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </error>
    </transaction>
  </body>
</authorizationService>
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}

{% tab title="Charge amount \(auth+settle\)" %}
To charge a stored card, simply send an authorization request with `reqtype=CAA`:

{% code-tabs %}
{% code-tabs-item title="Charge" %}
```bash
curl https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp \
-H "Content-Type: application/xml" \
-d '<?xml version="1.0" encoding="UTF-8" ?>
           <authorizationService version="2">
               <body merchantId="1000011011">
                   <transaction refno="123abc">
                       <request>
                           <amount>1000</amount>
                           <currency>CHF</currency>
                           <aliasCC>424242SKMPRI4242</aliasCC>
                           <expm>12</expm>
                           <expy>18</expy>
                           <sign>30916165706580013</sign>
                           <reqtype>CAA</reqtype>
                       </request>
                   </transaction>
               </body>
           </authorizationService>'
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(successful\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='response'>
      <request>
        <amount>1000</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>CAA</reqtype>
      </request>
      <response>
        <responseCode>01</responseCode>
        <responseMessage>Authorized</responseMessage>
        <uppTransactionId>180413160338192663</uppTransactionId>
        <authorizationCode>338242664</authorizationCode>
        <acqAuthorizationCode>160338</acqAuthorizationCode>
        <maskedCC>424242xxxxxx4242</maskedCC>
        <cardnumber>4242424242424242</cardnumber>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </response>
    </transaction>
  </body>
</authorizationService>% 
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(insufficient limit\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='error'>
      <request>
        <amount>9100</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>CAA</reqtype>
      </request>
      <error>
        <errorCode>1403</errorCode>
        <errorMessage>declined</errorMessage>
        <errorDetail>Declined</errorDetail>
        <uppTransactionId>180413161627985895</uppTransactionId>
        <acqErrorCode>50</acqErrorCode>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </error>
    </transaction>
  </body>
</authorizationService>
```
{% endcode-tabs-item %}

{% code-tabs-item title="Response \(card blocked\)" %}
```markup
<?xml version='1.0' encoding='UTF-8'?>
<authorizationService version='2'>
  <body merchantId='1000011011' status='accepted'>
    <transaction refno='123abc' trxStatus='error'>
      <request>
        <amount>12000</amount>
        <currency>CHF</currency>
        <aliasCC>424242SKMPRI4242</aliasCC>
        <expm>12</expm>
        <expy>18</expy>
        <sign>30916165706580013</sign>
        <reqtype>CAA</reqtype>
      </request>
      <error>
        <errorCode>1404</errorCode>
        <errorMessage>card blocked</errorMessage>
        <errorDetail>Declined - card blocked</errorDetail>
        <uppTransactionId>180413162049417343</uppTransactionId>
        <acqErrorCode>42</acqErrorCode>
        <returnCustomerCountry>CHE</returnCustomerCountry>
      </error>
    </transaction>
  </body>
</authorizationService>
```
{% endcode-tabs-item %}
{% endcode-tabs %}
{% endtab %}
{% endtabs %}

#### Additional return parameter

If the authorization was successful, you will additionally receive the following parameter:

| Parameter | Type | Description |
| --- | --- | --- |
| `responseCode` | N2 | 01 or 02 for a successful transaction |
| `responseMessage` |  | Authorisation response message text |
| `uppTransactionId` | N18 | Unique transaction identifier assigned by Datatrans |
| `authorizationCode` | N9 | Outdated; internal reference ID assigned by Datatrans; please ignore and use uppTransactionId instead |
| `acqAuthorizationCode` | AN7 | Authorisation code returned by the acquirer |
| `maskedCC` |  | Masked credit card number, which can be stored in your system. |

If the authorization failed, you will additionally receive the following error parameter:

| Parameter | Type | Description |
| --- | --- | --- |
| `errorCode` | N7 | Error code, please refer to the [Technical Implementation Guide](https://pilot.datatrans.biz/showcase/doc/Technical_Implementation_Guide.pdf) for the response code list |
| `errorMessage` |  | Error text |
| `errrorDetail` |  | Description of error detail |
| `uppTransactionId` | N18 | Unique transaction identifier assigned by Datatrans |
| `acqErrorCode` | AN7 | Error code returned by the acquirer |

