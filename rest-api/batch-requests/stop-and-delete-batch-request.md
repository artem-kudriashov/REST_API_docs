# Stop and delete batch request

<mark style="color:red;">`DELETE`</mark> `https://app.ecwid.com/api/v3/{storeId}/batch?ticketId={ticketId}`

{% hint style="info" %}
Stops all remaining non-executed requests inside the batch and completely deletes it from history.
{% endhint %}

### Required access scopes

This request does not require any **access scopes.**

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

Request works with one **required** query param.

<table><thead><tr><th width="150">Param</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticketId</td><td>string</td><td>Internal "ticket ID" assigned to the batch.<br><br><strong>Required</strong></td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

| Field       | Type   | Description                                                                                                                                                                             |
| ----------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| deleteCount | number | <p>The number of deleted items that defines if the request was successful.<br><br>One of:<br><code>1</code> if the item was deleted,<br><code>0</code> if the item was not deleted.</p> |
