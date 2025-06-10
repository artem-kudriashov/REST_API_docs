# Update Instant Site profile

<mark style="color:purple;">`PUT`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/profile`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Header</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token-apiv1.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Request JSON

A JSON object with the following fields:

<table><thead><tr><th width="238.53125">Field</th><th width="137.38671875">Type</th><th>Description</th></tr></thead><tbody><tr><td>locale</td><td>string</td><td>Site locale that matches the default website language.</td></tr><tr><td>enabledLanguages</td><td>array of strings</td><td>List of enabled languages.</td></tr><tr><td>storeName</td><td>string</td><td>Name of the website used in SEO and visible in browser tabs.</td></tr><tr><td>countryCode</td><td>string</td><td>Two-digit country code of the store location.</td></tr><tr><td>postalCode</td><td>string</td><td>ZIP code of the store location.</td></tr><tr><td>email</td><td>string</td><td>Email specified as the "store email" in the Instant Site editor.</td></tr><tr><td>dateFormat</td><td>string</td><td>Date format used on the website, for example, <code>"dd.MM.yyyy"</code>.</td></tr><tr><td>timeFormat</td><td>string</td><td>Time format used on the website, for example, <code>"HH:mm:ss"</code>.</td></tr><tr><td>timezoneOffsetInMinutes</td><td>number</td><td>Offset of the store time from the UTC +0 in minutes.</td></tr></tbody></table>

