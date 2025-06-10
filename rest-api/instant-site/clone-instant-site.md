# Clone Instant Site

<mark style="color:blue;">`POST`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/clone`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`, `clone_stores`

### Path params

All path params are **required**.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Header</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="get-instant-site-api-token-apiv1.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Request JSON

A JSON object with the following fields:

<table><thead><tr><th width="138.484375">Field</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>source</td><td>number</td><td>ID of the source Ecwid store whose settings should be cloned to a new one.</td></tr><tr><td>draft</td><td>boolean</td><td>Define if the copied site settings are published right away (<code>false</code>) or saved as a draft in the target store (<code>true</code>).</td></tr></tbody></table>
