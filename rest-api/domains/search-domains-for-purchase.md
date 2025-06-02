# Search domains for purchase

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/{storeId}domains/search?keyword={keyword}`&#x20;

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

Request works with one **required** query param.

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>keyword</td><td>boolean</td><td>Search term for the domain name.<br><br><strong>Required</strong></td></tr></tbody></table>

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

{% include "../../.gitbook/includes/rest-api-response-json.md" %}

| Field   | Type                                                     | Description                          |
| ------- | -------------------------------------------------------- | ------------------------------------ |
| keyword | string                                                   | Keyword used for the search request. |
| domains | object [domains](search-domains-for-purchase.md#domains) | Domains found by keyword.            |

#### domains

| Field          | Type   | Description                                                                                         |
| -------------- | ------ | --------------------------------------------------------------------------------------------------- |
| name           | string | Domain name, for example. `"mysuperstore.info"` or `"mysuperstore.com"`                             |
| status         | string | Status of domain. Possible values: `"available"` if domain is available to buy, `"taken"` otherwise |
| price          | number | Domain price.                                                                                       |
| currency       | string | Currency used to buy domain, e.g. `"USD"`                                                           |
| priceFormatted | string | Domain price in a string format, including price and currency, e.g. `"$100.00"`                     |

