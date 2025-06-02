# Delete Instant Site tile

<mark style="color:red;">`DELETE`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/tile/{tileId}`

{% hint style="info" %}
When the tile is deleted with this API request, it also gets deleted from all pages where it was previously available.
{% endhint %}

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description       |
| ------- | ------ | ----------------- |
| storeId | number | Ecwid store ID.   |
| tileId  | string | Internal tile ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Header</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

