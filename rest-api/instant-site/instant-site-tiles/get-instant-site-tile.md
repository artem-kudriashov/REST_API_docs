# Get Instant Site tile

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/tile/{tileId}`

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

<table><thead><tr><th width="138.484375">Field</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>Internal tile ID.</td></tr><tr><td>type</td><td>string</td><td>Tile type that defines its functionality. <br><br>One of: <code>GLOBAL</code>, <code>TEXT</code>, <code>CALL_TO_ACTION</code>, <code>GIFT_CARD</code>, <code>COVER</code>, <code>STORE</code>, <code>IMAGE_TEXT</code>, <code>HEADER</code>, <code>FOOTER</code>, <code>LOCATION</code>, <code>MULTI_LOCATION</code>, <code>PRODUCT_BROWSER</code>, <code>GDPR_BANNER</code>, <code>FEATURED_PRODUCTS</code>, <code>ROOT_CATEGORIES</code>, <code>CUSTOMER_REVIEW</code>, <code>FEATURE_LIST</code>, <code>ANNOUNCEMENT_BAR</code>, <code>SLIDER</code>, <code>CUSTOM</code>, <code>CUSTOM_HEADER</code>, <code>CUSTOM_FOOTER</code>, <code>VIDEO</code>, <code>VIDEO_LIST</code>, <code>CATEGORY_PRODUCTS</code>, <code>CATEGORY_COLLECTION</code>, <code>FEATURED_PRODUCT</code>, <code>LOGO_GALLERY</code>, <code>CONTACT_US</code>, <code>AGE_CONFIRMATION</code>.</td></tr><tr><td>role</td><td>string</td><td>Tile role. One of: <code>BLOCK</code>, <code>NOTICE</code>.</td></tr><tr><td>tileName</td><td>string</td><td>Name of the website used in SEO and visible in browser tabs.</td></tr><tr><td>sourceId</td><td>string</td><td>Internal ID of the tile pre-built by the Ecwid team.</td></tr><tr><td>content</td><td>object content</td><td>Tile content, such as texts and images, manageable through the Instant Site editor.</td></tr><tr><td>externalContent</td><td>object externalContent</td><td>Tile content unavailable in the Instant Site editor, such as information about store products or external links to legal pages. </td></tr><tr><td>design</td><td>object design</td><td>Design settings available in the Instant Site editor for tile content from the <code>content</code> object.</td></tr><tr><td>visibility</td><td>boolean</td><td>Visibility of the tile on the storefront. If <code>true</code>, the tile is visible.</td></tr><tr><td>order</td><td>number</td><td>Order in the tiles list defining their order on the storefront from top to bottom. Starts with <code>0</code> (displayed at the top) and increments by <code>1</code>.</td></tr><tr><td>hasChanges</td><td>boolean</td><td>Defines if the draft has changes from the published version.</td></tr><tr><td>featuresEnabled</td><td>object featuresEnabled</td><td>Internal list of features enabled for this tile.</td></tr></tbody></table>



