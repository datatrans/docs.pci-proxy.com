# HTTPS to HTTPS

## 1. Add integrations to your account

Before you can send request to a PCI compliant 3rd party you have to add the remote server as an integration to your account.

1. Navigate to the **Integrations** menu in the Project section and type in the name of the integration
2. Check the endpoint of the integration and press **Install**
3. Check if the payload fits your example and press again **Install** to activate the integration

Continue here if you miss an integration, if the payload or an endpoint doesn't match your requirements.

1. Navigate to the **Integrations** menu in the Project section and type in the name of the integration
2. Press **Request new Integration** button and complete the form
3. You get notified once the requested integration is ready for you

{% hint style="warning" %}
Please note the allowed TCP ports for endpoints:

**Sandbox** port **80 **and **`443`**

**Production** port **443**
{% endhint %}

## 2. Select forward method

PCI Proxy supports two different filter methods [**`/v1/pull`**](./#pull-method) and [**`/v1/push`**](./#push-method) to suit all your needs.&#x20;

Collecting card data from a partner via APIs can work in two ways. In general, either you perform a pull request to receive card data from your partner or a partner starts a push request to send you card data. PCI Proxy can extract sensitive data in both operations.

* ****[**/v1/pull**](broken-reference) - You start the request.

![Pull request](<../../../.gitbook/assets/Pull request big.svg>)

* ****[**/v1/push**](broken-reference) - Your partner starts the request.

![](<../../../.gitbook/assets/Pull request big.svg>)

## 3. [Continue with PULL method](pull-method.md)

## 4. [Continue with PUSH method](push-method.md)
