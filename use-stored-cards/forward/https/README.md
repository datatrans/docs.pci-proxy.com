# HTTPS to HTTPS

## 1. Add integrations to your account

Before you can send request to a PCI compliant 3rd party you have to add the remote server as an integration to your account. 

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration\
2\) Check the endpoint of the integration and press **Install**\
3\) Check if the payload fits your example and press again **Install** to activate the integration

Continue here if you miss an integration, if the payload or an endpoint doesn't match your requirements.

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration\
2\) Press **Request new Integration** button and complete the form\
3\) You get notified once the requested integration is ready for you

{% hint style="warning" %}
Please note the allowed TCP ports for endpoints:

**Sandbox **Port `80 `and `443`

**Production **Port `443`
{% endhint %}

## 2. Select forward method

PCI Proxy supports two forwarding methods [`/v1/pull/`](./#pull-method) and [`/v1/push/`](./#push-method) to suit all your needs.

Forwarding card data to a remote server via HTTPS can work in two ways. In general, either you perform a pull request to forward card data to the Receiver or a Receiver starts a push request to receive card data from you in the response. PCI Proxy can populate both operations with sensitive data.

| [**`/v1/pull/`**](./#pull-method)                                      | [**`/v1/push/`**](./#push-method)                                      |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| You start the request.                                                 | The Receiver starts the request.                                       |
| ![](<../../../.gitbook/assets/receiver_pull_status_quo_color (1).png>) | ![](<../../../.gitbook/assets/receiver_push_status_quo_color (1).png>) |

## 3. [Continue with PULL method](pull-method.md)          [Continue with PUSH method](push-method.md)
