# Request Types

In general, either **you start a request** (`PULL`) or a **remote server starts a request** (`PUSH`). Depending on where the sensitive data is found (request/response), PCI Proxy extracts or populates sensitive data on the fly.&#x20;

## Receive from Channel

Receiving card data from a remote server (Channel) can work in two ways. In general, either you perform a [**`/v1/pull/`**](broken-reference) request to receive card data from the Channel or the Channel starts a [**`/v1/push/`**](broken-reference) request with card data. PCI Proxy can tokenize and store sensitive data on both operations.

{% tabs %}
{% tab title="PULL without PCI Proxy" %}
![](<../../.gitbook/assets/pull channel without PCIP.svg>)



1. You start a request against a Channel API endpoint.
2. The Channel returns a response containing sensitive data to you.
{% endtab %}

{% tab title="PULL via PCI Proxy" %}
![](<../../.gitbook/assets/pull channel (1) (1).svg>)

****

1. ****[**You start a request**](../../collect/filter-proxy/https/pull.md) to the PCI Proxy endpoint.
2. PCI Proxy forwards the request to the Channel API endpoint.
3. The Channel returns a response containing sensitive data to PCI Proxy.
4. PCI Proxy scans the response and tokenizes the card data.
5. PCI Proxy forwards the **response with tokens** to you.
{% endtab %}

{% tab title="PUSH without PCI Proxy" %}
![](<../../.gitbook/assets/push channel without PCIP.svg>)

1. The Channel starts a **request with card data** to your API endpoint (you are in PCI scope).
{% endtab %}

{% tab title="PUSH via PCI Proxy" %}
![](<../../.gitbook/assets/push channel (1).svg>)



1. The [**Channel starts a request**](../../collect/filter-proxy/https/push.md) with card data to a PCI Proxy endpoint.
2. PCI Proxy scans the request and tokenizes the card data.
3. PCI Proxy forwards the **request with tokens** to your API endpoint (you are out of PCI scope).
{% endtab %}
{% endtabs %}

## Forward to Receiver

Forwarding card data to a remote server (Receiver) can work in two ways. In general, either you perform a [**`/v1/pull/`**](broken-reference) request to forward card data to a Receiver or the Receiver starts a [**`/v1/push/`**](broken-reference) request to ask for card data. PCI Proxy can populate sensitive data on both operations.

{% tabs %}
{% tab title="PULL without PCI Proxy" %}
![](<../../.gitbook/assets/pull receiver without PCIP.svg>)

1. You start **request with card data** to Receiver API endpoint.
{% endtab %}

{% tab title="PULL via PCI Proxy" %}
![](<../../.gitbook/assets/pull receiver (1).svg>)

****

1. ****[**You start a request with token**](../../use/forward-proxy/https/pull.md) to a PCI Proxy endpoint.
2. PCI Proxy detokenizes and populates the request with card data.
3. PCI Proxy forwards the **request with card data** to a Receiver.&#x20;
{% endtab %}

{% tab title="PUSH without PCI Proxy" %}
![](<../../.gitbook/assets/push receiver without PCIP.svg>)

1. A Receiver starts a request to your API endpoint.
2. You return a **response with card data** to the Receiver.
{% endtab %}

{% tab title="PUSH via PCI Proxy" %}
![](<../../.gitbook/assets/push receiver (1).svg>)

1. The [**Receiver starts a request**](../../use/forward-proxy/https/push.md) to PCI Proxy endpoint.
2. PCI Proxy forwards the request to your API endpoint.
3. You return a response with tokens to PCI Proxy.
4. PCI Proxy detokenizes and populates the response body with card data.
5. PCI Proxy forwards the **response with card data** to the Receiver.
{% endtab %}
{% endtabs %}
