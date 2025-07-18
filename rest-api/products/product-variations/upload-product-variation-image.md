# Upload product variation image

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/products/{productId}/combinations/{combinationId}/image`&#x20;

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

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>externalUrl</td><td>boolean</td><td>HTTPS link to the image file that will be uploaded to the store.<br><br>Alternatively, you can send the image as binary data in the request body.</td></tr></tbody></table>

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

| Field | Type   | Description                        |
| ----- | ------ | ---------------------------------- |
| id    | number | Internal ID of the uploaded image. |
