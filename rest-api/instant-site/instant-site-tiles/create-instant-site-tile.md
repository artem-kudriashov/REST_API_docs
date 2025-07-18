# Create Instant Site tile

<mark style="color:blue;">`POST`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/tile`

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

<table><thead><tr><th width="174.99609375">Field</th><th width="134.6875">Type</th><th>Description</th></tr></thead><tbody><tr><td>tileShowcaseItemId</td><td>string</td><td>Internal tile ID.</td></tr><tr><td>tileCategoryType</td><td>string</td><td>Tile category type. Tile is placed into the matching category in the Instant Site editor. <br><br>One of: <code>HEADER</code>, <code>COVER</code>, <code>SPECIAL_OFFER</code>, <code>COMPANY_INFO</code>, <code>SHIPPING_PAYMENT</code>, <code>STORE</code>, <code>LOCATION</code>, <code>CUSTOMER_REVIEW</code>, <code>ANNOUNCEMENT</code>, <code>SLIDER</code>, <code>TEMPLATE</code>, <code>CUSTOM</code>, <code>VIDEO</code>, <code>VIDEO_LIST</code>, <code>LOGO_GALLERY</code>, <code>FEATURED_PRODUCT</code>, <code>CATEGORY_PRODUCTS</code>, <code>CATEGORY_COLLECTION</code>, <code>FOOTER</code>, <code>CONTACT_US</code>.</td></tr><tr><td>tileOrder</td><td>number</td><td>Order in the tiles list where the new tile should appear.</td></tr><tr><td>useTileShowcase</td><td>boolean</td><td>Define if the new tile should use showcase settings.</td></tr><tr><td>tile</td><td>object <a data-mention href="create-instant-site-tile.md#tile">#tile</a></td><td>Internal ID of the tile pre-built by the Ecwid team.</td></tr><tr><td>pageId</td><td>string</td><td>Internal page ID where the tile should be added.</td></tr></tbody></table>

#### tile

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>string</td><td>Tile type that defines its functionality. <br><br>One of: <code>GLOBAL</code>, <code>TEXT</code>, <code>CALL_TO_ACTION</code>, <code>CONTACT_INFO_CALL_TO_ACTION</code>, <code>GIFT_CARD</code>, <code>COVER</code>, <code>STORE</code>, <code>IMAGE_TEXT</code>, <code>HEADER</code>, <code>FOOTER</code>, <code>LOCATION</code>, <code>MULTI_LOCATION</code>, <code>PRODUCT_BROWSER</code>, <code>GDPR_BANNER</code>, <code>FEATURED_PRODUCTS</code>, <code>ROOT_CATEGORIES</code>, <code>CUSTOMER_REVIEW</code>, <code>FEATURE_LIST</code>, <code>ANNOUNCEMENT_BAR</code>, <code>SLIDER</code>, <code>CUSTOM</code>, <code>CUSTOM_HEADER</code>, <code>CUSTOM_FOOTER</code>, <code>VIDEO</code>, <code>VIDEO_LIST</code>, <code>CATEGORY_PRODUCTS</code>, <code>CATEGORY_COLLECTION</code>, <code>FEATURED_PRODUCT</code>, <code>LOGO_GALLERY</code>, <code>CONTACT_US</code>, <code>AGE_CONFIRMATION</code>.</td></tr><tr><td>tileName</td><td>string</td><td>Name of the website used in SEO and visible in browser tabs.</td></tr><tr><td>content</td><td>object content</td><td>Tile content, such as texts and images, manageable through the Instant Site editor.</td></tr><tr><td>design</td><td>object design</td><td>Design settings available in the Instant Site editor for tile content from the <code>content</code> object.</td></tr><tr><td>visibility</td><td>boolean</td><td>Visibility of the tile on the storefront. If <code>true</code>, the tile is visible.</td></tr><tr><td>order</td><td>number</td><td>Order in the tiles list defining their order on the storefront from top to bottom. Starts with <code>0</code> (displayed at the top) and increments by <code>1</code>.</td></tr><tr><td>hasChanges</td><td>boolean</td><td>Defines if the draft has changes from the published version.</td></tr></tbody></table>



