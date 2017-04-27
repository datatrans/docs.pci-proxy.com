# Quickstart: Charge stored card with Datatrans' Payment gateway

Lets assume you want to authorize or settle an amount on the payment data that you have collected earlier.

You can simply `send an XML request with a token to charge the stored card.`

> _For this feature, you need an existing acquiring contract. Please see our list of _[_**Supported Acquirer**_](/supported_acquirer.md)_._

| Charge an amount | Reserve an amount | Recur transaction |
| :--- | :--- | :--- |
| Make a payment against a stored credit card. | Block an amount on a stored credit card. | Reuse stored credit card data for recurring transactions or One-Click payments. |

---

## 1. Add an Acquirer to your Account

You can choose from a list of [**Supported Acquirer**](/supported_acquirer.md).

| Contact us at [setup@pci-proxy.com](/mailto:setup@pci-proxy.com) |
| :--- |


---

## 2. Charge a stored credit card

If you have added an Acquirer to your account, you can either use the Payment Page or a Server-to-Server request to charge a token.

### via Payment Page

When using the Payment Page , all possible input fields are getting pre-filled. See example:

| [Charge stored credit card via Payment Page](https://pay.sandbox.datatrans.com/upp/jsp/upStart.jsp?theme=DT2015&merchantId=1100004624&amount=1337&currency=CHF&refno=123456789&sign=30916165706580013&paymentmethod=VIS&aliasCC=70119122433810042&expm=12&expy=18&language=en) |
| :--- |


In the example above the CVV code for the payment method \(VIS\) is mandatory. The payment page is getting pre-filled with the masked credit card number and the expiry date only. The cardholder is asked to enter the CVV code only for a simplified payment process.

Open the following URL with parameters:

```js
https://pay.sandbox.datatrans.com/upp/jsp/upStart.jsp            // HOST: Payment Page Endpoint
                ?theme=DT2015                                
                &merchantId=1100004624                       // Merchant ID you received at adding a Acquirer
                &amount=1337                                 // Specify the amount you want to authorize
                &currency=CHF                                // Specify currency in which you want to charge
                &refno=123456789                             // Unique ID for reference - assigned by you
                &sign=30916165706580013                      // Security Sign you created in Step 1
                &paymentmethod=VIS                           // Specify the payment method you want to charge
                &aliasCC=424242SKMPRI4242                    // CC token to identify stored credit card number
                &aliasCVV=LfDiiolgQ86kRSyNEXyx8jwU           // CVV token to identify stored CVV code
                &expm=12                                     // Expiry Month of stored credit card
                &expy=18                                     // Expiry Year of stored credit card
                &language=en                                 // Define language in which Payment Page should be opened
```

### via Server-to-Server Request \(One-Click Checkout\)

Send an XML request to Datatrans' XML Gateway Endpoint by using the following call:

```js
$ curl "https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp"         // HOST: XML Gateway Endpoint
        -H "Content-Type: application/xml"                             // Content-Type: application/xml

        -d '<?xml version="1.0" encoding="UTF-8" ?>                    // We expect an XML formatted message       
                <authorizationService version="2">                     
                    <body merchantId="1000011011">                     // Merchant ID you received at adding a Acquirer
                        <transaction refno="123abc">                   // Unique ID for reference - assigned by you
                            <request>                                  
                                <amount>1000</amount>                  // Specify the amount you want to authorize
                                <currency>CHF</currency>               // Specify currency in which you want to charge
                                <aliasCC>424242SKMPRI4242</aliasCC>    // CC token to identify stored credit card
                                <aliasCVV>xxx</aliasCVV>               // CV token to identify stored CVV code
                                <expm>12</expm>                        // Expiry Month of stored credit card
                                <expy>15</expy>                        // Expiry Year of stored credit card
                                <sign>30916165706580013</sign>         // Security Sign you created in Step 1
                            </request>
                        </transaction>
                    </body>
                </authorizationService>'
```

---

#### Reference

The authorization request needs to be sent as an XML formatted message via a https request to Datatrans endpoint.

| ** XML Gateway Endpoint:** |
| --- |
| [https://api.sandbox.datatrans.com/upp/jsp/XML\_authorize.jsp](https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp) |

| Mandatory Input Parameter | Type | Description |
| --- | --- | --- |
| `merchantId` | N10 | Your merchant ID or merchant ID of your customer |
| `amount` | N | Transaction amount in the smallest available unit |
| `currency` | A3 | Transaction currency – ISO character code \(CHF, EUR, USD etc.\) |
| `refno` | AN18 | Unique reference number assigned by you |
| `aliasCC` | AN20 | CC token for credit card number, Postfinance or PayPal |
| `aliasCVV` |  | CVV token for CVV code |
| `expm` | MM | Expiration month \(for credit card only\) |
| `expy` | YY | Expiration year \(for credit card only\) |

| Optional Input Parameter | Type | Description |
| --- | --- | --- |
| `uppCustomerIpAddress` |  | Customer’s IP address \(source IP used by the cardholder\) |
| `sign` |  | Your security sign |
| `reqtype` |  | _NOA_ – Authorisation only \(default\) or _CAA_ – Authorisation and settlement |

##### Successful Authorisation

If the authorization was successful, you will additionally receive the following parameter:

| Parameter | Type | Description |
| --- | --- | --- |
| `responseCode` | N2 | 01 or 02 for a successful transaction |
| `responseMessage` |  | Authorisation response message text |
| `uppTransactionId` | N18 | Unique transaction identifier assigned by Datatrans |
| `authorizationCode` | N9 | Outdated; internal reference ID assigned by Datatrans; please ignore and use uppTransactionId instead |
| `acqAuthorizationCode` | AN7 | Authorisation code returned by the acquirer |
| `maskedCC` |  | Masked credit card number, which can be stored in your system. |

Example of successful authorization response:

```js
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

##### Failed Authorization

If the authorization failed, you will additionally receive the following error parameter:

| Parameter | Type | Description |
| --- | --- | --- |
| `errorCode` | N7 | Error code, please refer to the [Technical Implementation Guide](https://pilot.datatrans.biz/showcase/doc/Technical_Implementation_Guide.pdf) for the response code list |
| `errorMessage` |  | Error text |
| `errrorDetail` |  | Description of error detail |
| `uppTransactionId` | N18 | Unique transaction identifier assigned by Datatrans |
| `acqErrorCode` | AN7 | Error code returned by the acquirer |

Example of failed authorization response:

```js
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

---

> ### Great job**: You have successfully integrated PCI Proxy! **
>
> You have securely charged a stored credit card without ever touching your servers. **Your systems never record, transmit or store real credit card data, only the token. Thus, you are out of PCI scope. **
>
> Enjoy PCI compliance in a risk-free environment. Keep in mind that you can use stored data as often as you need it.
>
> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



