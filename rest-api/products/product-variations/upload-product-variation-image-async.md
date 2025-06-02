# Upload product variation image (async)

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/products/{productId}/combinations/{combinationId}/image/async`&#x20;

### Required access scopes

Your app must have the following **access scopes** to make this request: `read_catalog`, `update_catalog`

### Path params

All path params are required.

| Param         | Type   | Description                    |
| ------------- | ------ | ------------------------------ |
| storeId       | number | Ecwid store ID.                |
| productId     | number | Internal product ID.           |
| combinationId | number | Internal product variation ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

### Request JSON

A JSON object with the following fields:

| Field      | Type                                                      | Description                                                                                              |
| ---------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| url        | string                                                    | <p>HTTPS link to the image file that will be uploaded to the store.<br><br><strong>Required</strong></p> |
| width      | string                                                    | <p>Width of the image. <br><br><strong>Required</strong></p>                                             |
| height     | string                                                    | <p>Height of the image. <br><br><strong>Required</strong></p>                                            |
| externalId | string                                                    | Internal image ID for Lightspeed R-Series/X-Series image sync.                                           |
| alt        | object [alt](upload-product-variation-image-async.md#alt) | Information about the image alt text.                                                                    |

#### alt

<table><thead><tr><th width="150">Field</th><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>main</td><td>string</td><td>Image alt text in the main store language.</td></tr><tr><td>translated</td><td>object <a href="upload-product-variation-image-async.md#translated">translated</a></td><td>Image alt text translations.</td></tr></tbody></table>

#### translated

Object with text field translations in the `"lang": "text"` format, where the `"lang"` is an ISO 639-1 language code. For example:

```
{
    "en": "Sample text",
    "nl": "Voorbeeldtekst"
}
```

Translations are available for all active store languages. Only the default language translations are returned if no other translations are provided for the field. Find active store languages with <mark style="color:green;">`GET`</mark> `/profile` request > `languages` > `enabledLanguages`.

### Response JSON

A JSON object with the following fields:

| Field | Type   | Description                        |
| ----- | ------ | ---------------------------------- |
| id    | number | Internal ID of the uploaded image. |
