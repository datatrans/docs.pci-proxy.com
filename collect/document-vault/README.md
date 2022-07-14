# Document Vault

The <mark style="color:blue;">**Document Vault**</mark> allows your customers to upload sensitive images and documents in a PCI DSS and data security compliant environment. Therefore, you generate a unique upload link that can be presented to the user in your application. It redirects the user to an upload page which is hosted on our servers. Subsequently, the uploaded files can be reviewed in the Dashboard by applying our approval logic without the need to take care of PCI DSS compliance.

To get started, please follow the step-by-step guide below.

## 1. Request upload link

To start, call our Request API from your server to create an upload link.

{% swagger baseUrl="https://api.vault.sandbox.pci-proxy.com" path="/v1/requests" method="post" summary="Request call" %}
{% swagger-description %}
Call our Request API from **your server** to create an upload link.

The parameters marked with \* are mandatory.&#x20;
{% endswagger-description %}

{% swagger-parameter in="header" name="pci-proxy-api-key" type="string" required="true" %}
Your PCI Proxy 

[API Key](../../resources/pci-proxy-dashboard/api-authentication-data.md)


{% endswagger-parameter %}

{% swagger-parameter in="header" name="content-type" type="string" required="false" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference" type="string" required="true" %}
Unique reference number to identify your request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="successUrl" type="string" required="true" %}
The URL where the cardholder will be redirected to if the upload was successful
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancelUrl" type="string" required="true" %}
The URL where the cardholder will be redirected to if the upload process got cancelled 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="errorUrl" type="string" required="true" %}
The URL where the cardholder will be redirected to if the upload process failed
{% endswagger-parameter %}

{% swagger-parameter in="body" name="webhookEndpoint" type="string" %}


[Webhook URL](request-status-and-webhooks.md#2.-webhooks)

 which will be called after the following actions: 

`Uploaded`

, 

`Viewed`

, 

`Approved`

, 

`Rejected`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="context" type="object" %}
Use this object to submit up to 6 additional parameters. They will be displayed in the Dashboard together with the uploaded document. 
{% endswagger-parameter %}

{% swagger-response status="200" description="Upload link created" %}
```
{
    "link": "https://dev-dashboard-pciproxy.datatrans.biz/public/vault/873CD451-8073-487B-8037-02D850D7603D"
}
```
{% endswagger-response %}
{% endswagger %}

### Request & Response example

{% tabs %}
{% tab title="Request" %}
```javascript
curl --location --request POST 'https://api.vault.sandbox.pci-proxy.com/v1/requests' \
--header 'pci-proxy-api-key: {{API Key}}' \
--header 'content-type: application/json' \
--data-raw '{
    "reference":"1337",
    "successUrl":"https://example.org/success",
    "cancelUrl":"https://example.org/cancel",
    "errorUrl":"https://example.org/error",
    "webhookEndpoint":"https://example.org/webhook",
    "context": {
        "Test Card":"true", 
        "FirstName": "Jon",
        "LastName": "Doe"
    }
}'
```
{% endtab %}

{% tab title="Response" %}
```
{
    "link": "https://vault.sandbox.pci-proxy.com/4E632C20-CC04-4E27-8B34-B580AD305494"
}
```
{% endtab %}
{% endtabs %}

## 2. Redirect the cardholder&#x20;

As a next step, embed the upload link received from the response into your application and redirect the user to it. The link will open an upload page hosted by us. \
In case of a successful, cancelled, or failed upload the user will be redirected automatically to the URLs specified in the API request above.&#x20;

{% hint style="info" %}
Supported file-types: `image/png`, `image/jpeg`, `image/heic`, `application/pdf`
{% endhint %}

## 3. Access and review requests

Login to our [Dashboard](https://dashboard.pci-proxy.com/login) and navigate to the "Document Vault" menu within the Project section on the left-hand side menu bar. You can see all the requested links and the current [status](request-status-and-webhooks.md#1.-request-status) of the request.&#x20;

{% hint style="info" %}
The Document Vault needs to be activated for you and requires special user rights with mandatory 2FA enabled. Please contact us to assign such a user role.&#x20;
{% endhint %}

![Document Vault overview menu](<../../.gitbook/assets/Vault overview.png>)

To review an uploaded document please press the View button on the right side.\
An overlay with the uploaded document and the optional data sent in the [API request](./#1.-request-upload-link) will be opened. To approve or reject a document use the buttons on the bottom. Each action will trigger a call to the [webhook](request-status-and-webhooks.md#2.-webhooks).&#x20;

![Document Vault detail view](<../../.gitbook/assets/Detail view.png>)

{% hint style="danger" %}
To keep your sensitive data secure and to be compliant with PCI DSS we have a retention policy for viewed documents in place. Learn more about the retention policy [here](security-and-retention-policy.md).&#x20;
{% endhint %}
