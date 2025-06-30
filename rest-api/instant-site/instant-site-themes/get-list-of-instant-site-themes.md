# Get list of Instant Site themes

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/themes`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Field</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token-apiv1.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="210.3515625">Field</th><th width="119.7421875">Type</th><th>Description</th></tr></thead><tbody><tr><td>themes</td><td>object <a data-mention href="get-list-of-instant-site-themes.md#themes">#themes</a></td><td>List of themes available on the Instant Site.</td></tr></tbody></table>

#### themes

<table><thead><tr><th width="210.3515625">Field</th><th width="119.7421875">Type</th><th>Description</th></tr></thead><tbody><tr><td>themeId</td><td>string</td><td>Internal theme ID.</td></tr><tr><td>colors</td><td>object <a data-mention href="get-list-of-instant-site-themes.md#colors">#colors</a></td><td>List of theme colors forming its palette.</td></tr></tbody></table>

#### colors

<table><thead><tr><th width="210.3515625">Field</th><th width="119.7421875">Type</th><th>Description</th></tr></thead><tbody><tr><td>colorA</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorB</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorC</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorD</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorE</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorF</td><td>string</td><td>One of the theme colors defining global palette.</td></tr></tbody></table>

