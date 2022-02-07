# Show Interface

The PCI Proxy Show API enables you to see the original credit card number of a stored credit card. Basically it is a web interface that can convert a token back into its original credit card number.

{% hint style="success" %}
Even though the interface is served by PCI Proxy, your PCI scope can extend. Therefore it's **mandatory** to implement it according to [PCI DSS user management](show-interface.md#pci-dss-compliant-user-management) and [password policy](show-interface.md#password-policy).&#x20;
{% endhint %}

{% swagger baseUrl="https://api.sandbox.datatrans.com/" path="upp/services/v1/noshow/init" method="post" summary="Init call" %}
{% swagger-description %}
1\. Let us know your IP address for whitelisting.

\


2\. Build this request to retrieve the NoShow link.
{% endswagger-description %}

{% swagger-parameter in="header" name="content-type" type="string" required="true" %}
API consumes application/xml or application/json
{% endswagger-parameter %}

{% swagger-parameter in="body" name="merchantId" type="string" required="true" %}
Your unique merchant id at PCI Proxy (e.g. 1100011011)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="aliasCC" type="string" required="true" %}
Credit card Token (e.g. AAABcHxr-sDssdexyrAAAfyXWIgaAF40
{% endswagger-parameter %}

{% swagger-parameter in="body" name="userName" type="string" required="false" %}
Unique userName (only required when no unique userEmail is given)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="userEmail" type="string" required="true" %}
**Unique**

 email-address where the link should be sent to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="SHASign" type="string" required="true" %}
Your security SHASign (see below how to calculate SHASign value)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="language" type="string" %}
default 

`en`

. Currently supported languages: 

`en`

, 

`de`

, 

`it`

, 

`fr`

, 

`es`

, 

`ru`
{% endswagger-parameter %}

{% swagger-response status="200" description="Response will contain NoShow link" %}
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<response>
  <url>https://api.sandbox.datatrans.com/upp/noshow?token=27cfba38-a606-49c0-9f03-c3bc6d580a66</url>
  <errorCode>0</errorCode>
</response>
```
{% endswagger-response %}
{% endswagger %}

### Examples

{% tabs %}
{% tab title="application/json" %}
{% code title="Request" %}
```javascript
curl -X POST https://api.sandbox.datatrans.com/upp/services/v1/noshow/init \
  -H 'content-type: application/json' \
  -d '{
    "merchantId": "1000011011",
    "aliasCC": "AAABcHxr-sDssdexyrAAAfyXWIgaAF40",
    "userName": "bond",
    "userEmail": "email@example.com",
    "SHASign": "d17ead827458e3532fd868b3b110671586b7e7ee0db106d5ae94e85ca93782ab",
    "language": "en"
   }'
```
{% endcode %}
{% endtab %}

{% tab title="application/xml" %}
{% code title="Request" %}
```markup
curl -X POST https://api.sandbox.datatrans.com/upp/services/v1/noshow/init \
  -H 'content-type: application/xml' \
  -d '<request>
        <merchantId>1000011011</merchantId>
        <aliasCC>AAABcHxr-sDssdexyrAAAfyXWIgaAF40</aliasCC>
        <userName>bond</userName>
        <userEmail>james.bond@yourcompany.com</userEmail>
        <SHASign>d17ead827458e3532fd868b3b110671586b7e7ee0db106d5ae94e85ca93782ab</SHASign>
        <language>en</language>
     </request>'
```
{% endcode %}
{% endtab %}
{% endtabs %}

3\. Embed the NoShow link from the response into your application

{% tabs %}
{% tab title="application/json" %}
{% code title="Response" %}
```javascript
{
    "url": "https://api.sandbox.datatrans.com/upp/noshow?token=2555559e-63d8-4c26-8799-0e9d64601037",
    "errorCode": 0
}
```
{% endcode %}
{% endtab %}

{% tab title="application/xml" %}
{% code title="Response" %}
```markup
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<response>
  <url>https://api.sandbox.datatrans.com/upp/noshow?token=27cfba38-a606-49c0-9f03-c3bc6d580a66</url>
  <errorCode>0</errorCode>
</response>
```
{% endcode %}
{% endtab %}
{% endtabs %}

4\. Once the user clicks on the link an email will be sent to `userEmail` where the new device must be authorized either by clicking on the provided link or by entering the activation code manually.&#x20;

5\. Subsequently the new device has been authorized and the user may enter a six digits security code in the opened iFrame to retrieve plain text credit card number.&#x20;

Need more help? Check out our [**NoShow example script**](https://datatrans.github.io/docs.pci-proxy.com/no-show.html).

6\. Ensure [PCI-compliant user management](show-interface.md#pci-dss-compliant-user-management)

{% hint style="info" %}
In test mode, only [test credit cards](broken-reference) are allowed!
{% endhint %}

### Reference

| PCI Proxy NoShow Endpoint **(Sandbox):**                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------ |
| [https://api.sandbox.datatrans.com/upp/services/v1/noshow/init](https://api.sandbox.datatrans.com/upp/services/v1/noshow/init) |

| **Parameter**                 | **Description**                                                                                                                                                               | **Example value**                          |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| `merchantId`                  | Your merchant ID                                                                                                                                                              | 1000011011                                 |
| `aliasCC`                     | Token you received when you collected the credit card                                                                                                                         | AAABcHxr-SDssdexrAAAfyXWIgaAF40            |
| `aliasCVV` (optional)         | Token you received when you collected the CVV code                                                                                                                            | ozjc9rJvShqRkDw3lugOnulq                   |
| `userName` (optional)         | [Unique userID](https://app.gitbook.com/@dtrx/s/v2-shu/\~/drafts/-MizDgZTlUVxDe3VmPpx/use/show-interface#unique-user-ids) or username if the parameter `userEmail` is generic | 659751 or JamesBond                        |
| `userEmail`                   | **Unique** email address of the authorized employee who retrieves the credit card number                                                                                      | james.bond@yourcompany.com                 |
| [`SHASign`](broken-reference) | SHA Hash - Hash converted to hexaDecimalString                                                                                                                                | SHA.256(salt+merchantId+aliasCC+userEmail) |
| `language` (optional)         | The language code in which the no-show page should be displayed                                                                                                               | `en`, `de`, `fr`, `it`, `es`, `ru`         |

### SHA.256 Security Sign

Generate NoShow-specific SHA.256 Security Sign with salt value, merchantId, aliasCC (token) and userEmail

```javascript
salt        = V3hmMm29gD35OVHWDSAYKBIBCRg0znRekNvGbM9d8I4GRgfIcs                       // Setup in Step 1
merchantId  = 1100005007                                                               // Your Merchant ID
aliasCC     = AAABcHxr-sDssdexyrAAAfyXWIgaAF40                                         // CC token to be de-tokenized
userEmail   = james.bond@yourcompany.com                                               // Email address of NoShow-User

→ String: V3hmMm29gD35OVHWDSAYKBIBCRg0znRekNvGbM9d8I4GRgfIcs1100005007424242SKMPRI4242 // Concatenate all 4 values
          james.bond@yourcompany.com 
SHA.256(salt+merchantId+aliasCC+userEmail)                                             // Use SHA.256 Hash Converter
→ SHASign: f641a6a3de574bd4b7609320e9a4fb1ed11364f136908822ff6a8e3b6b1bca1f            // Security Sign for NoShow.jsp
```

{% hint style="info" %}
The **salt value** can be accessed in the PCI Proxy dashboard within the[ API Keys](broken-reference) section.&#x20;
{% endhint %}

Example: [NoShow sign calculation](https://datatrans.github.io/docs.pci-proxy.com/no-show.html)

### **Optional: Add JavaScript callbacks/hooks**

```
// Use the attached Javascript callsbacks/hooks file to see which events are getting emitted to the parent frame.
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

## PCI DSS Compliant User Management

Using our _NoShow.jsp_ script requires you to handle your user management and password policy in a PCI DSS compliant way. Below you will find a comprehensive overview for a PCI DSS compliant user management. For a more detailed version on PCI DSS user management please see the official PCI DSS documents (Requirement 8) [PCI DSS - Requirements and Security Assessment Procedures](https://www.pcisecuritystandards.org/documents/PCI\_DSS\_v3-2.pdf?agreement=true\&time=1476177008560).

### **Unique User IDs**

Every single user having access to the No-Show.jsp needs to have a unique user login to be clearly identified. Assigning a unique identification (ID) to each person with access ensures that each individual is uniquely accountable for their actions. When such accountability is in place, actions taken on critical data and systems are performed, by and can be traced to, known and authorized users and processes.&#x20;

{% hint style="danger" %}
Shared user logins are not allowed.&#x20;
{% endhint %}

### Password Policy

The effectiveness of a password is largely determined by the design and implementation of the authentication system—particularly, how frequently password attempts can be made by an attacker, and the security methods to protect user passwords at the point of entry, during transmission, and while in storage. In general, the following minimum password rules have to be observed:

* Users are required to change their passwords every 90 days
* The password must have a minimum length of 7 characters.
* The password must contain upper and lower case letters, numbers, and at least one special character.
* When changing the password none of the last four passwords can be used.
* Vendor-supplied defaults will not be allowed.
* When passwords are generated for the user, the password must be unique to each user and be changed after the first use.
* After 6 failed login attempts a user account is locked. It can only be unlocked by the administrator.
* After 15 minutes of inactivity, the password must be entered to reactivate the terminal/session.
* The maximum session time after which the user must log in again must not exceed 200 minutes.