# Get store

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/stores?email={email}`

### Required access scopes

This API call requires the following access scope: `read_stores`

### Headers

All request headers are **required**.

<table><thead><tr><th width="225.734375">Header</th><th width="140.7890625">Type</th><th>Description</th></tr></thead><tbody><tr><td>X-Ecwid-App-Client-Id</td><td>string</td><td>Your application’s <code>client_id</code></td></tr><tr><td>X-Ecwid-App-Secret-Key</td><td>string</td><td>Your application’s <code>client_secret</code></td></tr></tbody></table>

### Query params

All query params are optional.

<table><thead><tr><th width="137.75390625">Name</th><th width="112.5625">Type</th><th>Description</th></tr></thead><tbody><tr><td>email</td><td>string</td><td>Store owner’s email address.<br><br><strong>Required</strong></td></tr><tr><td>facebookID</td><td>string</td><td>Store owner’s Facebook account ID.</td></tr><tr><td>googleID</td><td>string</td><td>Store owner’s Google account ID.</td></tr></tbody></table>

### Response JSON

HTTP status `200 OK` with an empty JSON object indicates that the store is already registered in Ecwid. Every other response (except HTP status 500) means no Ecwid stores exist with the specified email.
