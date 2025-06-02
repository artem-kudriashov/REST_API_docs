# Upload Instant Site tile image

<mark style="color:blue;">`POST`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/tile/{tileId}/image`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description       |
| ------- | ------ | ----------------- |
| storeId | number | Ecwid store ID.   |
| tileId  | string | Internal tile ID. |

### Headers

Both headers are **required**.

<table><thead><tr><th width="138.484375">Header</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../../get-instant-site-api-token.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr><tr><td>Content-type</td><td>string</td><td>Must be <code>application/json</code></td></tr></tbody></table>

### Request JSON

A JSON object with the following fields:

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>acceptHeader</td><td>string</td><td>Must be <code>multipart/form-data</code>.<br><br><strong>Required</strong></td></tr></tbody></table>

JSON in the request body must look like:

```json
{
    "acceptHeader": "multipart/form-data"  
}
```

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>url</td><td>string</td><td>URL for uploading the image. <br><br>Image must be uploaded through a <mark style="color:blue;"><code>POST</code></mark> request with the <code>Content-Type: multipart/form-data</code> header and image <strong>binary data</strong> in the request body.</td></tr><tr><td>id</td><td>string</td><td>Internal ID reserved for the image. <br><br>Use <a data-mention href="get-tile-image-upload-result.md">get-tile-image-upload-result.md</a> request to check the status and details after uploading the image.</td></tr></tbody></table>
