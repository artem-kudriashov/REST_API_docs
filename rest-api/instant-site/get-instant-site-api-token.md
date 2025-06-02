# Get Instant Site API token

<mark style="color:blue;">`POST`</mark> `https://vuega.ecwid.com/api/v1/oauth/token?grant_type={grant_type}&site_id={site_id}&code={code}`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Query params

All query params are **required**.

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>grant_type</td><td>string</td><td><p>Type of the generated token that defines if it can apply any changes to Instant Site.</p><p></p><p>One of: </p><p><code>authorization_code</code> - generated token grants full access to Instant Site API methods</p><p><code>draft_code</code> - generated token only allows opening the Instant Site editor and can't be used for API requests</p></td></tr><tr><td>site_id</td><td>number</td><td>Ecwid store ID.</td></tr><tr><td>code</td><td>string</td><td>App's <code>secret_token</code>. <br><br>The app must have the <code>manage_instant_site</code> access scope.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

| Header      | Type   | Description                                                                                                                           |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------- |
| accessToken | string | <p>Token for Instant Site API calls. <br><br>Requires <code>authorization_code</code> in the <code>grant_type</code> query param.</p> |
| tokenType   | string | Type of the received token. Always `bearer`.                                                                                          |
| expiresIn   | number | Token's expiration time in milliseconds. For example, `86400`.                                                                        |

