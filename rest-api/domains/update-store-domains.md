# Update store domains

<mark style="color:purple;">`PUT`</mark> `https://app.ecwid.com/api/v3/{storeId}/domains`&#x20;

### Required access scopes

Your app must have the following **access scopes** to make this request: `update_store_profile`, `buy_domains`

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

### Request JSON

A JSON object with the following fields:

| Field             | Type                                                                          | Description                                             |
| ----------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------- |
| instantSiteDomain | object [instantSiteDomain](update-store-domains.md#instantsitedomain)         | Details for the currently enabled store domain.         |
| purchasedDomains  | array of objects [purchasedDomains](update-store-domains.md#purchaseddomains) | List with details for each domain bought for the store. |

#### instantSiteDomain

| Field                  | Type   | Description                                                                                                               |
| ---------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------- |
| ecwidSubdomain         | string | Subdomain of the default Instant Site URL.                                                                                |
| thirdPartyVendorDomain | string | Custom domain specified in the Control Panel settings. Has the same value as the `customDomain` in the Instant Site Info. |

#### purchasedDomains

| Field                  | Type    | Description                                                                          |
| ---------------------- | ------- | ------------------------------------------------------------------------------------ |
| connectedToInstantSite | boolean | Shows if this domain is connected to Instant Site. Available values: `true`, `false` |
| primaryDomain          | boolean | Shows if this domain is the main one. Available values: `true`, `false`              |
| autorenew              | boolean | Shows if automatic renewal charge is enabled. Available values: `true`, `false`      |

{% include "../../.gitbook/includes/rest-api-response-json.md" %}

| Field       | Type   | Description                                                                                                                                                                             |
| ----------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateCount | number | <p>The number of updated items that defines if the request was successful.<br><br>One of:<br><code>1</code> if the item was updated,<br><code>0</code> if the item was not updated.</p> |
