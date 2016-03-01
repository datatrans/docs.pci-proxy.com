# Charge payment data against our payment gateway

Lets assume you want to authorize or settle an amount on the payment data that you have collected earlier. 

You can simply ```send an XML request with a token to charge the payment data behind it```. 

*For this feature, you or your customer needs an existing acquiring contract. We have integrated a list of acquirer you can choose from. If your desired acquirer is not on the list, please get in touch.*

**Consider the following business cases:**

- **Charge an amount** and transact against the collected payment data.

- **Reserve an amount:** Travel companies often receive payment data that is not charged directly. For instance, hotels require payment data from their customers to guarantee a reservation. Hotels can reserve the amount for the stay or simply test the validity of the payment data by authorizing an amount.

- **Recurring billing** is used primarily for charging recurring services such as subscriptions for newspapers or membership fees. The cardholder is not involved in the payment process.

- **One-click checkout:** You want to simplify your checkout for your recurring customers. One-click checkout is a user-friendly way to handle recurring customers because collected data can be charged many times. The customer has to identify himself on your website and register his credit card on his profile.  Recurrent customers do not need to enter card details again to make a payment. They can simply pay with only one click.



## Authorization Request

The authorization request needs to be sent as an XML formatted message via a https request to Datatrans endpoint. Once the request is validated, you receive a XML formatted response which contains all necessary information about the transaction. 

| ** Endpoint:** |
| -- |
| https://pilot.datatrans.biz/upp/jsp/XML_authorize.jsp|

- **Mandatory input parameter:**

| Parameter | Type | Description |
| -- | -- | -- |
| merchantId | N10 | Your merchant ID or merchant ID of your customer |
| amount | N | Transaction amount in the smallest available unit |
| currency | A3 | Transaction currency – ISO character code (CHF, EUR, USD etc.) |
| refno | AN18 | Unique reference number assigned by you|
| aliasCC | AN20 | Alias for credit card, Postfinance or PayPal |
| expm | MM | Expiration month (for credit card only) |
| expy | YY | Expiration year (for credit card only) |


- **Optional input parameter:**

| Parameter | Type | Description |
| -- | -- | -- |
| uppCustomerIpAddress |  | Customer’s IP address (source IP used by the cardholder) |
| sign |  | Your security sign |
| reqtype |  | *NOA* – Authorisation only (default) or *CAA* – Authorisation and settlement |



- **Example of authorization request:**

```XML
    <?xml version="1.0" encoding="UTF-8" ?>
        <authorizationService version="2">
            <body merchantId="1000011011">
                <transaction refno="1234987">
                    <request>
                        <amount>1000</amount>
                        <currency>CHF</currency>
                        <aliasCC>70323122544331174</aliasCC>
                        <expm>12</expm>
                        <expy>15</expy>
                        <sign>30916165706580013</sign>
                    </request>
                </transaction>
            </body>
        </authorizationService>
```

## Response 

All input parameters will be returned. Additionally you will receive parameters, indicating whether the
transaction was successful or not.


### Successful Authorisation

If the authorization was successful, you will additionally receive the following parameter:

| Parameter | Type | Description |
| -- | -- | -- |
| responseCode | N2 | 01 or 02 for a successful transaction |
| responseMessage |  | Authorisation response message text |
| uppTransactionId | N18 | Unique transaction identifier assigned by Datatrans |
| authorizationCode | N9 | Outdated; internal reference ID assigned by Datatrans; please ignore and use uppTransactionId instead |
| acqAuthorizationCode | AN7 | Authorisation code returned by the acquirer |
| maskedCC |  | Masked credit card number, which can be stored in your system. |

- **Example of successful authorization response:**

```XML
    <?xml version=”1.0” encoding=”UTF-8”?>
        <authorizationService version=”2”>
            <body merchantId=”1000011011” status=”accepted”>
                <transaction refno=”1234987” trxStatus=”response”>
                    <request>
                        <amount>1000</amount>
                        <currency>CHF</currency>
                        <aliasCC>70323122544331174</aliasCC>
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
        </authorizationService>```

### Failed Authorization

If the authorization failed, you will additionally receive the following error parameter:

| Parameter | Type | Description |
| -- | -- | -- |
| errorCode | N7 | Error code, please refer to the Technical Implementation Guide for the response code list |
| errorMessage |  | Error text |
| errrorDetail |  | Description of error detail |
| uppTransactionId | N18 | Unique transaction identifier assigned by Datatrans |
| acqErrorCode | AN7 | Error code returned by the acquirer |

- **Example of failed / unsuccessful authorization response:**

```XML
    <?xml version=”1.0” encoding=”UTF-8”?>
        <authorizationService version=”2”>
            <body merchantId=”1000011011” status=”accepted”>
                <transaction refno=”1234987” trxStatus=”error”>
                    <request>
                        <amount>9500</amount>
                        <currency>CHF</currency>
                        <aliasCC>70323122544331174</aliasCC>
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
        </authorizationService>```
