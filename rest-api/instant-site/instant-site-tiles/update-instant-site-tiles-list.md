# Update Instant Site tiles list

<mark style="color:purple;">`PUT`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/tile`

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

### Request JSON

A JSON object with the following fields:

<table><thead><tr><th width="138.484375">Field</th><th width="149.97265625">Type</th><th>Description</th></tr></thead><tbody><tr><td>tiles</td><td>array of objects <a data-mention href="update-instant-site-tiles-list.md#tiles">#tiles</a></td><td>List of tiles for the update.</td></tr></tbody></table>

#### tiles

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>Internal tile ID.</td></tr><tr><td>tileName</td><td>string</td><td>Name of the website used in SEO and visible in browser tabs.</td></tr><tr><td>content</td><td>object content</td><td>Tile content, such as texts and images, manageable through the Instant Site editor.</td></tr><tr><td>design</td><td>object design</td><td>Design settings available in the Instant Site editor for tile content from the <code>content</code> object.</td></tr><tr><td>visibility</td><td>boolean</td><td>Visibility of the tile on the storefront. If <code>true</code>, the tile is visible.</td></tr><tr><td>order</td><td>number</td><td>Order in the tiles list defining their order on the storefront from top to bottom. Starts with <code>0</code> (displayed at the top) and increments by <code>1</code>.</td></tr><tr><td>hasChanges</td><td>boolean</td><td>Defines if the draft has changes from the published version.</td></tr></tbody></table>



