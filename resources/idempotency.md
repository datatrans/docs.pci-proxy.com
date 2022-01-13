# Idempotency

To retry identical requests with the same effect without accidentally performing the same operation more than needed, you can add the header `Idempotency-Key` to your requests. This is useful when API calls are disrupted or you did not receive a response. In other words, retrying identical requests with our idempotency key will not have any side effects. We will return the same response for any identical request that includes the same idempotency key.

If your request failed to reach our servers, no idempotent result is saved because no API endpoint processed your request. In such cases, you can simply retry your operation safely. Idempotency keys remain stored for 60 minutes. After 60 minutes have passed, sending the same request together with the previous idempotency key will create a new operation.

Please note that the idempotency key has to be unique for each request and has to be defined by yourself. We recommend assigning a random value as your idempotency key and using UUID v4. Idempotency is only available for `POST` requests.

Idempotency was implemented according to the ["The Idempotency HTTP Header Field" Internet-Draft](https://tools.ietf.org/id/draft-idempotency-header-01.html)



| Scenario           | Condition                                                               | Expectation                                                                                             |
| ------------------ | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| First time request | Idempotency key has not been seen during the past 60 minutes.           | The request is processed normally.                                                                      |
| Repeated request   | The request was retried after the first time request completed.         | The response from the first time request will be returned.                                              |
| Repeated request   | The request was retried before the first time request completed.        | 409 Conflict. It is recommended that clients time their retries using an exponential backoff algorithm. |
| Repeated request   | The request body is different than the one from the first time request. | 422 Unprocessable Entity.                                                                               |

### Example

```
curl -L -X POST 'https://api.sandbox.datatrans.com/v1/tokenizations/220112095131012129' \
-H 'Authorization: Basic MTEwMDAxNzc4OTpNQUd6UUVEbkVxd001d0Vr' \
-H 'Content-Type: application/json' \
-H 'Idempotency-Key: e75d621b-0e56-4b71-b889-1acec3e9d870'
```
