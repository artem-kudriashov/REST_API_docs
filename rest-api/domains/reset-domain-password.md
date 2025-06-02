# Reset domain password

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/domains/reset_domain_password?domain_name={domain_name}`&#x20;

### Required access scopes

Your app must have the following **access scopes** to make this request: `buy_domains`

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

Some query params are required.

<table><thead><tr><th width="179">Param</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>domain_name</td><td>string</td><td>Domain name. Value matches <code>domainName</code> field with <code>/domains/purchase</code> and <code>purchasedDomains["name"]</code> field in <code>/profile/domains</code>.<br><br><strong>Required</strong></td></tr><tr><td>send_to</td><td>string</td><td><p>Indicates the contact to which the password is to be reset. </p><p><br>One of: <code>owner</code>,<code>admin</code>.</p></td></tr><tr><td>sub_user</td><td>string</td><td><code>1</code> if password should be sent to the sub-user of the domain, <code>0</code> otherwise.</td></tr></tbody></table>

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>
