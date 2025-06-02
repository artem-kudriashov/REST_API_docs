# Get product type

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/{storeId}/classes/{classId}`&#x20;

<details>

<summary>Request and response example</summary>

Request:

```http
GET /api/v3/1003/classes/0 HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer secret_token
```

Response:

{% code fullWidth="true" %}
```json
[
  {
    "id": 0,
    "attributes": [
      {
        "id": 139165261,
        "name": "Units in product",
        "type": "UNITS_IN_PRODUCT",
        "show": "DESCR"
      },
      {
        "id": 82991001,
        "name": "Price per unit",
        "type": "PRICE_PER_UNIT",
        "show": "PRICE"
      },
      {
        "id": 201437969,
        "name": "UPC",
        "type": "UPC",
        "show": "DESCR"
      },
      {
        "id": 201437970,
        "name": "Brand",
        "type": "BRAND",
        "show": "DESCR"
      }
    ]
  }
]
```
{% endcode %}

</details>

### Required access scopes

Your app must have the following **access scopes** to make this request: `read_catalog`

### Path params

All path params are required.

| Param   | Type   | Description               |
| ------- | ------ | ------------------------- |
| storeId | number | Ecwid store ID.           |
| classId | number | Internal product type ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="179">Field</th><th width="229">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>number</td><td>Internal unique ID of the product type. <br><br>By default, all products get the "General" type which ID is <code>0</code>.</td></tr><tr><td>name</td><td>string</td><td>Product type name. Empty for the "General" type.</td></tr><tr><td>googleTaxonomy</td><td>string</td><td>Google taxonomy associated with the type.</td></tr><tr><td>attributes</td><td>array of objects <a href="get-product-type.md#attributes">attributes</a></td><td>Product attributes assigned to this product type.</td></tr></tbody></table>

#### attributes

<table><thead><tr><th width="181">Field</th><th width="183">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>number</td><td>Internal unique ID of the product attribute.</td></tr><tr><td>name</td><td>string</td><td>Attribute title visible. Product attribute with an empty name field will also be returned</td></tr><tr><td>nameTranslated</td><td>object <a href="get-product-type.md#translations">translations</a></td><td>Available translations for product attribute name</td></tr><tr><td>type</td><td>string</td><td>Attribute type. There are user-defined attributes, general attributes and special 'price per unit' attributes. The 'type' field contains one of the following: <code>CUSTOM</code>, <code>UPC</code>, <code>BRAND</code>, <code>GENDER</code>, <code>AGE_GROUP</code>, <code>COLOR</code>, <code>SIZE</code>, <code>PRICE_PER_UNIT</code>, <code>UNITS_IN_PRODUCT</code>. Attributes of type <code>PRICE_PER_UNIT</code> and <code>UNITS_IN_PRODUCT</code> are only returned if price per unit feature is enabled.</td></tr><tr><td>show</td><td>string</td><td>Defines if an attribute is visible on a product page. Supported values: <code>NOTSHOW</code>, <code>DESCR</code>, <code>PRICE</code>. The value <code>PRICE</code> = <code>DESCR</code>. For <a href="ref:authentication-basics#access-tokens">public tokens</a>, <code>NOTSHOW</code> attributes are not returned</td></tr></tbody></table>

#### translations

Object with text field translations in the `"lang": "text"` format, where the `"lang"` is an ISO 639-1 language code. For example:

```
{
    "en": "Sample text",
    "nl": "Voorbeeldtekst"
}
```

Translations are available for all active store languages. Only the default language translations are returned if no other translations are provided for the field. Find active store languages with <mark style="color:green;">`GET`</mark> `/profile` request > `languages` > `enabledLanguages`.
