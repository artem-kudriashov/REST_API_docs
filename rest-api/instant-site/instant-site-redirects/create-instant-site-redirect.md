# Create Instant Site redirect

<mark style="color:blue;">`POST`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/instant-site/redirects`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Field</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>fromUrl</td><td>string</td><td>URL of the page from which the redirect happens.<br><br><strong>Required</strong></td></tr><tr><td>toUrl</td><td>string</td><td>URL of the page where the redirect leads users.<br><br><strong>Required</strong></td></tr></tbody></table>
