---
description: PCI Proxy token format overview
---

# Token format

PCI Proxy supports the following token format: 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Example</th>
      <th style="text-align:left">Format</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Alias 2.0</td>
      <td style="text-align:left">AAABcH0Bq92s3kgAESIAAbGj5NIsAHWC</td>
      <td style="text-align:left">AN32</td>
      <td style="text-align:left">
        <p>This format consists in numbers, letters, dash and underline.</p>
        <p>When using the Alias 2.0 format we additionally return a parameter <code>fingerprint</code> from
          our APIs. It helps you for example to identify customers who signed up
          with the same card number.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Masked Alias</td>
      <td style="text-align:left"><em>123456ABCDEF3456</em>
      </td>
      <td style="text-align:left">AN20</td>
      <td style="text-align:left">This format consists of the first 6 digits of the real credit card number,
        the actual BIN Range (Bank Identification Number), followed by the token
        in form of 6 upper-case letters. The Masked Credit Card Token ends with
        the last 4 digits of the actual credit card number. Based on card brand
        the length of the token varies.</td>
    </tr>
    <tr>
      <td style="text-align:left">Full Substitution</td>
      <td style="text-align:left"><em>1198182968382186732</em>
      </td>
      <td style="text-align:left">AN20</td>
      <td style="text-align:left">This format consists of digits only.</td>
    </tr>
    <tr>
      <td style="text-align:left">Masked Card Number</td>
      <td style="text-align:left"><em>424242XXXXXX4242</em>
      </td>
      <td style="text-align:left">AN20</td>
      <td style="text-align:left">Masked card number is returned with all APIs.</td>
    </tr>
  </tbody>
</table>

{% hint style="warning" %}
Although all formats are supported and compliant according PCI DSS we highly recommend to use `Alias 2.0` format to run certain operations. Please refer to [Convert API](https://docs.pci-proxy.com/use-stored-cards/manage) if you want to migrate from a legacy to the new format. 
{% endhint %}



