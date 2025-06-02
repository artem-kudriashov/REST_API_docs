# Get Instant Site tile showcases

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/tile/showcase`

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

| Field      | Type                                                                          | Description                                      |
| ---------- | ----------------------------------------------------------------------------- | ------------------------------------------------ |
| categories | object [#categories](get-instant-site-tile-showcases.md#categories "mention") | List of received tile categories and their data. |

#### categories

<table><thead><tr><th width="149.98046875">Field</th><th width="149.52734375">Type</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>string</td><td>Tile category type. Tiles are placed into the matching categories in the Instant Site editor. <br><br>One of: <code>HEADER</code>, <code>COVER</code>, <code>SPECIAL_OFFER</code>, <code>COMPANY_INFO</code>, <code>SHIPPING_PAYMENT</code>, <code>STORE</code>, <code>LOCATION</code>, <code>CUSTOMER_REVIEW</code>, <code>ANNOUNCEMENT</code>, <code>SLIDER</code>, <code>TEMPLATE</code>, <code>CUSTOM</code>, <code>VIDEO</code>, <code>VIDEO_LIST</code>, <code>LOGO_GALLERY</code>, <code>FEATURED_PRODUCT</code>, <code>CATEGORY_PRODUCTS</code>, <code>CATEGORY_COLLECTION</code>, <code>FOOTER</code>, <code>CONTACT_US</code>.</td></tr><tr><td>items</td><td>array of objects <a data-mention href="get-instant-site-tile-showcases.md#items">#items</a></td><td>Showcase details: internal ID, image URL, width, height.</td></tr></tbody></table>

#### items

<table><thead><tr><th width="149.98046875">Field</th><th width="149.52734375">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>Internal ID of the showcase.</td></tr><tr><td>previewImageUrl</td><td>string</td><td>Link to the showcase preview image. Users see this image in the Instant Site editor when adding new tiles.</td></tr><tr><td>previewHeight</td><td>number</td><td>Height of the showcase preview image.</td></tr><tr><td>previewWidth</td><td>number</td><td>Width of the showcase preview image.</td></tr><tr><td>featureProperty</td><td>string</td><td>Internal text for the feature description showcased in the tile. Available only for tiles built by the Ecwid team. </td></tr><tr><td>isDeprecated</td><td>boolean</td><td>Internal field that marks older tiles built by the Ecwid team.</td></tr></tbody></table>
