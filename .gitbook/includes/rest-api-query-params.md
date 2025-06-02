---
title: 'REST API: query params'
---

## Query params

All query params are optional.

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>showExtendedInfo</td><td>boolean</td><td>Set <code>true</code> to receive additional store profile data including account/billing data. Requires <code>read_store_profile_extended</code> access scope.</td></tr><tr><td>lang</td><td>string</td><td>Language ISO code for translations in JSON response, e.g. <code>en</code>, <code>fr</code>. Translates fields like: <code>title</code>, <code>description</code>, <code>pickupInstruction</code>, <code>text</code>, etc.</td></tr><tr><td>responseFields</td><td>string</td><td>Specify the exact fields to receive in response JSON. If not specified, the response JSON will have all available fields for the entity.<br>Example: <code>?responseFields=generalInfo(storeId,storeUrl)</code></td></tr></tbody></table>

Example of using `responseFields` param:

{% tabs %}
{% tab title="Request" %}
```
curl --location 'https://app.ecwid.com/api/v3/1003/profile?responseFields=generalInfo(storeId,storeUrl)' \
--header 'Authorization: Bearer secret_ab***cd'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "generalInfo": {
        "storeId": 1003,
        "storeUrl": "https://store1003.company.site/"
    }
}
```
{% endtab %}
{% endtabs %}
