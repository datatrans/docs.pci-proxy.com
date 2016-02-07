# Charge payment data against payment gateways

The authorization request needs to be sent as an XML formatted message via a https request to Datatrans. After
the request is validated, the merchant will receive an XML formatted response message which contains all
necessary information about the transaction. 

API Endpoint:
`https://pilot.datatrans.biz/upp/jsp/XML_authorize.jsp`

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