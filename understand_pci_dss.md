# Understand PCI DSS

You will learn who needs to be compliant and how you can achieve PCI DSS compliant.

Storing and handling sensitive payment data can be a tough try and it makes you a great target. 

## Who needs to comply with PCI DSS?

*Everyone storing, processing or transmitting sensitive card data* is required to comply with PCI DSS.

Even if you use certified third party providers to handle your sensitive card data, *you always need to proof your compliance.* 

PCI Proxy can reduce your efforts for PCI compliance to the minimal requirements. 

Thereby you avoid building your own PCI compliant environment and save costs and time.


## How to proof your compliance?

> Depends on how you handle sensitive payment data.

| Handling sensitive card data yourself | Use tokenization as a service |
| -- | -- |
| By handling sensitive payment data by yourself, you need to prove your compliance by conducting full onsite audits or completing SAQ D with 286 requirements annually plus performing quarterly network scans by approved scanning vendors. This is depending on the number of transactions you process yearly. | With PCI Proxy you generally prove your compliance by relying on Datatrans’ PCI DSS Level 1 certification. You can just fill out a reduced Self-Assessment Questionnaire (SAQ).  |
 
Eventually, the ultimate requirements are dictated by your acquirer/bank.


## Applicable SAQ

> Which Self-Assessment-Questionnaire applies to you? 

If you have decided whether you want to handle sensitive card data yourself or use Datatrans PCI Proxy to take care of your sensitive data, you fill out one of the relevant SAQs for online merchants:


### SAQ A
Your systems ```do not touch``` sensitive cardholder data or serve card collection forms.

[See relevant PCI PROXY APIs](collect-payment-data)


### SAQ A-EP
Your systems ```do not touch``` sensitive cardholder data ```but do serve``` card collection forms.

[See relevant PCI PROXY APIs](collect-payment-data)

### SAQ D
Your systems ```do touch``` sensitive cardholder data.

[See relevant PCI PROXY APIs](collect-payment-data)
