# Delete Instant Site theme

<mark style="color:red;">`DELETE`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/themes/{themeId}`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description                     |
| ------- | ------ | ------------------------------- |
| storeId | number | Ecwid store ID.                 |
| themeId | string | Internal Instant Site theme ID. |

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="210.3515625">Field</th><th width="119.7421875">Type</th><th>Description</th></tr></thead><tbody><tr><td>themeId</td><td>string</td><td>Internal theme ID.</td></tr><tr><td>colors</td><td>object <a data-mention href="delete-instant-site-theme.md#colors">#colors</a></td><td>List of theme colors forming its palette.</td></tr></tbody></table>

#### colors

<table><thead><tr><th width="210.3515625">Field</th><th width="119.7421875">Type</th><th>Description</th></tr></thead><tbody><tr><td>colorA</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorB</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorC</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorD</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorE</td><td>string</td><td>One of the theme colors defining global palette.</td></tr><tr><td>colorF</td><td>string</td><td>One of the theme colors defining global palette.</td></tr></tbody></table>
