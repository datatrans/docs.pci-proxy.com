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

Example link, pre-filled with token 424242SKMPRI4242_:_

| **Click to **[**Show Credit Card Number**](https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp?merchantId=1100005007&aliasCC=424242SKMPRI4242&aliasCVV=&sign=428dd59d048d78144a0def92a27b934f7bb39138161baf482ae2deb95c1741f5) |
| :--- |
| The NoShow link should retrieve the [test card number](/sandbox-environment.md) 4242 4242 4242 4242. |

##### 1. Generate NoShow-specific `SHA.256 Security Sign` with `salt value`, `merchantId` and `aliasCC` \(token\)

```js
salt        = V3hmMm29gD35OVHWDSAYKBIBCRg0znRekNvGbM9d8I4GRgfIcs                       // Setup in Step 1
merchantId  = 1100005007                                                               // Your Merchant ID
aliasCC     = 424242SKMPRI4242                                                         // CC token to be de-tokenized
aliasCVV    = xxx                                                                      // CVV token to be detokenized (optional)
userEmail   = example@gmail.com                                                        // Email address of NoShow-User

→ String: V3hmMm29gD35OVHWDSAYKBIBCRg0znRekNvGbM9d8I4GRgfIcs1100005007424242SKMPRI4242 // Concatenate all 3 values

SHA.256(salt+merchantId+aliasCC)                                                       // Use SHA.256 Hash Converter
→ Sign: 428dd59d048d78144a0def92a27b934f7bb39138161baf482ae2deb95c1741f5               // Security Sign for NoShow.jsp
```

> Need more help? Check out our [**NoShow example script**](https://datatrans.github.io/docs.pci-proxy.com/no-show.html).
>
> **2. Build NoShow Link with **`merchandId`**, **`aliasCC`** \(token\), **`sign`** and **`username`

```js
https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp 
               ?merchantId=1100005007
               &aliasCC=424242SKMPRI4242
               &sign=428dd59d048d78144a0def92a27b934f7bb39138161baf482ae2deb95c1741f5
               &username=max.mustermann@yourcompany.com
```

##### 3**. Optional: Add JavaScript callbacks/hooks**

```js
// Use attached Javascript callsbacks/hooks file to see which events are getting emitted to the parent frame.
// Bind an event listener to the parent frame to listen for those events:

function messageReceived(message)
{
  console.log(message.data);
}

if(window.addEventListener)
  window.addEventListener("message",messageReceived);
else
if(window.attachEvent)
  window.attachEvent("message",messageReceived);
else
  console.log("Could not listen.")
```

> Check out our [**Javascript callbacks/hooks sample file**](https://datatrans.github.io/docs.pci-proxy.com/noshow-test-pilot.html).

**4. Ensure PCI-compliant user management**

##### 5. Embed `NoShow Link` into your application

_Note: In test mode, only test credit cards are allowed!_

---

### Reference

| **No-Show interface endpoint \(Sandbox\):** |
| :--- |
| [https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp](https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp) |

| Required Parameter | Description | Example value |
| --- | --- | --- |
| `merchantId` | Your merchant ID | 1000011011 |
| `aliasCC` | Token you received when you collected the credit card | 70119122433810042 |
| `username` | Valid, non generic email address of authorized employee who retrieves it | max.mustermann@yourcompany.com |
| `sign` | SHA Hash - Hash converted to hexaDecimalString | SHA.256\(salt+merchantId+aliasCC\) |
| `language` | The language code in which the no-show page should be displayed | en |

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



