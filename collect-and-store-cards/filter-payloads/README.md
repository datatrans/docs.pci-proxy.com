# Filter \(webservice\)

Simply redirect requests containing sensitive card data through PCI Proxy to avoid sensitive data hitting your servers. PCI Proxy automatically scans requests for sensitive card data. Located card data is instantly collected, tokenized and stored in our secure vaults in Switzerland. A reference number \(token\) is issued that substitutes the sensitive data in the request or response. All other headers and payload always remains the same.

{% hint style="success" %}
All happens before sensitive card data ever touches your servers to reduce your PCI scope.
{% endhint %}

## 1. Add integrations to your account

Before you can filter payloads from a remote server you have to add the remote server as an integration to your account:

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration  
2\) Check the endpoint of the integrationd and press **Install**  
3\) Check if the payload fits your example and press again **Install** to activate the integration

Continue here if you miss an integration, if the payload or an endpoint doesn't match your requirements.

1\) Navigate to the **Integrations** menu in the Project section and type in the name of the integration  
2\) Press **Request new Integration** button and complete the form  
3\) You get notified once the requested integration is ready for you

{% hint style="warning" %}
Please note the allowed TCP ports for endpoints:

**Sandbox** Port `80` and `443`

**Production** Port `443`
{% endhint %}

## 2. Select filter method

PCI Proxy supports two different filter methods [`/v1/pull`](./#pull-method) and [`/v1/push`](./#push-method) to suit all your needs. 

Collecting card data from a Channel via web service can work in two ways. In general, either you perform a pull request to receive card data from the Channel or a Channel starts a push request to send you card data. PCI Proxy can extract sensitive data in both operations.

| [**`/v1/pull`**](./#pull-method)  | [**`/v1/push`**](./#push-method)  |
| :--- | :--- |
| You start the request. | The Channel starts the request. |
| ![](../../.gitbook/assets/channel_pull_status_quo_color%20%285%29.png) | ![](../../.gitbook/assets/channel_push_status_quo_color.png) |

## 3. [Continue with PULL method  ](pull-method.md)       [Continue with PUSH method](push-method.md)

