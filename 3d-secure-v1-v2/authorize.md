---
description: Authorize transactions which are alrady authenticated.
---

# Authorize

If you processed authentication only through either [Secure Fields](securefields-1/) or [3D API](api-beta.md), this API can be called to authorize the amount against your acquiring contract. 

{% hint style="info" %}
* This service requires basic authentication. The password can be found in the [Web Admin Tool](https://admin.sandbox.datatrans.com/) under _UPP Administration &gt; Security &gt; Server-to-Server services security_.
* Make sure to use our 3D Secure enabled test credit cards [here](testing-3d-secure.md).
{% endhint %}

### 1. Add acquirer to your account

| You can choose from a list of [**Supported Acquirer**](../resources/supported-acquirer.md) and contact us at [setup@pci-proxy.com](mailto:setup@pci-proxy.com) |
| :--- |


{% hint style="warning" %}
For this feature, you need an existing acquiring contract.
{% endhint %}

### 2. Authorize a stored card

{% api-method method="post" host="https://api.sandbox.datatrans.com" path="/upp/jsp/XML\_authorize.jsp" %}
{% api-method-summary %}
Authorize
{% endapi-method-summary %}

{% api-method-description %}
Authorize transactions which are alrady authenticated.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Basic MTAwMDAxMTAxMTpYMWVXNmkjJA==   
see Setup
{% endapi-method-parameter %}

{% api-method-parameter name="Content-Type" type="string" required=true %}
API consumes application/xml; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="merchantId" type="string" required=true %}
Your unique account id at PCI Proxy \(e.g. 1000011011\)
{% endapi-method-parameter %}

{% api-method-parameter name="refno" type="string" required=true %}
Your unique reference number \(AN20\)
{% endapi-method-parameter %}

{% api-method-parameter name="amount" type="string" required=true %}
Transaction amount in smallest unit \(e.g. 123.50 = 12350\)
{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
Transaction currency - ISO character code \(e.g. EUR\)
{% endapi-method-parameter %}

{% api-method-parameter name="aliasCC" type="string" required=true %}
Credit card token \(AN20\)
{% endapi-method-parameter %}

{% api-method-parameter name="aliasCVV" type="string" required=false %}
CVV token \(base64\)
{% endapi-method-parameter %}

{% api-method-parameter name="expm" type="integer" required=true %}
Expiration month \(MM\)
{% endapi-method-parameter %}

{% api-method-parameter name="expy" type="integer" required=true %}
Expiration year \(YY\)
{% endapi-method-parameter %}

{% api-method-parameter name="eci" type="string" required=true %}
`eci` parameter of `3D` object returned in `/v1/transactions/{transactionId}` call
{% endapi-method-parameter %}

{% api-method-parameter name="xid" type="string" required=true %}
`xid` parameter of `3D` object returned in `/v1/transactions/{transactionId}` call
{% endapi-method-parameter %}

{% api-method-parameter name="cavv" type="string" required=true %}
`cavv` parameter of `3D` object returned in `/v1/transactions/{transactionId}` call
{% endapi-method-parameter %}

{% api-method-parameter name="enrolled" type="string" required=true %}
`directoryResponse` parameter of `3D` object returned in `/v1/transactions/{transactionId}` call 
{% endapi-method-parameter %}

{% api-method-parameter name="status\_3d" type="string" required=true %}
`authenticationResponse` parameter of `3D` object returned in `/v1/transactions/{transactionId}` call 
{% endapi-method-parameter %}

{% api-method-parameter name="version\_3d" type="string" required=true %}
`threeDSVersion` parameter of `3D` object returned in `/v1/transactions/{transactionId}` call
{% endapi-method-parameter %}

{% api-method-parameter name="sign" type="string" required=true %}
Your security sign - see Setup
{% endapi-method-parameter %}

{% api-method-parameter name="reqtype" type="string" required=false %}
`NOA` - Authorisation only \(default\)  
`CAA` - Authorisation and settlement
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Transaction successfully authorized
{% endapi-method-response-example-description %}

```javascript

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
In test mode, only [test credit cards](../test-card-data.md) are allowed.
{% endhint %}

### Examples

{% tabs %}
{% tab title="Reserve amount \(authorize\)" %}
To reserve an amount, simply send an authorization request with an amount \(`amount=1000`\):

{% code title="Reserve" %}
```bash
curl -X POST \
  https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp \
  -H 'Authorization: Basic MTEwMDAxNzc4OTpueG9ndnJPdGJScFhIUTFB' \
  -d '<authorizationService version="4">
   <body merchantId="1100017789">
     <transaction refno="bsc-test">
       <request>
         <amount>1000</amount>
         <currency>EUR</currency>
         <aliasCC>520000RIVWAS0080</aliasCC>
         <expm>12</expm>
         <expy>21</expy>
         <aliasCVV>PxZw66K5Ssq3RKZWL_JHLOTO</aliasCVV>
         <parameters_3d>
           <eci>02</eci>
           <xid>MDAxOTA4MDkxNjMzMDkzNTUwMDQ=</xid>
           <cavv>OTkxOTA4MDkxNjMzMTYwNTUwMzY=</cavv>
           <enrolled>Y</enrolled>
           <status_3d>Y</status_3d>
           <version_3d>2.1.0</version_3d>
         </parameters_3d>
         <sign>190411090116949280</sign>
       </request>
     </transaction>
   </body>
 </authorizationService>'
```
{% endcode %}

{% code title="Response \(successful\)" %}
```markup
<authorizationService version='4'>
    <body merchantId='1100017789' status='accepted'>
        <transaction refno='bsc-test' trxStatus='response'>
            <response>
                <responseCode>01</responseCode>
                <responseMessage>Authorized</responseMessage>
                <uppTransactionId>190809164624026430</uppTransactionId>
                <authorizationCode>624066431</authorizationCode>
                <acqAuthorizationCode>164624</acqAuthorizationCode>
                <maskedCC>520000xxxxxx0080</maskedCC>
            </response>
        </transaction>
    </body>
</authorizationService>
```
{% endcode %}

{% code title="Response \(insufficient limit\)" %}
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
{% endcode %}

{% code title="Response \(card blocked\)" %}
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
{% endcode %}
{% endtab %}

{% tab title="Charge amount \(auth+settle\)" %}
To charge a stored card, simply send an authorization request with `reqtype=CAA`:

{% code title="Charge" %}
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
{% endcode %}

{% code title="Response \(successful\)" %}
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
{% endcode %}

{% code title="Response \(insufficient limit\)" %}
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
{% endcode %}

{% code title="Response \(card blocked\)" %}
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
{% endcode %}
{% endtab %}
{% endtabs %}

#### Additional return parameter

If the authorization was successful, you will additionally receive the following parameter:

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `responseCode` | N2 | 01 or 02 for a successful transaction |
| `responseMessage` |  | Authorisation response message text |
| `uppTransactionId` | N18 | Unique transaction identifier assigned by Datatrans |
| `authorizationCode` | N9 | Outdated; internal reference ID assigned by Datatrans; please ignore and use uppTransactionId instead |
| `acqAuthorizationCode` | AN7 | Authorisation code returned by the acquirer |
| `maskedCC` |  | Masked credit card number, which can be stored in your system. |

If the authorization failed, you will additionally receive the following error parameter:

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `errorCode` | N7 | Error code, please refer to the [Technical Implementation Guide](https://pilot.datatrans.biz/showcase/doc/Technical_Implementation_Guide.pdf) for the response code list |
| `errorMessage` |  | Error text |
| `errrorDetail` |  | Description of error detail |
| `uppTransactionId` | N18 | Unique transaction identifier assigned by Datatrans |
| `acqErrorCode` | AN7 | Error code returned by the acquirer |



