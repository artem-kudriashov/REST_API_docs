# Stop batch request

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/batch/cancel-group?ticketId={ticketId}&groupId={groupId}`

{% hint style="info" %}
Stops all remaining non-executed requests inside the batch. These requests receive `COMPLETED` status and therefore are not executed later on.\
\
Already completed requests inside the batch are not affected.
{% endhint %}

### Required access scopes

This request does not require any **access scopes.**

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

Some of the query params are **required**.

<table><thead><tr><th width="150">Param</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticketId</td><td>string</td><td>Internal "ticket ID" assigned to the batch.<br><br><strong>Required</strong></td></tr><tr><td>groupId</td><td>number</td><td>Internal group ID assigned to the batch. <br><br><strong>Required</strong></td></tr><tr><td>escapedJson</td><td>number</td><td>Set  <code>true</code> to get responses for already completed requests included in the batch.<br><br>Responses are returned as escaped JSON string in the <code>escapedHttpBody</code> field. <br><br>By default, responses for API requests included in the batch are not returned.<br><br><strong>Optional</strong></td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

| Field       | Type   | Description                                                                                                                                             |
| ----------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateCount | number | <p>Defines if the request was successful.<br><br>One of:<br><code>1</code> if the batch was stopped,<br><code>0</code> if the item was not updated.</p> |
