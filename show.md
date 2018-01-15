# Quickstart: Show credit card number of a stored card

PCI Proxy enables you to see the original credit card number of a stored credit card. Basically, it is `a web interface that can convert a token back into its original credit card number`.

**Consider a business that needs this ability:**  
_You are a travel technology company providing hotels with software to manage their reservations. Authorized hotel employees need to retrieve single credit cards from reservations to book a no-show fee with their POS terminal if a guest does not show up._

There are two ways how you can show single credit cards:

| **Datatrans Web Admin Tool** | **NoShow.jsp integration into your application** |
| --- | --- |
| You can use our Web Admin Tool and let PCI Proxy handle the user access. | You can use our _NoShow.jsp_ script and integrate this feature seamlessly into your application. |

_Note: Even though the interface is served by PCI Proxy, your PCI scope can extend._

---

## 1a. Show a credit card number via Web Admin tool

Simply log into our [Web Admin Tool](https://pilot.datatrans.biz/) and go under _"Process" / "Inverse Alias"_.

## 1b. Show a credit card number via NoShow.jsp

| PCI Proxy NoShow Endpoint |
| :--- |
| [https://api.sandbox.datatrans.com/upp/services/v1/noshow/init](https://api.sandbox.datatrans.com/upp/services/v1/noshow/init) |

1. **Let us know your IP address for whitelisting**

2. **Use **`PCI Proxy NoShow Endpoint`** as **`Host`** with following parameter **`merchantId`**, **`aliasCC`**, **[`sign`](#sign)** and **`userEmail`** to retrieve NoShow link**

```js
curl -X POST https://api.sandbox.datatrans.com/upp/services/v1/noshow/init \
  -H 'content-type: application/xml' \
  -d '<request>
        <merchantId>1000011011</merchantId>
        <aliasCC>70119122433810042</aliasCC>
        <sign>d17ead827458e3532fd868b3b110671586b7e7ee0db106d5ae94e85ca93782ab</sign>
        <userEmail>email@example.com</userEmail>
     </request>'
```

**3. Embed the NoShow Link from the response into your application.**

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<response>
  <url>https://api.sandbox.datatrans.com/upp/noshow?token=27cfba38-a606-49c0-9f03-c3bc6d580a66</url>
  <errorCode>0</errorCode>
</response>
```

**4. Once the user clicks the link an iFrame will be opened where the user have to enter a six digits alphanumeric code which will be sent by email  to **`userEmail`![](/assets/Unbenannt.JPG)

Example link, pre-filled with token 424242SKMPRI4242_:_

| **Click to **[**Show Credit Card Number**](https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp?merchantId=1100005007&aliasCC=424242SKMPRI4242&aliasCVV=&sign=428dd59d048d78144a0def92a27b934f7bb39138161baf482ae2deb95c1741f5) |
| :--- |
| The NoShow link should retrieve the [test card number](/sandbox-environment.md) 4242 4242 4242 4242. |

##### 

> Need more help? Check out our [**NoShow example script**](https://datatrans.github.io/docs.pci-proxy.com/no-show.html).

##### 4**. Optional: Add JavaScript callbacks/hooks**

```js
// Use attached Javascript callsbacks/hooks file to see which events are getting emitted to the parent frame.
// Bind an event listener to the parent frame to listen for those events:

function messageReceived(message) {
  console.log(message.data);
}

if(window.addEventListener)
  window.addEventListener("message",messageReceived);
else
if(window.attachEvent)
  window.attachEvent("message",messageReceived);
else
  console.log("Could not listen.")

/*
    Possible event messages:
    {type: 'error',     reason: 'wrong request'}        Invalid merchant id, alias or sign
    {type: 'error',     reason: 'service not allowed'}  Merchant not configured
    {type: 'error',     reason: 'fraud check 3082'}     Declined by fraud check
    {type: 'error',     reason: 'system error'}         System error
    {type: 'error',     reason: 'invalid sign'}         Invalid sign
    {type: 'error',     reason: 'time expired'}         The user did not enter the chaptcha in less than 90 seconds
    {type: 'error',     reason: 'wrong captcha'}        The entered captcha was wrong
    {type: 'error',     reason: 'invalid card'}         Wrong card number
    {type: 'error',     reason: 'velocity checker'}     Declined by velocity checker
    {type: 'error',     reason: 'wrong alias'}          Wrong alias
    {type: 'waiting',   reason: 'captcha'}              The page is waiting for user input of captcha
    {type: 'success',   reason: 'CC'}                   The card number was successfully displayed
    {type: 'success',   reason: 'CVV'}                  The CVV code was successfully displayed
*/
```

> Check out our [**Javascript callbacks/hooks sample file**](https://datatrans.github.io/docs.pci-proxy.com/noshow-test-pilot.html).

**5. Ensure PCI-compliant user management**

_Note: In test mode, only test credit cards are allowed!_

---

### Reference

| **No-Show interface endpoint \(Sandbox\):** |
| :--- |
| [https://api.sandbox.datatrans.com/upp/services/v1/noshow/init](https://api.sandbox.datatrans.com/upp/services/v1/noshow/init) |

| Parameter | Description | Example value |
| :--- | :--- | :--- |
| `merchantId` | Your merchant ID | 1000011011 |
| `aliasCC` | Token you received when you collected the credit card | 424242SKMPRI4242 |
| `aliasCVV` \(optional\) | Token you received when you collected the CVV code | ozjc9rJvShqRkDw3lugOnulq |
| `username` | Unique and non generic userid or username | 659751 |
| `userEmail` | Email address of authorized employeewho retrieves it | james.bond@yourcompany.com |
| `sign` | SHA Hash - Hash converted to hexaDecimalString | SHA.256\(salt+merchantId+aliasCC\) |
| `language` \(optional\) | The language code in which the no-show page should be displayed | en |

### SIGN

##### Generate NoShow-specific `SHA.256 Security Sign` with `salt value`, `merchantId,` `aliasCC` \(token\) and `userEmail`

```js
salt        = V3hmMm29gD35OVHWDSAYKBIBCRg0znRekNvGbM9d8I4GRgfIcs                       // Setup in Step 1
merchantId  = 1100005007                                                               // Your Merchant ID
aliasCC     = 424242SKMPRI4242                                                         // CC token to be de-tokenized
userEmail   = example@gmail.com                                                        // Email address of NoShow-User

→ String: V3hmMm29gD35OVHWDSAYKBIBCRg0znRekNvGbM9d8I4GRgfIcs1100005007424242SKMPRI4242 // Concatenate all 3 values

SHA.256(salt+merchantId+aliasCC)                                                       // Use SHA.256 Hash Converter
→ Sign: 428dd59d048d78144a0def92a27b934f7bb39138161baf482ae2deb95c1741f5               // Security Sign for NoShow.jsp
```

_The „**salt**“ value has to be generated in the Datatrans web administration tool \(_[https://admin.sandbox.datatrans.com](https://admin.sandbox.datatrans.com)_\) under “UPP Administration” -&gt; “Security” -&gt; “Other Services”._

#### PCI DSS Compliant User Management

Using our _NoShow.jsp_ script requires you to handle your user management in a PCI DSS compliant way. PCI DSS requires certain user and password policies. Below you will find a comprehensive overview for a PCI DSS compliant user management. For a more detailed version on PCI DSS user management please see the official PCI DSS documents \(Requirement 8\)  [PCI DSS - Requirements and Security Assessment Procedures](https://www.pcisecuritystandards.org/documents/PCI_DSS_v3-2.pdf?agreement=true&time=1476177008560).

##### Unique User IDs

Every single user having access to the No-Show.jsp needs to have a unique user login to be clearly identified. **Shared user logins are not allowed. **

#### Password Policy

In general, the following password rules have to be observed:

* Passwords must be changed at least every 90 days.
* The password must have a minimum length of 7 characters.
* The password must contain upper and lower case letters, numbers and at least one special character.
* When changing the password none of the last four passwords can be used.
* After 6 failed login attempts a user account is locked. It can only be unlocked by the administrator.
* After 15 minutes of inactivity, the password must be entered to reactivate the terminal / session.
* The maximum session time after which the user must log in again must not exceed 200 minutes.

---

> ### Great job**: You have successfully integrated PCI Proxy! **
>
> You have securely retrieved a stored credit card without ever touching your servers. **Your systems never record, transmit or store real credit card data, only the token. Thus, you are out of PCI scope. **
>
> Enjoy PCI compliance in a risk-free environment. Keep in mind that you can use stored data as often as you need it.
>
> #### Questions?
>
> Don't hesitate to talk to us via email, phone, or Slack. We love to help you with the integration or other questions around PCI compliance or the PCI Proxy.
>
> Phone: +41 44 256 81 91  
> Email: [support@pci-proxy.com](/mailto:support@pci-proxy.com)



