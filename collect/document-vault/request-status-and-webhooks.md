---
description: Additional information around the Request Status and the Webhooks
---

# Request Status & Webhooks

### 1. Request Status

A Document Vault request can have the following status:

| Status               | Describtion                                                       |
| -------------------- | ----------------------------------------------------------------- |
| `Pending`            | A new Upload link has been requested. No further action happened. |
| `Documents provided` | A new document has been uploaded.                                 |
| `Viewed`             | The document has been viewed. The expiration counter started.     |
| `Approved`           | The document has been approved.                                   |
| `Rejected`           | The document has been rejected.                                   |

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
