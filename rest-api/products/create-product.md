# Create product

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/products`&#x20;

<details>

<summary>Request and response example</summary>

Request:

```http
POST /api/v3/1003/products HTTP/1.1
Authorization: Bearer secret_token
Host: app.ecwid.com
Content-Type: application/json
Cache-Control: no-cache

{
  "sku": "000012199",
  "quantity": 10,
  "name": "New Product",
  "price": 10,
  "compareToPrice": 15,
  "costPrice": 8,
  "isShippingRequired": false,
  "categoryIds": [
    9691094
  ],
  "weight": 10,
  "enabled": true,
  "description": "A <b>new</b> product description",
  "productClassId": 0,
  "volume": 500,
  "volumeUnit": "ml",
  "fixedShippingRateOnly": false,
  "fixedShippingRate": 1.2,
  "tax": {
    "enabledManualTaxes": [
      1117939042
    ],
    "taxable": true
  },  
  "options": [
    {
      "type": "RADIO",
      "name": "Size",
      "choices": [
        {
          "text": "Small",
          "priceModifier": 0,
          "priceModifierType": "ABSOLUTE"
        },
        {
          "text": "Large",
          "priceModifier": 15,
          "priceModifierType": "ABSOLUTE"
        }
      ],
        "defaultChoice": 0,
        "required": true
    }
  ],
  "shipping": {
    "type": "SELECTED_METHODS",
    "methodMarkup": 0,
    "flatRate": 0,
    "disabledMethods": [
      "1396442138-1534946367952"
    ],
    "enabledMethods": []
  }
}
```

Response:

```json
{
  "id": 39766764
}
```

</details>

### Required access scopes

Your app must have the following **access scopes** to make this request: `create_catalog`

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

### Request JSON

A JSON object with the following fields:

| Field                         | Type                                                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ----------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| sku                           | string                                                                | Product SKU. Items with options can have several SKUs specified in the product variations.                                                                                                                                                                                                                                                                                                                                                                                                                            |
| quantity                      | number                                                                | <p>Amount of product items in stock (available for purchase). </p><p></p><p>If the product has unlimited stock (<code>unlimited</code> is <code>true</code>), this field is not returned.</p>                                                                                                                                                                                                                                                                                                                         |
| unlimited                     | boolean                                                               | Defines if the product has unlimited stock.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| inStock                       | boolean                                                               | Defines if the product or any of its variations are in stock (`quantity` is more than `0`).                                                                                                                                                                                                                                                                                                                                                                                                                           |
| name                          | string                                                                | Product name visible on the storefront.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| nameTranslated                | string                                                                | Available translations for the product name.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| price                         | number                                                                | Base product price without any modifiers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| tax                           | object [tax](create-product.md#tax)                                   | Detailed information about product's taxes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| wholesalePrices               | array of objects [wholesalePrices](create-product.md#wholesaleprices) | Sorted list of wholesale price tiers: "minimum quantity = price" pairs.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| compareToPrice                | number                                                                | Product pre-sale price with the same value as specified in Ecwid admin (without taxes), e.g. `40`.                                                                                                                                                                                                                                                                                                                                                                                                                    |
| lowestPriceSettings           | object [lowestPriceSettings](create-product.md#lowestpricesettings)   | <p>Product lowest price settings for EU stores.<br><br>Read more on lowes price settings in <a href="https://support.ecwid.com/hc/en-us/articles/9382914337820-Lowest-product-price-before-discounting">Help Center</a>.</p>                                                                                                                                                                                                                                                                                          |
| isShippingRequired            | boolean                                                               | Defines if the product requires shipping.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| weight                        | number                                                                | <p>Product weight in the units defined in store settings.<br><br>If the product doesn't have weight, this field is not returned.</p>                                                                                                                                                                                                                                                                                                                                                                                  |
| customSlug                    | string                                                                | Custom slug defined by the store owner. Affects product page URL.                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| productClassId                | number                                                                | <p>ID of the product class that affects attributes management. <br><br>If it's <code>0</code> the product belongs to the default "General" class. <br><br>Read more on product types and attributes in <a href="https://support.ecwid.com/hc/en-us/articles/207807495-Product-types-and-attributes">Help Center</a>.</p>                                                                                                                                                                                              |
| enabled                       | boolean                                                               | <p>Defines if the product is enabled and visible on the storefront.<br><br>If <code>false</code>, the product can't be opened on the storefront or added to the cart.</p>                                                                                                                                                                                                                                                                                                                                             |
| options                       | array [options](create-product.md#options)                            | <p>Detailed list of product options. <br><br>Empty (<code>[]</code>) if no options are specified for the product.</p>                                                                                                                                                                                                                                                                                                                                                                                                 |
| warningLimit                  | number                                                                | Minimum amount of products in stock to trigger an automated "low stock" email notification for the store owner.                                                                                                                                                                                                                                                                                                                                                                                                       |
| fixedShippingRateOnly         | boolean                                                               | <p><strong>Legacy feature</strong> – see <code>shipping</code> field instead.<br><br><code>true</code> if shipping cost for this product is calculated as <em>'Fixed rate per item'</em> (managed under the "Tax and Shipping" section of the product management page in Ecwid Control panel). <code>false</code> otherwise. <br><br>With this option on, the <code>fixedShippingRate</code> field specifies the shipping cost of the product.</p>                                                                    |
| fixedShippingRate             | number                                                                | <p><strong>Legacy feature</strong> – see <code>shipping</code> field instead. <br><br>When <code>fixedShippingRateOnly</code> is <code>true</code>, this field sets the product fixed shipping cost per item. <br><br>When <code>fixedShippingRateOnly</code> is <code>false</code>, the value in this field is treated as an extra shipping cost the product adds to the global calculated shipping</p>                                                                                                              |
| shipping                      | object [shipping](create-product.md#shipping)                         | Shipping settings specific to the product.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| description                   | string                                                                | <p>Product description in HTML format.<br><br>Scripts inside product descriptions are not supported.</p>                                                                                                                                                                                                                                                                                                                                                                                                              |
| descriptionTranslated         | object [translations](create-product.md#translations)                 | Available translations for the product description.                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| categoryIds                   | array of numbers                                                      | List of the category IDs the product belongs to.                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| defaultCategoryId             | number                                                                | Default category ID of the product. If value is `0`, then product does not have a default category and is not shown anywhere in storefront                                                                                                                                                                                                                                                                                                                                                                            |
| seoTitle                      | string                                                                | <p>Page title for search engines.<br><br>Recommended length &#x3C; 55 characters.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| seoTitleTranslated            | object [translations](create-product.md#translations)                 | Translations for the SEO page title.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| seoDescription                | string                                                                | <p>Page description for search engines. <br><br>Recommended length &#x3C; 160 characters.</p>                                                                                                                                                                                                                                                                                                                                                                                                                         |
| seoDescriptionTranslated      | object [translations](create-product.md#translations)                 | Translations for the SEO page description.                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| attributes                    | array of objects [attributes](create-product.md#attributes)           | List of product attributes and their values.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| files                         | array of objects [files](create-product.md#files)                     | Details about downloadable files attached to the product.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| relatedProducts               | object [relatedProducts](create-product.md#relatedproducts)           | List of related products displayed as "You may also like" products of the product.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| dimensions                    | object [dimensions](create-product.md#dimensions)                     | Product's dimensions.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| volume                        | number                                                                | Product volume for calculations shipping costs, fractional number, `0` by default.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| showOnFrontpage               | number                                                                | Product index on the main storefront page starting with `1`.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| isGiftCard                    | boolean                                                               | Defines if a product is a gift card.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| subtitle                      | string                                                                | Small product description visible on category and product pages under the product title.                                                                                                                                                                                                                                                                                                                                                                                                                              |
| subtitleTranslated            | object [translations](create-product.md#translations)                 | Available translations for product subtitles.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| discountsAllowed              | boolean                                                               | Defines if Ecwid can apply discounts to the product.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| externalReferenceId           | string                                                                | External ID for products synced from external services, for example, POS.                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| outOfStockVisibilityBehaviour | boolean                                                               | <p>Defines if a product is visible and/or can be pre-ordered when out-of-stock. <br><br>Requires enabled pre-orders on the store level: <code>allowPreordersForOutOfStockProducts</code> setting in <code>/profile</code> endpoint.<br><br>Supported values:<br><code>SHOW</code> - Show out-of-stock products, but adding them to the cart is impossible.<br><code>HIDE</code> - Hide out-of-stock products.<br><code>ALLOW_PREORDER</code> - Show out-of-stock products and allow them to be added to the cart.</p> |
| minPurchaseQuantity           | number                                                                | <p>Sets minimum product purchase quantity.<br><br> Default value is <code>null</code>.</p>                                                                                                                                                                                                                                                                                                                                                                                                                            |
| maxPurchaseQuantity           | number                                                                | <p>Sets maximum product purchase quantity. <br><br>Default value is <code>null</code>.</p>                                                                                                                                                                                                                                                                                                                                                                                                                            |
| reviewsCollectingAllowed      | boolean                                                               | When `true`, allows to collect, check, and publish reviews for this product in store.                                                                                                                                                                                                                                                                                                                                                                                                                                 |

#### wholesalePrices

<table><thead><tr><th>Field</th><th width="128">Type</th><th>Description</th></tr></thead><tbody><tr><td>quantity</td><td>number</td><td>Number of product items on this wholesale tier.</td></tr><tr><td>price</td><td>number</td><td>Product price on the tier.</td></tr></tbody></table>

#### lowestPriceSettings

<table><thead><tr><th>Field</th><th width="142">Type</th><th>Description</th></tr></thead><tbody><tr><td>lowestPriceEnabled</td><td>boolean</td><td>Defines if the lowest price is enabled for the product and shown on the storefront.</td></tr><tr><td>manualLowestPrice</td><td>number</td><td>Manually entered lowest price for the last 30 days before any discounts or taxes applied.</td></tr></tbody></table>

#### options

{% include "../../.gitbook/includes/rest-api-product-greater-than-options.md" %}

#### choices

{% include "../../.gitbook/includes/rest-api-product-greater-than-choices.md" %}

#### shipping

<table><thead><tr><th>Field</th><th width="160">Type</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>string</td><td>One of: <code>"GLOBAL_METHODS"</code>, <code>"SELECTED_METHODS"</code>, <code>"FLAT_RATE"</code>, <code>"FREE_SHIPPING"</code>. <code>"GLOBAL_METHODS"</code> – all standard shipping methods set up in store settings; <code>"SELECTED_METHODS"</code> – <br><br>Ecwid will use <code>enabledMethods</code> and <code>disabledMethods</code> list to make shipping calculations; <code>"FLAT_RATE"</code> – sets flat rate for product's shipping, see <code>flatRate</code> field.</td></tr><tr><td>methodMarkup</td><td>number</td><td>Additional product shipping cost added to any shipping methods.</td></tr><tr><td>flatRate</td><td>number</td><td>Flat rate cost for shipping the product. If set, shipping costs for it will not be calculated.</td></tr><tr><td>disabledMethods</td><td>array of strings</td><td>IDs of shipping methods that need to be excluded from calculation when this product is in cart. <br><br>Full list of shipping method IDs is available thorugh the <a href="ref:store-profile">Store profile</a> call.</td></tr><tr><td>enabledMethods</td><td>array of strings</td><td>IDs of shipping methods which will only be shown when this product is in cart. No other shipping methods will be shown.<br><br>Full list of shipping method IDs is available thorugh the <a href="ref:store-profile">Store profile</a> call.</td></tr></tbody></table>

#### categories

| Field   | Type    | Description                         |
| ------- | ------- | ----------------------------------- |
| id      | number  | Internal category ID.               |
| enabled | boolean | Defines if the category is enabled. |

#### attributes

<table><thead><tr><th>Field</th><th width="185">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>number</td><td>Internal attribute ID. </td></tr><tr><td>name</td><td>string</td><td>Attribute name visible on the storefront.</td></tr><tr><td>nameTranslated</td><td>object <a href="create-product.md#translations">translations</a></td><td>Available translations for the attribute name.</td></tr><tr><td>value</td><td>string</td><td>Value of the attribute for this product.</td></tr><tr><td>valueTranslated</td><td>object <a href="create-product.md#translations">translations</a></td><td>Available translations for the attribute value.</td></tr><tr><td>type</td><td>string</td><td>Attribute type. There are user-defined attributes, general attributes and attributes pre-defined by Ecwid, for example, "price per unit". <br><br>One of:<br><code>CUSTOM</code><br><code>UPC</code><br><code>BRAND</code><br><code>GENDER</code><br><code>AGE_GROUP</code><br><code>COLOR</code><br><code>SIZE</code><br><code>PRICE_PER_UNIT</code><br><code>UNITS_IN_PRODUCT</code></td></tr><tr><td>show</td><td>string</td><td>Defines if an attribute is visible on a product page. <br><br>One of:<br><code>NOTSHOW</code> - Not visible.<br><code>DESCR</code> - Visible under the product description.<br><code>PRICE</code> - Visible under the product price</td></tr></tbody></table>

#### files

| Field       | Type   | Description                                                                                                                                                                                                                                                                                                           |
| ----------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id          | number | Internal ID of the file attached to the product.                                                                                                                                                                                                                                                                      |
| name        | string | File name visible to clients.                                                                                                                                                                                                                                                                                         |
| description | string | File description visible to clients.                                                                                                                                                                                                                                                                                  |
| size        | number | File size in bytes (64-bit integer).                                                                                                                                                                                                                                                                                  |
| adminUrl    | string | <p>Direct link to the file.<br><br><strong>Important</strong>: to download the file, add your API access token to this URL like this: <code>https://app.ecwid.com/api/v3/4870020/products/37208340/files/7215102?token=YOUR-API-TOKEN</code><br><br><strong>Do not share links containing access tokens.</strong></p> |

#### relatedProducts

| Field           | Type                                                        | Description                                                       |
| --------------- | ----------------------------------------------------------- | ----------------------------------------------------------------- |
| productIds      | array of numbers                                            | List of related product IDs.                                      |
| relatedCategory | object [relatedCategory](create-product.md#relatedcategory) | Describes the "N random related products from a category" option. |

#### relatedCategory

| Field        | Type    | Description                                                                                                  |
| ------------ | ------- | ------------------------------------------------------------------------------------------------------------ |
| enabled      | boolean | Defines if the "N random related products from a category" option is enabled.                                |
| categoryId   | number  | <p>ID of the related category. <br><br>Empty value means that related products can be from any category.</p> |
| productCount | number  | Number of random products from the given category.                                                           |

#### dimensions

| Field  | Type   | Description                                         |
| ------ | ------ | --------------------------------------------------- |
| length | number | Length of a product for calculating shipping costs. |
| width  | number | Width of a product for calculating shipping costs.  |
| height | number | Height of a product for calculating shipping costs. |

#### tax

| Field              | Type             | Description                                                                                                                |
| ------------------ | ---------------- | -------------------------------------------------------------------------------------------------------------------------- |
| taxable            | boolean          | Defines if taxes can be applied to the product.                                                                            |
| enabledManualTaxes | array of numbers | <p>List of internal IDs for manual taxes. <br><br>Empty if no manual taxes are enabled or automatic taxes are enabled.</p> |
| taxClassCode       | string           | Tax class code for the product that determines the taxability of the products for a certain region.                        |

#### translations

Object with text field translations in the `"lang": "text"` format, where the `"lang"` is an ISO 639-1 language code. For example:

```
{
    "en": "Sample text",
    "nl": "Voorbeeldtekst"
}
```

Translations are available for all active store languages. Only the default language translations are returned if no other translations are provided for the field. Find active store languages with <mark style="color:green;">`GET`</mark> `/profile` request > `languages` > `enabledLanguages`.

### Response JSON

A JSON object with the following fields:

| Field | Type   | Description                         |
| ----- | ------ | ----------------------------------- |
| id    | number | Internal ID of the created product. |
