---
description: Manage your aliases
---

# Manage

The alias manage APIs offers you a set of APIs to interact and work with the aliases you have created and stored on your servers.&#x20;

The operations possible range from requesting payment method meta data, to updating an existing alias to delete or block them and much more. Read below in detail what each of the APIs offers and what's fitting best to your requirement.&#x20;

{% hint style="warning" %}
Please note that the alias manage APIs are only working with the two latest [Alias 2.0 format](../../resources/token-formats.md#alias-2.0). Please reach out to your PCI Proxy contact if you are not sure which alias format you are using.
{% endhint %}

{% content-ref url="status.md" %}
[status.md](status.md)
{% endcontent-ref %}

The alias status API returns detailed information about the alias and the underlying card itself, such as the fingerprint, masked card value and card meta data. Additionally use this API to check wheter a Network Token has been issued. In that case, you can also check if the card expiry date has been updated.&#x20;

{% content-ref url="patch.md" %}
[patch.md](patch.md)
{% endcontent-ref %}

Update an existing alias with the expiry month and year if not already done in the initial alias creation process or remove the underlying PAN of an alias from storage.&#x20;

{% content-ref url="delete.md" %}
[delete.md](delete.md)
{% endcontent-ref %}

Delete an alias with immediate effect.&#x20;

{% content-ref url="check.md" %}
[check.md](check.md)
{% endcontent-ref %}

Check if the card is still valid by running a zero-amount request against the card schemes. The response tells you if a card has been stolen, expired or simply blocked.&#x20;

{% content-ref url="convert.md" %}
[convert.md](convert.md)
{% endcontent-ref %}

Convert an old alias format to an [Alias 2.0 format](../../resources/token-formats.md).&#x20;

{% content-ref url="block.md" %}
[block.md](block.md)
{% endcontent-ref %}

Blacklist suspicious aliases.&#x20;
