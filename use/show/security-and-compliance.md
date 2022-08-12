---
description: Learn how display card data in a secure and compliant way
---

# Security and Compliance

Although using PCI Proxy Show reduces your PCI DSS scope, it does not completely eliminate it. Please read below to see **your responsibilities** to guarantee a safe and compliant usage of the PCI Proxy Show feature.&#x20;

{% hint style="danger" %}
As the Show API displays sensitive cardholder data, it should only be used for end users. Using it internally will extend your scope.&#x20;
{% endhint %}

#### User authentication&#x20;

The Show API does not serve any user authentication method nor does it interact with your authentication mechanism. It is therefore extremely important that your backend application manages the user authentication and ensures that, when card data will be displayed in your application:

1. your application provides a login method
2. the reveal feature is protected with Multi Factor Authentication&#x20;
3. the user which requests to see card data is authenticated and matches with the tokens that are being requested

Those requirements are **mandatory** and will be checked by our team before granting access to the Show API.

#### **Unique User IDs**

Every single user having access to the Show API needs to have a unique user login to be clearly identified. Assigning a unique identification (ID) to each person with access ensures that each individual is uniquely accountable for their actions. When such accountability is in place, actions taken on critical data and systems are performed, by and can be traced to, known and authorized users and processes.&#x20;

{% hint style="danger" %}
Shared user logins are not allowed.&#x20;
{% endhint %}

#### Password Policy

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

For a more detailed version on PCI DSS user management please see the official PCI DSS documents (Requirement 8) [PCI DSS - Requirements and Security Assessment Procedures](https://www.pcisecuritystandards.org/documents/PCI\_DSS\_v3-2.pdf?agreement=true\&time=1476177008560).
