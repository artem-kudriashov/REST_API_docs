# Get batch status

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/{storeId}/batch?ticket={ticketId}`&#x20;

<details>

<summary>Request and response example</summary>

Request:

```http
GET /api/v3/1003/batch?ticket=11kl140a2-966f-1a9f-b4e6-fc451bc78570 HTTP/1.1
Authorization: Bearer secret_token
Host: app.ecwid.com
```

Response:

```json
{
    "status": "COMPLETED",
    "totalRequests": 3,
    "completedRequests": 3
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

Request works with two query params, one of which is **required**.

<table><thead><tr><th width="165">Param</th><th width="122">Type</th><th>Description</th></tr></thead><tbody><tr><td>ticketId</td><td>string</td><td>Internal ticket ID assigned to the specific batch request.<br><br><strong>Required</strong></td></tr><tr><td>escapedJson</td><td>boolean</td><td>Set  <code>true</code> to get responses for API requests included in the batch.<br><br>Responses are returned as escaped JSON string in the <code>escapedHttpBody</code> field. <br><br>By default, responses for API requests included in the batch are not returned.<br><br><strong>Optional</strong></td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="213">Field</th><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>status</td><td>string</td><td>Current status of the batch request.<br><br>One of:<br><code>QUEUED</code> – No requests inside the batch are yet completed. yet. <br><code>IN_PROGRESS</code> – At least one request inside the batch was already completed.<br><code>COMPLETED</code> – All requests inside the batch have been completed.</td></tr><tr><td>totalRequests</td><td>number</td><td>Total number of API requests included in the batch.</td></tr><tr><td>completedRequests</td><td>number</td><td>Number of completed API requests from the batch.</td></tr><tr><td>responses</td><td>object <a href="get-batch-status.md#responses">responses</a></td><td>Details of requests included in the batch.</td></tr></tbody></table>

#### responses

<table><thead><tr><th width="215">Field</th><th width="135">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>Optional ID for the REST API request included in the batch. <br><br>Only returns if it was specified in the batch request.</td></tr><tr><td>status</td><td>string</td><td>Request status.<br><br>One of:<br><code>COMPLETED</code> – All requests were completed. <br><code>FAILED</code> – Response HTTP code was not <code>200 OK</code>. <br><code>NOT_EXECUTED</code> – Request was not executed, because one of the previous requests failed and batch execution has been stoped.</td></tr><tr><td>httpBody</td><td>json object</td><td>Response body for the request, if it has any. <br><br>Returned only if <code>escapedJson</code> query param is not included or is set to <code>false</code>.<br></td></tr><tr><td>escapedHttpBody</td><td>string</td><td>Escaped JSON string of response body for the request. <br><br>Returned only with <code>escapedJson=true</code> query param.</td></tr><tr><td>httpStatusCode</td><td>number</td><td>Response HTTP code for the request. </td></tr><tr><td>httpStatusLine</td><td>string</td><td>Contains error messages for failed requests in the batch.</td></tr></tbody></table>
