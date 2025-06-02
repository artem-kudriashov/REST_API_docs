# Create store

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/stores`

### Required access scopes

This API call requires the following access scope: `create_stores`

### Headers

All request headers are **required**.

<table><thead><tr><th width="225.734375">Header</th><th width="140.7890625">Type</th><th>Description</th></tr></thead><tbody><tr><td>X-Ecwid-App-Client-Id</td><td>string</td><td>Your application’s <code>client_id</code></td></tr><tr><td>X-Ecwid-App-Secret-Key</td><td>string</td><td>Your application’s <code>client_secret</code></td></tr></tbody></table>

### Query params

All query params are optional

| Name           | Type    | Description                                                                                                                                                                                                          |
| -------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| returnApiToken | boolean | `true`to include token into API response. When a store is successfully created, API will return Store ID ('id') of the created store and API token that should be saved and used later for API calls for this store. |

### Request JSON

| Field            | Type                                                        | Description                                                         |
| ---------------- | ----------------------------------------------------------- | ------------------------------------------------------------------- |
| merchant         | object [merchant](create-store.md#merchant)                 | <p>Store owner’s account data.<br><br><strong>Required</strong></p> |
| affiliatePartner | object [affiliatePartner](create-store.md#affiliatepartner) | Affiliate partner data.                                             |
| profile          | object [profile](create-store.md#profile)                   | General settings for the new store.                                 |

#### merchant

<table><thead><tr><th width="170.7265625">Field</th><th width="196.9296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>email</td><td>string</td><td>Store owner’s email.<br><br><strong>Required</strong></td></tr><tr><td>name</td><td>string</td><td>Store owner’s name.<br><br><strong>Required</strong></td></tr><tr><td>password</td><td>string</td><td>Ecwid account password. Minimum password length is 6 characters.</td></tr><tr><td>ip</td><td>string</td><td>Store owner’s IP. Is used to predetermine user’s location and set default settings in store</td></tr><tr><td>facebookLogin</td><td>object <a href="create-store.md#facebooklogin">facebookLogin</a></td><td>Merchant's Facebook login info – when creating account via social buttons. Use Facebook or Google info for registration with social account. Facebook email and name will be used for this Ecwid account if available in Facebook</td></tr><tr><td>googleLogin</td><td>object <a href="create-store.md#googlelogin">googleLogin</a></td><td>Merchant's Google login info – when creating account via social buttons. Use Facebook or Google info for registration with social account. Google email and name will be used for this Ecwid account if available on Google</td></tr></tbody></table>

#### facebookLogin

| Field         | Type   | Description                  |
| ------------- | ------ | ---------------------------- |
| facebookID    | string | Store owner’s Facebook ID    |
| facebookToken | string | Store owner’s Facebook token |

#### googleLogin

| Field       | Type   | Description                |
| ----------- | ------ | -------------------------- |
| googleToken | string | Store owner’s Google token |

#### affiliatePartner

| Field      | Type                                            | Description                                                                                                                     |
| ---------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| source     | string                                          | Determines the source of the registered account                                                                                 |
| ambassador | object [ambassador](create-store.md#ambassador) | Ambassador affiliate account details. [More info](https://support.ecwid.com/hc/en-us/articles/207600079-Ecwid-referral-program) |

#### ambassador

| Field      | Type   | Description         |
| ---------- | ------ | ------------------- |
| ref        | string | Referral account ID |
| campaignId | string | Campaign ID         |

#### profile

See [Update store profile](../../rest-api/store-profile/update-store-profile.md) API call for reference.

### Response JSON

| Field | Type   | Description                           |
| ----- | ------ | ------------------------------------- |
| id    | number | ID of the created store               |
| token | string | A secret token for the created store. |
