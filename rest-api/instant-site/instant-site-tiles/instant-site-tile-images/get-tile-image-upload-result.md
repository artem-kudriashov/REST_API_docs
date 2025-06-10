# Get tile image upload result

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/image/{imageId}`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

<table><thead><tr><th width="138.4140625">Param</th><th width="86.296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>storeId</td><td>number</td><td>Ecwid store ID.</td></tr><tr><td>imageId</td><td>string</td><td>Internal tile image ID received in <a data-mention href="upload-instant-site-tile-image.md">upload-instant-site-tile-image.md</a> request.</td></tr></tbody></table>

### Headers

Both headers are **required**.

<table><thead><tr><th width="138.484375">Header</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../../get-instant-site-api-token-apiv1.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>bucket</td><td>string</td><td>Internal ID of the bucket – server that hosts the uploaded image. For example, <code>"eu-fra"</code>.<br><br>Use <a data-mention href="get-list-of-buckets-for-tile-images.md">get-list-of-buckets-for-tile-images.md</a> request to get the bucket's URL. Then combine it with the <code>set</code> > <code>url</code> from this request to get the full image URL.</td></tr><tr><td>set</td><td>array of objects <a data-mention href="get-tile-image-upload-result.md#set">#set</a></td><td>Details about tile image in one or several sizes.</td></tr><tr><td>borderInfo</td><td>object <a data-mention href="get-tile-image-upload-result.md#borderinfo">#borderinfo</a></td><td>Image border details.</td></tr></tbody></table>

#### set

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>url</td><td>string</td><td>Link to the image. Does not include bucket, for example, <code>"1003/cover-Zm***N/7xGvpFA-600x600.web"</code>.</td></tr><tr><td>width</td><td>number</td><td>Image width in px.</td></tr><tr><td>height</td><td>number</td><td>Image height in px.</td></tr></tbody></table>

#### borderInfo

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>homogeneity</td><td>boolean</td><td>Defines if the image border is homogeneous (<code>true</code>) or not (<code>false</code>).</td></tr><tr><td>color</td><td>object <a data-mention href="get-tile-image-upload-result.md#color">#color</a></td><td>Border color in RGBa.</td></tr></tbody></table>

#### color

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>r</td><td>number</td><td>Red channel value.</td></tr><tr><td>g</td><td>number</td><td>Green channel value.</td></tr><tr><td>b</td><td>number</td><td>Blue channel value.</td></tr><tr><td>a</td><td>number</td><td>Alpha channel value (opacity).</td></tr></tbody></table>
