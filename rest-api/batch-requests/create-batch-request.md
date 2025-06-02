# Create batch request

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/batch`&#x20;

<details>

<summary>Request and response example</summary>

Request:

```http
POST /api/v3/1003/batch?allowParallelMode=true HTTP/1.1
Authorization: Bearer secret_token
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

[
  {
    "id": "000001",
    "path": "/orders?limit=1&email=ec.apps@lightspeedhq.com",
    "method": "GET",
    "body": ""
  },
  {
    "id": "000002",
    "path": "/profile",
    "method": "GET",
    "body": ""
  },
  {
    "id": "000003",
    "path": "/products",
    "method": "POST",
    "body": {
      "sku": "0012199",
      "quantity": 10,
      "name": "New Product",
      "price": 19.99,
      "compareToPrice": 24.99,
      "isShippingRequired": false,
      "categoryIds": [
        9691094
      ],
      "weight": 10,
      "enabled": true,
      "description": "A <b>new</b> product description",
      "productClassId": 0
    }
  }
]
```

Response:

```json
{
  "ticket": "11kl140a2-966f-1a9f-b4e6-fc451bc78570"
}
```

</details>

### Required access scopes

Your app must have all **access scopes** required for requests included in the batch.

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

All query params are optional.

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>allowParallelMode</td><td>boolean</td><td>Set <code>true</code> to force requests to be done in parallel. Maximum of <strong>100</strong> requests can be processed at the same time.<br><br>If not specified, all requests in the batch will be completed consecutively.</td></tr><tr><td>stopOnFirstFailure</td><td>boolean</td><td><p>By default, batch requests stop executing on the first error response for any request included in the batch. <br><br>Set <code>false</code> to continue executing requests even when REST API responds with error codes.<br><br>Depending on the error code, batch will handle requests differently:</p><ul><li>Error codes <code>4XX</code> – batch executes the next request.</li><li>Error code <code>5XX</code> – batch tries to execute the same request 5 times with a 3-second interval before moving to the next one.</li></ul></td></tr><tr><td>deduplicationKey</td><td>string</td><td>UUID value that can be used to assign an ID to a ticket. If there's a consecutive create request with the same <code>deduplicationKey</code>, then the result for the first one will be retrieved. The result for this batch request is memorized for one hour.</td></tr><tr><td>groupId</td><td>string</td><td>Assign an internal ID to the batch request, so it can be canceled with the  "Cancel batch group" request later on.</td></tr></tbody></table>

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

### Request JSON

A JSON **array of objects** (where each object is a REST API request) with the following fields:

<table><thead><tr><th width="137">Field</th><th width="120">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string</td><td>Internal request ID that allows you to manage requests in the batch easier.<br><br><strong>Optional</strong></td></tr><tr><td>path</td><td>string</td><td>Path to Ecwid REST API endpoint.<br><br><strong>Do not include</strong> the <code>https://app.ecwid.com/api/v3/{STORE_ID}/</code> part of the request URL, as is added automatically.<br><br>For example: <code>/orders?offset=100&#x26;paymentStatus=PAID,AWAITING_PAYMENT</code><br><br><strong>Required</strong></td></tr><tr><td>method</td><td>string</td><td><p>HTTP method that must be used for the request. </p><p><br>One of: <br><code>GET</code><br><code>POST</code><br><code>PUT</code><br><code>DELETE</code><br><br><strong>Required</strong></p></td></tr><tr><td>body</td><td>string</td><td>Request body that is required for some of the <code>"PUT"</code> or <code>"POST"</code> requests, for example, "update product" or "create customer".<br><br><strong>Optional</strong></td></tr></tbody></table>

{% include "../../.gitbook/includes/rest-api-response-json.md" %}

| Field  | Type   | Description                                                                         |
| ------ | ------ | ----------------------------------------------------------------------------------- |
| ticket | string | <p>Ticket ID for your batch request. <br><br>Use it to get batch request status</p> |
