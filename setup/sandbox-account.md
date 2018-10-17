# Sandbox account

## Sandbox endpoints

### Server-to-Server APIs

{% tabs %}
{% tab title="/v1/pull" %}
[https://sandbox.pci-proxy.com/v1/pull](https://sandbox.pci-proxy.com/v1/pull)
{% endtab %}

{% tab title="/v1/push" %}
[https://sandbox.pci-proxy.com/v1/push](https://sandbox.pci-proxy.com/v1/push)
{% endtab %}

{% tab title="TokenAPI" %}
[https://api.sandbox.datatrans.com/upp/services/v1/inline/token](https://api.sandbox.datatrans.com/upp/services/v1/inline/token)
{% endtab %}

{% tab title="AliasGateway" %}
[https://api.sandbox.datatrans.com/upp/jsp/XML\_authorize.jsp ](https://api.sandbox.datatrans.com/upp/jsp/XML_authorize.jsp )
{% endtab %}

{% tab title="PayByEmail" %}
[https://api.sandbox.datatrans.com/upp/jsp/XML\_PayByEmail ](https://api.sandbox.datatrans.com/upp/jsp/XML_PayByEmail )
{% endtab %}
{% endtabs %}

### Browser APIs

{% tabs %}
{% tab title="Secure Fields" %}
[https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-1.0.0.js](https://pay.sandbox.datatrans.com/upp/payment/js/secure-fields-1.0.0.js)
{% endtab %}

{% tab title="Payment Page" %}
[https://pay.sandbox.datatrans.com/upp/jsp/upStart.jsp ](https://pay.sandbox.datatrans.com/upp/jsp/upStart.jsp )
{% endtab %}

{% tab title="NoShow" %}
[https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp ](https://pay.sandbox.datatrans.com/upp/jsp/noShow.jsp )
{% endtab %}
{% endtabs %}

### Web Admin Tool

#### [https://admin.sandbox.datatrans.com/ ](sandbox-account.md#https:admin.sandbox.datatrans.com)

Our web admin tool gives you a comprehensive management tool \(backoffice\) for initiating charges and credits, analyzing of transactions, personalization of the web application interface, creation of reports and management of configuration data.

### Production vs. Sandbox

Our production and sandbox environment always behave the same. Once all tests on your sandbox are successful, you can be rest assured that everything works the same in production. However, we differentiate between Production and Sandbox data to keep the environment separated. 

## Test card numbers

We have a set of test credit card numbers that you can use in our sandbox environment to test your integration. Please see [Test card data](../test-card-data.md).

## Slack Developer Chat

Chat with our developers if you need support relating to your sandbox account or PCI Proxy integration. Just drop us a line at [setup@pci-proxy.com](mailto:setup@pci-proxy.com) with your name and email address and we will invite you.

## Migrate payment data

If you have credit card data that is currently stored somewhere else and would like to migrate them to the PCI Proxy vault, you can either use the self-managed migration option [Vault \(alias gateway\)](../collect-and-store-cards/vault-alias-gateway.md) or [contact us](../have-a-question/contact-us.md) for a manual one-time import of large chunks of credit card data.

