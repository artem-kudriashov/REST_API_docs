# Search Instant Site redirects

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/instant-site/redirects`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

All query params are optional.

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>keyword</td><td>string</td><td>Search string for URLs of saved Instant Site redirects.</td></tr></tbody></table>

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Field</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="180.06640625">Field</th><th width="180.40234375">Type</th><th>Description</th></tr></thead><tbody><tr><td>total</td><td>number</td><td>Total number of found items (might be more than the number of returned items).</td></tr><tr><td>count</td><td>number</td><td>Total number of items returned in the response.</td></tr><tr><td>offset</td><td>number</td><td>Offset from the beginning of the returned items list specified in the request.</td></tr><tr><td>limit</td><td>number</td><td>Maximum number of returned items specified in the request. Maximum and default value: <code>100</code>.</td></tr><tr><td>items</td><td>array of objects <a data-mention href="search-instant-site-redirects.md#items">#items</a></td><td>Detailed information about returned Instant Site redirects.</td></tr></tbody></table>

#### items

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>Internal ID of the Instant Site redirect.</td></tr><tr><td>fromUrl</td><td>string</td><td>URL of the page from which the redirect happens.</td></tr><tr><td>toUrl</td><td>string</td><td>URL of the page where the redirect leads users.</td></tr></tbody></table>
