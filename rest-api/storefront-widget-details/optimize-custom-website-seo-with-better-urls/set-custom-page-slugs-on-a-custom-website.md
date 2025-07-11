# Set Custom Page Slugs on a custom website

**Custom Page Slugs** feature allows you to set custom URLs for product and category pages to enhance website SEO and make the customer experience more engaging. For example, you can simplify a product named "BRAND Football ball R15 New" with a product URL from `https://example-shop.com/store/brand-football-ball-r15-new` to a URL like `https://example-foolball-shop.com/store/ball-r15` instead of it containing a full product name.

Read more about [**URL features for custom websites**](./)

### Requirements for Custom Page Slugs

Custom Page Slugs are automatically enabled if:

* Your store is on the [**Business or Unlimited plan**](https://support.ecwid.com/hc/en-us/articles/207100729-Ecwid-plans-and-features).
* Your website has [**Clean URLs enabled**](enable-clean-store-urls-on-a-custom-website.md).

### Step 1. Enable Clean Store URLs.

To set custom slugs, **Clean Store URLs** must be enabled on your custom website.

{% hint style="info" %}
If you use Ecwid Instant Site, you can skip this step as the Clean Store URLs feature is enabled out of the box.
{% endhint %}

Once Clean Store URLs are enabled, set custom slugs for product and category pages in the Ecwid admin panel (supported for Instant Site only) or via the REST API. Learn about [**setting custom slugs through Ecwid admin**](https://support.ecwid.com/hc/en-us/articles/207100509-Improving-SEO-for-Ecwid-site-and-store#-set-custom-url-slugs-for-products-and-categories)

### Step 2. Set custom slugs with REST API

With the Ecwid REST API, you can set custom slugs for both new and existing products or categories:

* Existing Products/Categories: Use the **Update product** and **Update category** endpoints.
* New Products/Categories: Use the **Create product** and **Create category** endpoints.

{% hint style="info" %}
Each request requires the product or category **ID**. If you do not know it, you can find it by the slug itself using REST API. \
\
Learn more about [**finding products and categories by slugs**](set-custom-page-slugs-on-a-custom-website.md#how-to-find-products-and-categories-by-their-slugs)
{% endhint %}

In all endpoints listed above, information related to product/category page slugs is stored in the following fields:

```json
{
	"url": "https://example.com/store/Shoes-p123",
	"autogeneratedSlug": "shoes-p123",
	"customSlug": ""
}
```

Where:

* `url` is the actual storefront URL for the product/category. It is generated from the main store URL and a page slug. If a custom slug exists for the product/category, Ecwid will always use it to generate `url` field value.
* `autogeneratedSlug` is a default page slug Ecwid generates automatically when the product/category is created or its name is updated.
* `customSlug` is a user-defined custom page slug for the product or category page. It has a higher priority than the `autogeneratedSlug` field and therefore overrides it if not empty.

Custom slugs are not updated automatically. If you change the name of a product or category, Ecwid will not update the `customSlug` field automatically. \
\
Table with logic for slug-related fields in products and categories:

<table data-header-hidden data-full-width="false"><thead><tr><th width="194"></th><th></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Field</strong></td><td><strong>Automatically updated when the product name is changed (</strong><code>customSlug</code> <strong>is empty)</strong></td><td><strong>Automatically updated when the product name is changed (</strong>customSlug <strong>has value)</strong></td><td><strong>Automatically updated when</strong> <code>customSlug</code> <strong>is changed</strong></td></tr><tr><td>url</td><td>Yes</td><td>No</td><td>Yes</td></tr><tr><td>autogeneratedSlug</td><td>Yes</td><td>Yes</td><td>No</td></tr><tr><td>customSlug</td><td>n/a</td><td>No</td><td>Yes (manual update)</td></tr></tbody></table>

Find update request examples below.

#### Example: update product name and its custom page slug

You can update the product name and its custom page slug using [**Update product**](../../products/update-product.md) request:

```http
PUT /api/v3/STOREID/products/689454040 HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer SECRET_TOKEN
Content-Type: application/json

{
    "name": "Best Pizza",
    "customSlug": "best-pizza"
}
```

```json
{
    "updateCount": 1
}
```

It is possible to update the custom slug without updating the name and vice versa. However, we recommend updating custom slug value when the name is changed.

The `"updateCount": 1` in the response body means that Ecwid successfully updated 1 product. You'll see an error message otherwise.

#### Example: update category name and its custom page slug

You can update the category name and its custom page slug using [**Update category**](../../categories/update-category.md) request:

```http
PUT /api/v3/STOREID/category/10038652 HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer SECRET_TOKEN
Content-Type: application/json

{
    "name": "Fresh vegetables",
    "customSlug": "vegetables"
}
```

```json
{
    "updateCount": 1
}
```

It is possible to update the custom slug without updating the name and vice versa. However, we recommend updating custom slug value when the name is changed.

The `"updateCount": 1` in the response means that Ecwid successfully updated 1 category. You'll see an error message otherwise.

### How to find products and categories by their slugs

The default approach to finding a product or category ID requires knowing the name, description, or SKU of said product or category. However, you can get these IDs much easier by using page slug as a search term with a dedicated [**GET request**](../get-page-slug-and-static-code.md).

This request accepts page `slug` as a search parameter and responds with product or category ID, page slug details, and static code data for the page. The method works with any `slug` value that ever worked on the storefront including partial URLs, and the history of slug changes.

Let's take a look at the following example of a product example where the product name remains the same (`Pizza`), but the default page slug has been changed two times:

`/products/Pizza-p689454040` -> `/products/best-pizza` -> `/products/pizza`

`/products/Pizza-p689454040` was the default page slug, generated by Ecwid upon product creation.\
`/products/best-pizza` was the first custom page slug that was changed later to another custom slug.\
`/products/pizza` is the actual custom slug, currently working on the storefront. Both previous slugs do not work on the storefront now.

Let's find the page with different slug values using [**Get page slug**](../get-page-slug-and-static-code.md):

* Search by partial URL with only product ID: `?slug=-p689454040`

```http
GET /api/v3/STOREID/storefront-widget-pages?slug=-p689454040 HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer SECRET_TOKEN
```

```json
{
    "status": "NONCANONICAL",
    "type": "PRODUCT",
    "canonicalSlug": "pizza",
    "storeEntityData": {
        "id": "689454040"
    }
}
```

* Search by partial URL with only product name: `?slug=Pizza`

```http
GET /api/v3/STOREID/storefront-widget-pages?slug=Pizza HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer SECRET_TOKEN
```

```json
{
    "status": "NONCANONICAL",
    "type": "PRODUCT",
    "canonicalSlug": "pizza",
    "storeEntityData": {
        "id": "689454040"
    }
}
```

* Search by default page slug: `?slug=Pizza-p689454040`

```http
GET /api/v3/STOREID/storefront-widget-pages?slug=Pizza-p689454040 HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer SECRET_TOKEN
```

```json
{
    "status": "NONCANONICAL",
    "type": "PRODUCT",
    "canonicalSlug": "pizza",
    "storeEntityData": {
        "id": "689454040"
    }
}
```

* Search by partial URL of a custom slug (and the actual custom slug): `?slug=pizza`

```http
GET /api/v3/STOREID/storefront-widget-pages?slug=pizza HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer SECRET_TOKEN
```

```json
{
    "status": "OK",
    "type": "PRODUCT",
    "canonicalSlug": "pizza",
    "storeEntityData": {
        "id": "689454040"
    }
}
```

* Search by slug history: `?slug=pizza-test`

```http
GET /api/v3/STOREID/storefront-widget-pages?slug=best-pizza HTTP/1.1
Host: app.ecwid.com
Authorization: Bearer SECRET_TOKEN
```

```json
{
    "status": "NONCANONICAL",
    "type": "PRODUCT",
    "canonicalSlug": "pizza",
    "storeEntityData": {
        "id": "689454040"
    }
}
```

All these options respond with the product ID allowing you to change its slug. However, you can use the same request to also receive static page code. [**Learn more**](../get-page-slug-and-static-code.md)

### Still have questions?

[**Email us**](mailto:ec.apps@lightspeedhq.com) with all the details that might help: your store ID, website URL and platform, server rewrite rules, and product/category ID with custom slugs. We are here to assist!
