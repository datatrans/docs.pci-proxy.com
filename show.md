# Show single credit cards

Let us assume you have authorized employees that need to see the original payment data set of a customer.

PCI Proxy enables you to manually retrieve single payment data sets. Basically, it is `a web interface that can convert a token back into its original payment data`. (e.g. to charge a credit card via POS terminal). 



## How to start

There are two ways how you can show single payment data:

| **Datatrans Web Admin Tool** | **Integration into your application** |
| -- | -- |
| You can use our Web Admin Tool and let PCI Proxy handle the user access. | You can use our *NoShow.jsp* script and integrate this feature seamlessly into your application.|

*Note: Even though the interface is served by PCI Proxy, your PCI scope can extend.*





## 1. Using our Web Admin Tool

Simply log into our [Web Admin Tool](https://pilot.datatrans.biz/) and go under *"Book Entries" / "Alias"*.


## 2. Seamless interface integration (NoShow.jsp)

Another way of showing single payment data is by using our *NoShow.jsp *script. You can implement it directly into your application. It offers a more seamless approach and can be embedded as iframe or by redirect.

 To see the interface in action, click the following link, prefilled with:
 

> [**No-Show Interface**](https://pilot.datatrans.biz/upp/jsp/noShow.jsp?merchantId=1100005048&aliasCC=70119122433810042&salt=xUWnv6TR0RqUyPsVWvxgUn0wXKCuPJjWAumgTy67TVUsimiL0V&sign=df9ed6edb62df004ce64db6c113038aa21bd769d866ca7cf305bf43610ce6232)

The token *70119122433810042* should result in test card number *4242424242424242*


**Consider a business that needs this ability:**
*You are a travel technology company providing hotels with software to manage their reservations. Authorized hotel employees need to retrieve single payment data sets from reservations to book a no-show fee with their POS terminal if a guest does not show up.*

### Quick Start Guide:

1. Embed interface as iframe or redirect into your application.
2. Ensure PCI DSS compliant user management.


| **No-Show interface endpoint:** |
| -- |
| https://pilot.datatrans.biz/upp/jsp/noShow.jsp |

- **Required parameter:**


| Parameter      | Description                                                        | Example value
| -------------- | -------------------------------------------------------------------| ---
| `merchantId` | Your merchant ID | 1000011011
| `aliasCC` | Token you received upon payment data collection | 70119122433810042
| `username` | Username of authorized employee who retrieves it| max.mustermann
| `sign` | SHA Hash - Hash converted to hexaDecimalString | SHA.256(salt+merchantId+aliasCC)
| `language` | The language code in which the no-show page should be displayed  | en
            
*The „**salt**“ value has to be generated in the Datatrans web administration tool (http://pilot.datatrans.biz) under “UPP Administration” -> “Security” -> “Other Services”.*

- **Example:**

```java
    https://pilot.datatrans.biz/upp/jsp/noShow.jsp
            ?merchantId=1100005048
            &aliasCC=70119122433810042
            &sign=df9ed6edb62df004ce64db6c113038aa21bd769d866ca7cf305bf43610ce6232

```

### PCI DSS Compliant User Management

Using our *NoShow.jsp* script requires you to handle your user management in a PCI DSS compliant way. PCI DSS requires certain user and password policies. Below you will find a comprehensive overview for a PCI DSS compliant user management. For a more detailed version on PCI DSS user management please see the official PCI DSS documents.

#### Unique User IDs

Every single user having access to the No-Show.jsp needs to have a unique user login to be clearly identified. Shared user logins are not allowed. 

#### Password Policy

In general, the following password rules have to be observed:

 - Passwords must be changed at least every 90 days.
 - The password must have a minimum length of 8 characters.
 - The password must contain upper and lower case letters, numbers and at least one special character.
 - When changing the password none of the last four passwords can be used.
 - After 6 failed login attempts a user account is locked. It can only be unlocked by the administrator.
 - After 15 minutes of inactivity, the password must be entered to reactivate the terminal / session.
 - The maximum session time after which the user must log in again must not exceed 200 minutes.


