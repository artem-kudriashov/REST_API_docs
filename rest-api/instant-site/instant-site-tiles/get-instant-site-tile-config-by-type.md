# Get Instant Site tile config by type

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/tile/config/{configType}`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

<table><thead><tr><th width="125.37890625">Param</th><th width="99.640625">Type</th><th>Description</th></tr></thead><tbody><tr><td>storeId</td><td>number</td><td>Ecwid store ID.</td></tr><tr><td>configType</td><td>string</td><td>Type of the tile category whose config you want to get.<br><br>One of: <code>GLOBAL</code>, <code>TEXT</code>, <code>CALL_TO_ACTION</code>, <code>GIFT_CARD</code>, <code>COVER</code>, <code>STORE</code>, <code>IMAGE_TEXT</code>, <code>HEADER</code>, <code>FOOTER</code>, <code>LOCATION</code>, <code>MULTI_LOCATION</code>, <code>PRODUCT_BROWSER</code>, <code>GDPR_BANNER</code>, <code>FEATURED_PRODUCTS</code>, <code>ROOT_CATEGORIES</code>, <code>CUSTOMER_REVIEW</code>, <code>FEATURE_LIST</code>, <code>ANNOUNCEMENT_BAR</code>, <code>SLIDER</code>, <code>CUSTOM</code>, <code>CUSTOM_HEADER</code>, <code>CUSTOM_FOOTER</code>, <code>VIDEO</code>, <code>VIDEO_LIST</code>, <code>CATEGORY_PRODUCTS</code>, <code>CATEGORY_COLLECTION</code>, <code>FEATURED_PRODUCT</code>, <code>LOGO_GALLERY</code>, <code>CONTACT_US</code>, <code>AGE_CONFIRMATION</code>.</td></tr></tbody></table>

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Field</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="179.8671875">Field</th><th width="180.43359375">Type</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>string</td><td>Tile type of the requested config.</td></tr><tr><td>config</td><td>object <a data-mention href="get-instant-site-tile-config-by-type.md#config">#config</a></td><td>Details about the config.</td></tr></tbody></table>

#### config

<table><thead><tr><th width="180.4921875">Field</th><th width="180.1015625">Type</th><th>Description</th></tr></thead><tbody><tr><td>layoutConfigList</td><td>array of objects <a data-mention href="get-instant-site-tile-config-by-type.md#layoutconfiglist">#layoutconfiglist</a></td><td>Details about the layouts assigned to the config.</td></tr></tbody></table>

#### layoutConfigList

<table><thead><tr><th width="180.328125">Field</th><th width="180.0546875">Type</th><th>Description</th></tr></thead><tbody><tr><td>name</td><td>string</td><td>Internal name of the layout.</td></tr><tr><td>contentEditorConfig</td><td>object contentEditorConfig</td><td>Object with content settings available in the Instant Site editor for this layout.</td></tr><tr><td>designEditorConfig</td><td>object designEditorConfig</td><td>Object with design settings available in the Instant Site editor for this layout.</td></tr><tr><td>defaults</td><td>object defaults</td><td>Object with default content and design settings for this layout.</td></tr><tr><td>deprecated</td><td>boolean</td><td>Layout state (for internal use only). </td></tr><tr><td>svgIcon</td><td>string</td><td>Details about the SVG icon assigned to the layout (visible in the editor).</td></tr><tr><td>svgIconText</td><td>string</td><td>Hover text for the SVG icon. </td></tr></tbody></table>
