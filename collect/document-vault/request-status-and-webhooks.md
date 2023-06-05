---
description: Additional information around the Request Status and the Webhooks
---

# Request Status & Webhooks

### 1. Request Status

A Document Vault request can have the following status:

<table><thead><tr><th width="305">Status</th><th>Describtion</th></tr></thead><tbody><tr><td><code>Pending</code></td><td>A new Upload link has been requested. No further action happened.</td></tr><tr><td><code>Documents provided</code></td><td>A new document has been uploaded. </td></tr><tr><td><code>Viewed</code></td><td>The document has been viewed. The expiration counter started. </td></tr><tr><td><code>Approved</code></td><td>The document has been approved.</td></tr><tr><td><code>Rejected</code></td><td>The document has been rejected. </td></tr></tbody></table>

### 2. Webhooks

Use the webhook feature to receive the current status of a request. A webhook will be triggered automatically after certain operation on the request resource.&#x20;

Simply submit your URL in the `webhookEndpoint` parameter sent to the [Request API](./#1.-request-upload-link) endpoint. An update is sent to the specified URL for the following status: `UPLOADED`, `VIEWED`, `APPROVED` and `REJECTED`. See an example for each webhook call below:&#x20;

#### Webhook examples

{% code title="Documents provided" %}
```json
{"id":"2DE3F521-39C1-4F86-BF99-F8616260D2C2","reference":"1337","status":"UPLOADED","validUntil":"2022-03-30T12:35:06.070Z"}

```
{% endcode %}

{% code title="Viewed" %}
```json
{"id":"2DE3F521-39C1-4F86-BF99-F8616260D2C2","reference":"1337","status":"VIEWED","validUntil":"2022-03-23T12:52:08.567Z"}

```
{% endcode %}

{% code title="Approved" %}
```json
{"id":"2DE3F521-39C1-4F86-BF99-F8616260D2C2","reference":"1337","status":"APPROVED","validUntil":"2022-03-23T12:52:08.567Z"}

```
{% endcode %}

{% code title="Rejected" %}
```json
{"id":"2DE3F521-39C1-4F86-BF99-F8616260D2C2","reference":"1337","status":"REJECTED","validUntil":"2022-03-23T12:52:08.567Z"}

```
{% endcode %}
