# Delete staff account

<mark style="color:red;">`DELETE`</mark> `https://app.ecwid.com/api/v3/{storeId}/staff/{staffAccountId}`&#x20;

### Required access scopes

Your app must have the following **access scopes** to make this request: `delete_staff`&#x20;

### Path params

All path params are required.

| Param          | Type   | Description                |
| -------------- | ------ | -------------------------- |
| storeId        | number | Ecwid store ID.            |
| staffAccountId | string | Internal staff account ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

{% include "../../.gitbook/includes/rest-api-response-json.md" %}

| Field       | Type   | Description                                                                                                                                                                             |
| ----------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| deleteCount | number | <p>The number of deleted items that defines if the request was successful.<br><br>One of:<br><code>1</code> if the item was deleted,<br><code>0</code> if the item was not deleted.</p> |
