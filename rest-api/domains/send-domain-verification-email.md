# Send domain verification email

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/domains/send_domain_verification_email?domain_name={domain_name}`&#x20;

### Required access scopes

Your app must have the following **access scopes** to make this request: `buy_domains`

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

Request works with one **required** query param.

<table><thead><tr><th width="179">Param</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>domain_name</td><td>string</td><td>Domain name. Value matches <code>domainName</code> field with <code>/domains/purchase</code> and <code>purchasedDomains["name"]</code> field in <code>/profile/domains</code>.<br><br><strong>Required</strong></td></tr></tbody></table>

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

