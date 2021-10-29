# Document Vault (beta)

The "Document Vault" allows your customers to upload sensitive images and documents in a PCI DSS and data security compliant environment.\
Therefore, you generate a unique upload link. The link can be presented to the user in your application. It redirects the user to an upload page which is hosted on our servers. Subsequently, the uploaded files can be reviewed in our Dashboard without the need to take care of PCI DSS compliance.

To get started, please follow the step-by-step guide below.

## 1. Request the upload link

Call our Init API from your server to request a unique upload link.

{% swagger baseUrl="https://dashboard.pci-proxy.com" path="/api/vault/request" method="post" summary="Init call" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="pci-proxy-api-key" type="string" required="true" %}
Your PCI Proxy API Key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="content-type" type="string" required="true" %}
application/json; charset=UTF-8
{% endswagger-parameter %}

{% swagger-parameter in="body" name="reference" type="string" required="true" %}
Unique reference number each request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="successUrl" type="string" required="false" %}
The URL where the cardholder gets redirected to if the upload was successful
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancelUrl" type="string" required="false" %}
The URL where the cardholder gets redirected to if the upload process got cancelled
{% endswagger-parameter %}

{% swagger-parameter in="body" name="errorUrl" type="string" required="false" %}
There URL where the cardholder gets redirected to if the upload process failed
{% endswagger-parameter %}

{% swagger-response status="200" description="Success response" %}
```javascript
{
    "link": "https://dev-dashboard-pciproxy.datatrans.biz/public/vault/BF33A0C8-F9ED-44AD-B818-015C08D76A44"
}
```
{% endswagger-response %}
{% endswagger %}

### Request & Response example

{% tabs %}
{% tab title="Request" %}
```javascript
curl -L -X POST 'https://dashboard.pci-proxy.com/api/vault/request' \
-H 'pci-proxy-api-key: {{API Key}}' \
-H 'content-type: application/json' \
--data-raw '{
    "reference":"tst-210812",
    "successUrl":"https://example.org/success",
    "cancelUrl":"https://example.org/cancel",
    "errorUrl":"https://example.org/error"
}'
```
{% endtab %}

{% tab title="Response" %}
```javascript
{
    "link": "https://dev-dashboard-pciproxy.datatrans.biz/public/vault/BF33A0C8-F9ED-44AD-B818-015C08D76A44"
}
```
{% endtab %}
{% endtabs %}

## 2. Redirect the cardholder

Embed the upload link received from the response into your application and redirect the cardholder to it.\
\
In case of a successful, cancelled or failed upload the cardholder will be redirected automatically to the URLs specified in the API request above.

{% hint style="info" %}
Supported file-types: `image/png`, `image/jpeg`, `image/heic`, `application/pdf`
{% endhint %}

## 3. Review uploaded documents

Login to our [dashboard](https://dashboard.pci-proxy.com/login) and navigate to the "Document Vault" menu within the Project section on the left-hand side menu bar. Press the View button to reveal an uploaded document.

{% hint style="info" %}
The "Document Vault" menu requires special user rights with mandatory 2FA enabled.\
Please contact us to assign such a user role.
{% endhint %}

!["Document Vault" menu](<.gitbook/assets/Document Vault view.png>)
