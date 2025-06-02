# Get list of buckets for tile images

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/image/bucket`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

<table><thead><tr><th width="138.4140625">Param</th><th width="86.296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>storeId</td><td>number</td><td>Ecwid store ID.</td></tr></tbody></table>

### Headers

Both headers are **required**.

<table><thead><tr><th width="138.484375">Header</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../../get-instant-site-api-token.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>urls</td><td>object <a data-mention href="get-list-of-buckets-for-tile-images.md#urls">#urls</a></td><td>Map of tile image bucket IDs and their URLs.</td></tr></tbody></table>

#### urls

JSON object, where the key is the bucket ID, and the value is this bucket's URL. For example:

<pre class="language-json"><code class="lang-json"><strong>{
</strong><strong>    "urls": {
</strong><strong>        "au-syd": "https://dfvc2y3mjtc8v.cloudfront.net",
</strong>        "us-vir": "https://dhgf5mcbrms62.cloudfront.net",
        "eu-fra": "https://d2gt4h1eeousrn.cloudfront.net"
<strong>    }
</strong><strong>}
</strong></code></pre>
