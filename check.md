# Quickstart: Check validity of stored cards

After collecting credit cards, you might want to check the validity of credit cards.

Therefore, simply send a zero-amount authorization request against our XML gateway endpoint. The authorization does not appear on the customer statement but still gives you the abillity to test the validity of a credit card.

---

## 1. Check validity of a stored card

Send a zero-amount authorization request to Datatrans' XML Gateway Endpoint by using the following call:

```js
$ curl "https://pilot.datatrans.biz/upp/jsp/XML_authorize.jsp"         // HOST: XML Gateway Endpoint
        -H "Content-Type: application/xml"                             // Content-Type: application/xml

        -d '<?xml version="1.0" encoding="UTF-8" ?>                    // We expect an XML formatted message       
                <authorizationService version="3">                     
                    <body merchantId="1000011011">                     // Merchant ID you received at adding a Acquirer
                        <transaction refno="107988">                   // Unique ID for reference - assigned by you
                            <request>                                  
                                <amount>0</amount>                     // Specify the amount you want to authorize
                                <currency>CHF</currency>               // Specify currency in which you want to charge
                                <aliasCC>70323122544331174</aliasCC>   // Token to identify stored credit card
                                <expm>12</expm>                        // Expiry Month of stored credit card
                                <expy>18</expy>                        // Expiry Year of stored credit card
                                <sign>30916165706580013</sign>         // Security Sign you created in Step 1
                            </request>
                        </transaction>
                    </body>
                </authorizationService>'
```

---

#### Reference

The zero-amount authorization request needs to be sent as an XML formatted message via a https request to Datatrans endpoint.

| ** XML Gateway Endpoint:** |
| --- |
| [https://pilot.datatrans.biz/upp/jsp/XML\_authorize.jsp](https://pilot.datatrans.biz/upp/jsp/XML_authorize.jsp) |

| Mandatory Input Parameter | Type | Description |
| --- | --- | --- |
| `merchantId` | N10 | Your merchant ID or merchant ID of your customer |
| `amount` | N | Transaction amount, in this case this would be the amount zero = 0 |
| `currency` | A3 | Transaction currency – ISO character code \(CHF, EUR, USD etc.\) |
| `refno` | AN18 | Unique reference number assigned by you |
| `aliasCC` | AN20 | Token for credit card |
| `expm` | MM | Expiration month |
| `expy` | YY | Expiration year |
|  |  |  |

| Optional Input Parameter | Type | Description |
| --- | --- | --- |
| `uppCustomerIpAddress` |  | Customer’s IP address \(source IP used by the cardholder\) |
| `sign` |  | Your security sign |
| `reqtype` |  | _NOA_ – Authorisation only \(default\) or |

##### 

Example of successful card check:

```js
<?xml version=”1.0” encoding=”UTF-8”?> 
    <authorizationService version=”3”> 
        <body merchantId=”1000011011” status=”accepted”> 
            <transaction refno=”107988” trxStatus=”response”> 
                <request> 
                    <amount>0</amount> 
                    <currency>CHF</currency> 
                    <aliasCC>70323122544331174</aliasCC> 
                    <expm>12</expm> 
                    <expy>15</expy> 
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

##### 

> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



