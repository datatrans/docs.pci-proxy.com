# Request Types

In general, either **you start a request** (`PULL`) or **a remote server starts a request** (`PUSH`). Depending on where to find sensitive data (request/response), PCI Proxy extracts or populates sensitive data on the fly.

## Receive from Channel

Receiving card data from a remote server (Channel) can work in two ways. In general, either you perform a [**`/v1/pull/`**](../collect-and-store-cards/filter-payloads/#pull-method) request to receive card data from the Channel or the Channel starts a [**`/v1/push/`**](../collect-and-store-cards/filter-payloads/#push-method) request with card data. PCI Proxy can tokenize and store sensitive data on both operations.

{% tabs %}
{% tab title="PULL without PCI Proxy" %}
![](<../.gitbook/assets/channel\_pull\_status\_quo\_color (5).png>)

1. You start a request against Channel API endpoint.
2. Channel returns **response with card data** to you.
{% endtab %}

{% tab title="PULL via PCI Proxy" %}
![](<../.gitbook/assets/channel\_pull\_pciproxy\_color (4).png>)

1. [**You start a request**](../collect-and-store-cards/filter-payloads/#pull-method) against PCI Proxy endpoint.
2. PCI Proxy forward request to Channel API endpoint.
3. Channel returns response with card data to PCI Proxy.
4. PCI Proxy scans response and tokenizes card data.
5. PCI Proxy forward **response with tokens** to you.
{% endtab %}

{% tab title="PUSH without PCI Proxy" %}
![](<../.gitbook/assets/channel\_push\_status\_quo\_color (2).png>)

1. Channel starts a **request with card data** to your API endpoint (you are in PCI scope).
{% endtab %}

{% tab title="PUSH via PCI Proxy" %}
![](<../.gitbook/assets/channel\_push\_pciproxy\_color (3).png>)

1. [**Channel starts request**](../collect-and-store-cards/filter-payloads/#push-method) with card data to PCI Proxy endpoint.
2. PCI Proxy scans request and tokenizes card data.
3. PCI Proxy forwards **request with tokens** to your API endpoint (you are out of PCI scope).
{% endtab %}
{% endtabs %}

## Forward to Receiver

Forwarding card data to a remote server (Receiver) can work in two ways. In general, either you perform a [**`/v1/pull/`**](../use-stored-cards/forward/https/#pull-method) request to forward card data to a Receiver or the Receiver starts a [**`/v1/push/`**](../use-stored-cards/forward/https/#push-method) request to ask for card data. PCI Proxy can populate sensitive data on both operations.

{% tabs %}
{% tab title="PULL without PCI Proxy" %}
![](<../.gitbook/assets/receiver\_pull\_status\_quo\_color (2).png>)

1. You start **request with card data** to Receiver API endpoint.
{% endtab %}

{% tab title="PULL via PCI Proxy " %}
![](<../.gitbook/assets/receiver\_pull\_pciproxy\_color (4).png>)

1. [**You start a request with token**](../use-stored-cards/forward/https/#pull-method) to PCI Proxy endpoint.
2. PCI Proxy detokenizes and populates request with card data.
3. PCI Proxy forwards **request with card data** to Receiver.
{% endtab %}

{% tab title="PUSH without PCI Proxy" %}
![](<../.gitbook/assets/receiver\_push\_status\_quo\_color (2).png>)

1. Receiver starts a request to your API endpoint.
2. You return **response with card data** to Receiver.
{% endtab %}

{% tab title="PUSH via PCI Proxy" %}
![](<../.gitbook/assets/receiver\_push\_pciproxy\_color (3).png>)

1. [**Receiver starts request**](../use-stored-cards/forward/https/#push-method) to PCI Proxy endpoint.
2. PCI Proxy forwards request to your API endpoint.
3. You return a response with token to PCI Proxy.
4. PCI Proxy detokenizes and populates response with card data.
5. PCI Proxy forwards **response with card data** to Receiver.
{% endtab %}
{% endtabs %}
