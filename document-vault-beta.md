# Document Vault \(beta\)

The "Document Vault" allows your customers to upload sensitive images and documents in a PCI DSS and data security compliant environment.   
Therefore, you generate a unique upload link. The link can be presented to the user in your application. It redirects the user to an upload page which is hosted on our servers. Subsequently, the uploaded files can be reviewed in our Dashboard without the need to take care of PCI DSS compliance. 

To get started, please follow the step-by-step guide below.

## 1. Request upload link

{% api-method method="post" host="https://dashboard.pci-proxy.com" path="/api/vault/request" %}
{% api-method-summary %}
Init call
{% endapi-method-summary %}

{% api-method-description %}
Call our Init API from **your server** to request a unique upload link. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="pci-proxy-api-key" type="string" required=true %}
Your PCI Proxy API Key
{% endapi-method-parameter %}

{% api-method-parameter name="content-type" type="string" required=true %}
application/json; charset=UTF-8
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="reference" type="string" required=true %}
Unique reference number each request
{% endapi-method-parameter %}

{% api-method-parameter name="successUrl" type="string" required=true %}
The URL where the cardholder gets redirected to if the upload was successful
{% endapi-method-parameter %}

{% api-method-parameter name="cancelUrl" type="string" required=true %}
The URL where the cardholder gets redirected to if the upload process got cancelled 
{% endapi-method-parameter %}

{% api-method-parameter name="errorUrl" type="string" required=true %}
There URL where the cardholder gets redirected to if the upload process failed
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Success response
{% endapi-method-response-example-description %}

```javascript
{
    "link": "https://dev-dashboard-pciproxy.datatrans.biz/public/vault/BF33A0C8-F9ED-44AD-B818-015C08D76A44"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

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

Embed the upload link received from the response into your application and redirect the cardholder to it.   
  
In case of a successful, cancelled or failed upload the cardholder will be redirected automatically to the URLs specified in the API request above. 

{% hint style="info" %}
Supported file-types: `image/png`, `image/jpeg`, `image/heic`, `application/pdf`
{% endhint %}

## 3. Review uploaded documents

Login to our [dashboard](https://dashboard.pci-proxy.com/login) and navigate to the "Document Vault" menu within the Project section on the left-hand side menu bar. Press the View button to reveal an uploaded document. 

{% hint style="info" %}
The "Document Vault" menu requires special user rights with mandatory 2FA enabled.   
Please contact us to assign such a user role. 
{% endhint %}

![&quot;Document Vault&quot; menu](.gitbook/assets/document-vault-view.png)

