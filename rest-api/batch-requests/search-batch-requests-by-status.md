# Search batch requests by status

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/{storeId}/batch?status=STATUS&limit=100`

<details>

<summary>Request and response example</summary>

Request:

```http
GET /api/v3/1003/batch?status=COMPLETED&limit=100 HTTP/1.1
Authorization: Bearer secret_token
Host: app.ecwid.com
```

Response:

```json
{
  "items": [
    {
      "ticket": "11kl140a2-966f-1a9f-b4e6-fc451bc78570",
      "status": "COMPLETED"
    }
  ]
}
```

</details>

### Required access scopes

This request does not require any **access scopes.**

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

Some of the query params are **required**.

<table><thead><tr><th width="150">Param</th><th width="133">Type</th><th>Description</th></tr></thead><tbody><tr><td>status</td><td>string</td><td><p>Search term for the current batch status. </p><p><br>One of: <br><code>QUEUED</code> – Find only batch requests that haven't been sarted yet. <br><code>IN_PROGRESS</code> – Find only batch requests in progress. <br><code>COMPLETED</code> – Find only completed batch requests.<br><br><strong>Required</strong></p></td></tr><tr><td>limit</td><td>number</td><td>Maximum number of returned items. Default and maximum allowed value: <code>100</code><br><br><strong>Required</strong></td></tr><tr><td>offset</td><td>number</td><td><p>Offset from the beginning of the returned items list. Used when the response contains more items than <code>limit</code> allows to receive in one request.<br><br>Usually used to receive all items in several requests with multiple of a hundred, for example:<br></p><p><code>?offset=0</code> for the first request,</p><p><code>?offset=100</code>, for the second request,</p><p><code>?offset=200</code>, for the third request, etc.<br><br><strong>Optional</strong></p></td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="127">Field</th><th width="140.0390625">Type</th><th>Description</th></tr></thead><tbody><tr><td>items</td><td>array of objects <a data-mention href="search-batch-requests-by-status.md#items">#items</a> </td><td>List of found batch requests.</td></tr></tbody></table>

#### items

<table><thead><tr><th width="127">Field</th><th width="140.05078125">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticket</td><td>string</td><td>Internal "ticket ID" assigned to the batch request.</td></tr><tr><td>status</td><td>string</td><td>Current status of the batch request.<br><br>One of:<br><code>QUEUED</code> – No requests inside the batch are yet completed. yet. <br><code>IN_PROGRESS</code> – At least one request inside the batch was already completed.<br><code>COMPLETED</code> – All requests inside the batch have been completed.</td></tr></tbody></table>
