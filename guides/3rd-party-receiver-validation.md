# Receiver PCI DSS compliance validation

The Payment Card Industry Data Security Standard is a set of security standards designed to ensure that all companies that **accept**, **process**, **store **or **transmit **credit card information maintain a secure environment. The PCI DSS applies to any organization, regardless of size or number of transactions, that accepts, transmits or stores any cardholder data, such as payment processors, acquirers, issuers, and service providers.

**PCI Proxy’s Forward API** allows you to distribute and share credit card data freely across PCI compliant level 1 and level 2 third-party service providers (Receivers). In order to ensure that you only share credit card data with compliant and trustworthy receivers, we have to validate the compliance status of the respectively third-party receiver to ensure continued protection of your customers credit card data.

{% tabs %}
{% tab title="PCI DSS Level 1 Service Provider (Onsite-Assessment)" %}
Stores, processes, or transmits **more **than 300,000 credit card transactions annually
{% endtab %}

{% tab title="PCI DSS Level 2 Service Provider (Self-Assessment)    " %}
Stores, processes, or transmits \*\*less \*\*than 300,000 credit card transactions annually
{% endtab %}
{% endtabs %}

## **Validation for Level 1 Service Providers (onsite-assessment)**

{% hint style="info" %}
All Level 1 third party receiver must complete an annual onsite assessment conducted by a PCI SSC certified [Qualified Security Assessor (QSA)](https://www.pcisecuritystandards.org/assessors\_and\_solutions/qualified\_security\_assessors) or Internal Security Assessor (ISA). Therefore, please obtain the document stated below:
{% endhint %}

1\) Request a signed copy of the Attestation of Compliance (AOC) for **onsite assessments**.

2\) Provide a copy of the AOC to [contact@pci-proxy.com](mailto:contact@pci-proxy.com)

3\) You will be notified once the AOC is approved.

## **Validation for Level 2 Service Providers (self-assessment)**

{% hint style="info" %}
All Level 2 third party receiver must complete an annual self-assessment with Self-Assessment Questionnaire D. Therefore, please obtain the documents stated below:
{% endhint %}

1\) Request a signed copy of the Attestation of Compliance (AOC) for [**Self-Assessment Questionnaire D**](https://www.pcisecuritystandards.org/documents/PCI-DSS-v3\_2\_1-SAQ-D\_ServiceProvider.pdf?agreement=true\&time=1595503662823) Service Provider

2\) To obtain an additional measure of assurance, obtain a written and signed acknowledgement about the responsibility for the security of cardholder data with your third party receiver. Please contact your account manager at PCI Proxy for an example **Letter of Acknowledgment** (PCI DSS requirement 12.8.2 and 12.9).

3\) Provide a copy of all documents to [contact@pci-proxy.com](mailto:contact@pci-proxy.com)

4\) You will be notified once the AOC is approved.

{% hint style="info" %}
Please note that the only documentation recognized for PCI DSS validation are the official documents from the PCI SSC website. Any other form of certificate or documentation issued for the purposes of illustrating compliance to PCI DSS or any other PCI standard are not authorized or validated, and their use is not acceptable for evidencing compliance. The use of certificates or other non-authorized documentation to validate PCI DSS Requirement 12.8 and/or Requirement 12.9 is also not acceptable.
{% endhint %}

## PCI DSS Glossary

| **Acronym** | **Definition**                                                                                                                                                                             | **Further information**                                                                                                                                                               |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PCI SSC     | Payment Card Industry Security Standards Council                                                                                                                                           | [PCI Security Standards](https://www.pcisecuritystandards.org)                                                                                                                        |
| PCI DSS     | Payment Card Industry Data Security Standard                                                                                                                                               | [PCI DSS v3.2.1](https://www.pcisecuritystandards.org/documents/PCI\_DSS\_v3-2-1.pdf?agreement=true)                                                                                  |
| AOC         | Attestation of Compliance                                                                                                                                                                  | AOC for onsite assessments: [AOC-ServiceProviders.docx](https://www.pcisecuritystandards.org/documents/PCI-DSS-v3\_2\_1-AOC-ServiceProviders.docx?agreement=true\&time=1595506976845) |
| SAQ-D       | <p>Self-Assessment Questionnaire type D -</p><p>Reporting tool used to document self-assessment results from an entity’s PCI DSS assessment.</p>                                           | [Self Assessment Questionnaire - D](https://www.pcisecuritystandards.org/documents/PCI-DSS-v3\_2\_1-SAQ-D\_ServiceProvider.pdf?agreement=true\&time=1595503662823)                    |
| QSA         | <p>Qualified Security Assessor -</p><p>QSAs are qualified by PCI SSC to perform PCI DSS on-site assessments.</p>                                                                           | [Search for a Qualified Security Assessor](https://www.pcisecuritystandards.org/assessors\_and\_solutions/qualified\_security\_assessors)                                             |
| ISA         | Internal Security Assessor - professionals of qualifying organizations which received PCI DSS training and certification that will improve the organization's understanding of the PCI DSS | [Verify an ISA Employee](https://www.pcisecuritystandards.org/assessors\_and\_solutions/internal\_security\_assessors)                                                                |
