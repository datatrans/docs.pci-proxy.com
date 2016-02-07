# Understand PCI DSS

Learn who needs to be PCI DSS compliant and how you can achieve PCI DSS compliance.

Storing and handling sensitive payment data can be a tough try and it makes you a great target. 

## Who needs to comply with PCI DSS?

*Everyone storing, processing or transmitting sensitive card data* is required to comply with PCI DSS.

Even if you use certified third party providers to handle your sensitive card data, *you always need to proof your compliance.* 

> PCI Proxy can reduce your efforts for PCI compliance to the minimal requirements. 

Thereby you avoid building your own PCI compliant environment and save costs and time.


## How to proof your compliance?

It depends on how you handle sensitive payment data. Eventually, it is dictated by your acquirer/bank.

| Handling sensitive card data yourself | Use tokenization as a service |
| -- | -- |
| You need to prove your compliance by conducting full onsite audits or completing SAQ D with 286 requirements annually plus performing quarterly network scans by approved scanning vendors (Depends on the number of transactions you process yearly). | With PCI Proxy you generally prove your compliance by relying on Datatrans’ PCI DSS Level 1 certification. You can just fill out a reduced Self-Assessment Questionnaire (SAQ).  |
 



## Which SAQ is applicable to you?

If you have decided whether you want to handle sensitive card data yourself or use PCI Proxy to take care of your sensitive data, you fill out one of the relevant SAQs for online merchants:


### SAQ A
Your systems ```do not touch``` sensitive cardholder data or serve card collection forms.

[See relevant PCI PROXY APIs](collect-payment-data)


### SAQ A-EP
Your systems ```do not touch``` sensitive cardholder data ```but do serve``` card collection forms.

[See relevant PCI PROXY APIs](collect-payment-data)

### SAQ D
Your systems ```do touch``` sensitive cardholder data.

[See relevant PCI PROXY APIs](collect-payment-data)

## What PCI Requirements fulfills PCI Proxy?

**Requirement 2:** Do not use vendor-supplied defaults for system passwords and other security parameters.

*PCI Proxy does not provide default credentials. All data vaults and API methods can be configured with unique access keys.*

**Requirement 3:** Protect stored cardholder data.

*PCI Proxy fully manages and secures all vaulted data. PCI Proxy uses the latest in encryption and hardware security modules to protect vaulted data. Encryption algorithms used include RSA, AES, 3DES, and DUKPT*

**Requirement 4:** Encrypt transmission of cardholder data across open, public networks.

*PCI Proxy uses TLS and SFTP protocols exclusive for transmission of cardholder data. PCI Proxy cannot accept unprotected data.*

**Requirement 7:** Restrict access to cardholder data by business need to know.

*PCI Proxy provides API access on a pre-method basis as well as IP whitelisting. PCI Proxy allows clients to separate tokenization and detokenization access controls to ensure only authorized staff with a need to know have access to the data vaults.*


**Requirement 9:** Restrict physical access to cardholder data.

*By removing cardholder data from your environment, physical security compliance becomes a breeze.
PCI Proxy uses top tier data centers with SAS70, PCI, and SSAE SOC2 certifications.*

**Requirement 10:** Track and monitor all access to network resources and cardholder data.

*PCI Proxy provides robust logging and usage capabilities to track all access into and out of your data vaults.*
