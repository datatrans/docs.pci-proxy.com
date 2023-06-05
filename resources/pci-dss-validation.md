# PCI DSS Validation

The Payment Card Industry Data Security Standard is a set of security standards designed to ensure that all companies that accept, process, store or transmit payment information maintain a secure environment. The PCI DSS applies to any organization, regardless of size or number of transactions, that accepts, transmits or stores any payment data, such as payment processors, acquirers, issuers, and service providers.

Using the <mark style="color:blue;">**Forward Proxy**</mark> allows you to distribute sensitive payment data freely across PCI-compliant endpoints (Receivers). In order to ensure that you only share payment data with compliant and trustworthy Receivers, we help you to validate the compliance status of the respectively third-party Receiver to ensure continued protection of your customers' payment data.



{% tabs %}
{% tab title="PCI DSS Level 1 Service Provider (Onsite-Assessment)" %}
Stores, processes, or transmits <mark style="color:blue;">**more**</mark> than 300,000 credit card transactions annually
{% endtab %}

{% tab title="PCI DSS Level 2 Service Provider (Self-Assessment)    " %}
Stores, processes, or transmits <mark style="color:blue;">**less**</mark> than 300,000 credit card transactions annually
{% endtab %}
{% endtabs %}

## **Validation for Level 1 Service Providers**

{% hint style="info" %}
Level 1 Service Provider must complete an annual <mark style="color:blue;">**Onsite Assessment**</mark> conducted by a PCI SSC certified Qualified Security Assessor (QSA) or Internal Security Assessor (ISA).&#x20;
{% endhint %}

Please obtain the document stated below:

1. Request a signed copy of the Attestation of Compliance (AOC) for Onsite Assessments.
2. Provide a copy of the AOC to support@pci-proxy.com.
3. You will be notified once the AoC is approved.

**Validation for Level 2 Service Providers**


{% hint style="info" %}
Level 2 Service Provider must complete an annual self-assessment with <mark style="color:blue;">**Self-Assessment Questionnaire D**</mark><mark style="color:blue;">.</mark>
{% endhint %}

Please obtain the documents stated below:&#x20;

1. Request a signed copy of the Attestation of Compliance (AOC) for Self-Assessment Questionnaire D.
2. To obtain an additional measure of assurance, obtain a written and signed acknowledgment about the responsibility for the security of cardholder data with your Receiver (please refer to PCI DSS requirement 12.8.2, 12.9). Please contact your Technical Account Manager at PCI Proxy for an example Letter of Acknowledgment.&#x20;
3. Provide a copy of the AOC and Letter of Acknowledgment to support@pci-proxy.com.
4. You will be notified once the documents are approved.

{% hint style="info" %}
Please note that the only documentation recognized for PCI DSS validation are the official documents from the PCI SSC website. Any other form of certificate or documentation issued for the purposes of illustrating compliance to PCI DSS or any other PCI standard are not authorized or validated, and their use is not acceptable for evidencing compliance. The use of certificates or other non-authorized documentation to validate PCI DSS Requirement 12.8 and/or Requirement 12.9 is also not acceptable.
{% endhint %}

## PCI DSS Glossary

<table><thead><tr><th>Acronym</th><th width="150">Definition</th><th>Further information</th></tr></thead><tbody><tr><td><code>PCI SSC</code></td><td>Payment Card Industry Security Standards Council</td><td><a href="https://www.pcisecuritystandards.org/">PCI Security Standards</a></td></tr><tr><td><code>PCI DSS</code></td><td>Payment Card Industry Data Security Standard</td><td><a href="https://www.pcisecuritystandards.org/documents/PCI_DSS_v3-2-1.pdf?agreement=true">PCI DSS v3.2.1</a></td></tr><tr><td><code>AOC</code> </td><td>Attestation of Compliance</td><td>AOC for onsite assessments: <a href="https://www.pcisecuritystandards.org/documents/PCI-DSS-v3_2_1-AOC-ServiceProviders.docx?agreement=true&#x26;time=1595506976845">AOC-ServiceProviders.docx</a></td></tr><tr><td><code>SAQ-D</code></td><td><p>Self-Assessment Questionnaire type D - </p><p>Reporting tool used to document self-assessment results from an entity’s PCI DSS assessment. </p></td><td><a href="https://www.pcisecuritystandards.org/documents/PCI-DSS-v3_2_1-SAQ-D_ServiceProvider.pdf?agreement=true&#x26;time=1595503662823">Self Assessment Questionnaire - D</a></td></tr><tr><td><code>QSA</code></td><td><p>Qualified Security Assessor - </p><p>QSAs are qualified by PCI SSC to perform PCI DSS on-site assessments.</p></td><td><a href="https://www.pcisecuritystandards.org/assessors_and_solutions/qualified_security_assessors">Search for a Qualified Security Assessor</a></td></tr><tr><td><code>ISA</code></td><td>Internal Security Assessor - professionals of qualifying organizations which received PCI DSS training and certification that will improve the organization's understanding of the PCI DSS</td><td><a href="https://www.pcisecuritystandards.org/assessors_and_solutions/internal_security_assessors">Verify an ISA Employee</a></td></tr></tbody></table>

