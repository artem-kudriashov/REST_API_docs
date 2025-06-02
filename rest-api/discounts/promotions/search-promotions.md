# Search promotions

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/{storeId}/promotions`&#x20;

<details>

<summary>Request and response example</summary>

Request:

```http
GET /api/v3/1003/promotions HTTP/1.1
Authorization: Bearer secret_token
Host: app.ecwid.com
```

Response:

```json
{
  "total": 1,
  "count": 1,
  "offset": 0,
  "limit": 100,
  "items": [
    {
      "id": 608502,
      "name": "10% off on cart total above €50,00",
      "enabled": true,
      "discountBase": "SUBTOTAL",
      "discountType": "PERCENT",
      "amount": 10,
      "triggers": {
        "subtotal": 50
      }
    }
  ]
}
```

</details>

### Required access scopes

Your app must have the following **access scopes** to make this request: `read_promotion`

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

All query params are optional.

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>responseFields</td><td>string</td><td>Specify the exact fields to receive in response JSON. If not specified, the response JSON will have all available fields for the entity.<br>Example: <code>?responseFields=items(name,enabled)</code></td></tr></tbody></table>

Example of using `responseFields` param:

{% tabs %}
{% tab title="Request" %}
```
curl --location 'https://app.ecwid.com/api/v3/1003/promotions?responseFields=items(name,enabled)' \
--header 'Authorization: Bearer secret_ab***cd'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "items": [
        {
            "name": "10% off on cart total above €50,00",
            "enabled": true
        }
    ]
}
```
{% endtab %}
{% endtabs %}

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="198">Field</th><th width="228">Type</th><th>Description</th></tr></thead><tbody><tr><td>total</td><td>number</td><td>Total number of found items (might be more than the number of returned items).</td></tr><tr><td>count</td><td>number</td><td>Total number of items returned in the response.</td></tr><tr><td>offset</td><td>number</td><td>Offset from the beginning of the returned items list specified in the request.</td></tr><tr><td>limit</td><td>number</td><td>Maximum number of returned items specified in the request. Maximum and default value: <code>100</code>.</td></tr><tr><td>items</td><td>array of objects <a href="search-promotions.md#items">items</a></td><td>Detailed information about returned promotions.</td></tr></tbody></table>

#### items

<table><thead><tr><th width="191">Field</th><th width="184">Type</th><th>Description</th></tr></thead><tbody><tr><td>name</td><td>string</td><td><p>Name of the discount visible at the checkout.<br></p><p>Max length: 1024 symbols.</p></td></tr><tr><td>discountBase</td><td>string</td><td><p>Base for calculating the discount at the checkout.<br></p><p>One of:<br><code>ITEM</code> – Discount is only applied to products matching conditions from <code>targets</code> array.<br><code>SUBTOTAL</code> – Discount is applied to the cart subtotal cost, ignoring product limitations from <code>targets</code> array.<br><code>SHIPPING</code> – Discount is only applied to shipping costs matching conditions from <code>targets</code> array.</p></td></tr><tr><td>enabled</td><td>boolean</td><td>Defines if the promotion is enabled (<code>true</code>) or disabled (<code>false</code>).<br><br>DIsabled promotions can't be used at the checkout.</td></tr><tr><td>discountType</td><td>string</td><td><p>Describes if the discount is calculated as a percent or an absolute value. </p><p><br>One of: </p><p><code>PERCENT</code> - Price modifier applies as a percent from the product price.</p><p><code>ABSOLUTE</code> - Price modifier applies as a flat value.</p></td></tr><tr><td>amount</td><td>number</td><td>Discount amount. <br><br>Value is applied as an absolute sum or a percent depending on the <code>"discountType"</code> field.</td></tr><tr><td>triggers</td><td>object <a href="search-promotions.md#triggers">triggers</a></td><td>Trigger conditions for the promotion to apply at the checkout.<br><br>Promotion is automatically applied when all specified conditions are met.</td></tr><tr><td>targets</td><td>object <a href="search-promotions.md#targets">targets</a></td><td>Target limitations: limit promotion's application by specific categories, products, combinations, and more.<br><br>Promotion is automatically applied to products in the cart if they match all specified target limitations.</td></tr><tr><td>externalReferenceId</td><td>string</td><td>Internal field for storing promotion ID from Lightspeed X-Series.</td></tr></tbody></table>

#### triggers

<table><thead><tr><th width="250">Field</th><th width="183">Type</th><th>Description</th></tr></thead><tbody><tr><td>startDate</td><td>string</td><td>Datetime when the promotion becomes available at the checkout.<br><br>For example, <code>2025-03-06 00:00:00 +0000</code></td></tr><tr><td>endDate</td><td>string</td><td>Datetime when the promotion stops being available at the checkout.<br><br>For example, <code>2025-03-30 12:00:00 +0000</code></td></tr><tr><td>customerGroups</td><td>array of numbers</td><td><p>Customer group IDs for the promotion, e.g. <code>[0, 12345, 23456]</code>.<br></p><p>Maximum number of IDs: 200.</p></td></tr><tr><td>subtotal</td><td>number</td><td>Minimum cart subtotal (cost of products) for the promotion to be applied.</td></tr><tr><td>minProductQuantityInCart</td><td>number</td><td>Minimum quantity of products in the cart for the promotion to apply at the checkout.</td></tr><tr><td>maxProductQuantityInCart</td><td>number</td><td>Maximum quantity of products in the cart for the promotion to apply at the checkout.</td></tr><tr><td>categories</td><td>array of numbers</td><td>List of category IDs for promotion trigger.<br><br>All products in the cart must be from specified category IDs to trigger the promotion.</td></tr><tr><td>excludedCategories</td><td>array of numbers</td><td>Exclude specific category IDs from promotion triggers.<br><br>If any products added to the cart belong to the specified category IDs, the promotion will not apply to the cart.</td></tr><tr><td>products</td><td>array of numbers</td><td>List of product IDs for promotion trigger.<br><br>All products in the cart must be from this list to trigger the promotion.</td></tr><tr><td>excludedProducts</td><td>array of numbers</td><td>Exclude specific product IDs from promotion triggers.<br><br>If any products added to the cart match the specified IDs, the promotion will not apply to the cart.</td></tr><tr><td>combinations</td><td>array of numbers</td><td>List of product variation IDs for promotion trigger.<br><br>All product variations added to the cart must be from this list to trigger the promotion.</td></tr><tr><td>excludedCombinations</td><td>array of numbers</td><td>Exclude specific product variation IDs from promotion triggers.<br><br>If any of the specified product variation IDs is added to the cart, the promotion will not apply to it.</td></tr><tr><td>recurring</td><td>boolean</td><td>Defines if the promotion has recurrence settings. Recurrent promotions automatically become active on specified days.<br><br>If <code>true</code>, requires <code>recurrenceSettings</code> > <code>activeDays</code> array to list at least one day of the week inside.</td></tr><tr><td>recurrenceSettings</td><td>object <a href="search-promotions.md#recurrencesettings">recurrenceSettings</a></td><td>Recurrence settings for the promotion. Requires <code>"recurring": true</code> to work.</td></tr></tbody></table>

#### targets

<table><thead><tr><th width="287">Field</th><th width="170">Type</th><th>Description</th></tr></thead><tbody><tr><td>categories</td><td>array of numbers</td><td>List of category IDs. <br><br>If specified, promotion only applies to products from specified category IDs. </td></tr><tr><td>excludedCategories</td><td>array of numbers</td><td>Exclude specific category IDs from promotion targets.<br><br>Promotion will not apply to products from specified categories.</td></tr><tr><td>products</td><td>array of numbers</td><td>List of product IDs. <br><br>If specified, promotion only applies to specified product IDs. </td></tr><tr><td>excludedProducts</td><td>array of numbers</td><td>Exclude specific product IDs from promotion targets.<br><br>Promotion will not apply to products from the list.</td></tr><tr><td>combinations</td><td>array of objects <a href="search-promotions.md#combinations">combinations</a></td><td>List of product variations promotion works with. If specified, promotion won't work with any product variations that are not specified here. </td></tr><tr><td>excludedCombinations</td><td>array of objects <a href="search-promotions.md#combinations">combinations</a></td><td>Exclude specific product variation IDs from promotion targets.<br><br>Promotion will not apply to product variations from the list.</td></tr><tr><td>attributes</td><td>array of objects <a href="search-promotions.md#attributes">attributes</a></td><td>List of product attribute values. If specified, promotion won't work with any products that don't have product attributes and values specified here. </td></tr><tr><td>minDiscountedProductQuantity</td><td>number</td><td>Minimum quantity of products in the cart that can be discounted by the promotion.</td></tr><tr><td>maxDiscountedProductQuantity</td><td>number</td><td>Maximum quantity of products in the cart that can be discounted by the promotion.</td></tr><tr><td>shippingMethods</td><td>array of strings</td><td><p>List of shipping method IDs promotion works with. If specified, promotion won't work with any shipping method that is not specified here. For example. <code>["6589-1709547151586"]</code>.</p><p><br>Requires <code>"discountBase": "SHIPPING"</code>.<br></p><p>Maximum number of IDs: 100.</p></td></tr><tr><td>all</td><td>boolean</td><td>Internal value (read-only).</td></tr></tbody></table>

#### attributes

| Field           | Type             | Description                                                                                                                                                                               |
| --------------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| attributeId     | number           | Internal attribute ID.                                                                                                                                                                    |
| attributeValues | array of strings | <p>List of matching attribute values in products, for which the promotion should apply.<br><br>Total maximum number of attribute values <strong>across all attributes</strong> is 30.</p> |

#### combinations

| Field          | Type             | Description                                                                                                                                                          |
| -------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| productId      | number           | Internal attribute ID.                                                                                                                                               |
| combinationIds | array of strings | <p>List of matching product variations IDs (in string format).<br><br>Total maximum number of product variation IDs <strong>across all products</strong> is 100.</p> |

#### recurrenceSettings

<table><thead><tr><th width="179.671875">Field</th><th width="140.1171875">Type</th><th>Description</th></tr></thead><tbody><tr><td>activeDays</td><td>array of strings</td><td>List of days when the promotion becomes active automatically. If specified and the <code>"recurring"</code> is <code>true</code> , then the promotion is only available on listed days of the week.<br><br>Format of days: <code>"MON"</code>, <code>"TUE"</code>, <code>"WED"</code>, <code>"THU"</code>, <code>"FRI"</code>, <code>"SAT"</code>, <code>"SUN"</code>. <br><br>For example, the "weekend sale" promotion will have <code>"activeDays": ["SAT", "SUN"]</code>.</td></tr><tr><td>activeDayStartTime</td><td>string</td><td>Time when the promotion activates on the listed days. If not specified, the promotion starts at 00:00.<br><br>Format: 24h, <code>hh:mm:ss</code>. <br>For example, <code>"activeDayStartTime": "09:30:00"</code>.</td></tr><tr><td>activeDayEndTime</td><td>string</td><td>Time when the promotion deactivates on the listed days. If not specified, the promotion ends at 24:00.<br><br>Format: 24h, <code>hh:mm:ss</code>. <br>For example, <code>"activeDaEndTime": "22:00:00"</code>.</td></tr></tbody></table>
