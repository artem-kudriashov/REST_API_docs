# Adjust product variation stock

<mark style="color:purple;">`PUT`</mark> `https://app.ecwid.com/api/v3/{storeId}/products/{productId}/combinations/{combinationId}/inventory`&#x20;

<details>

<summary>Request and response example</summary>

Request:

```http
PUT /api/v3/1003/products/692730761/combinations/422488528/inventory HTTP/1.1
Authorization: Bearer secret_token
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

{
    "quantityDelta": -10
}
```

Response:

{% code fullWidth="true" %}
```json
{
    "updateCount": 1
}
```
{% endcode %}

</details>

### Required access scopes

Your app must have the following **access scopes** to make this request: `read_catalog`, `update_catalog`

### Path params

All path params are required.

| Param         | Type   | Description                    |
| ------------- | ------ | ------------------------------ |
| storeId       | number | Ecwid store ID.                |
| productId     | number | Internal product ID.           |
| combinationId | number | Internal product variation ID. |

### Query params

All query params are optional.

<table><thead><tr><th width="260">Field</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td>checkLowStockNotification</td><td>boolean</td><td>Defines if Ecwid should check the quantity of product stock and send the low stock email notification to the store owner.</td></tr></tbody></table>

{% include "../../../.gitbook/includes/rest-api-headers.md" %}

### Request JSON

A JSON object with the following fields:

| Field         | Type   | Description                                                                                                                                                                                                                             |
| ------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| quantityDelta | number | <p>The quantity value for updating product quantity. Positive value increases product stock, a negative one decreases it.<br><br>For example, <code>5</code> adds 5 to the product stock, and <code>-10</code> decreases it for 10.</p> |

### Response JSON

A JSON object with the following fields:

| Field       | Type   | Description                                                                                                                                                                                   |
| ----------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| updateCount | number | <p>The number of updated items that defines if the request was successful.<br><br>One of:</p><p><code>1</code> if the item was updated,</p><p><code>0</code> if the item was not updated.</p> |
| warning     | string | Inventory update warning  displayed if the product variation stock became negative after the request.                                                                                         |
