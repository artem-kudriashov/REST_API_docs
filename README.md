# REST API overview

Ecwid REST API allows you to access and manage any store data, payment and shipping methods, and storefront settings.

We use OAuth 2.0 authorization simplified for single-store customizations, JSON-formatted data, and a clear structure.&#x20;

Please note that our REST API has **rate limits**.

We accept up to **600 requests per minute** **per token**. If you exceed the limit, all subsequent requests will be ignored with an error 429 and a **"Retry-After": N** header (number **N** is a cooldown) . If more requests continue to come from a non-working token, Ecwid will block it for much longer after 20 requests per minute or a total of 600 requests with non-working tokens per IP.

### Get access to REST API

If you don't yet have access to Ecwid API, follow the detailed instructions in these articles:

1. [Set up your dev environment in Ecwid](https://app.gitbook.com/s/uOzT5egoVTAjMJwRuMQT/get-started/set-up-your-dev-environment-in-ecwid "mention")
2. [Make your first API request](https://app.gitbook.com/s/uOzT5egoVTAjMJwRuMQT/get-started/make-your-first-api-request "mention")
3. [Add more features to your custom app](https://app.gitbook.com/s/uOzT5egoVTAjMJwRuMQT/get-started/add-more-features-to-your-custom-app "mention")

### Get started with the popular API calls

<table data-view="cards"><thead><tr><th></th><th data-type="content-ref"></th><th data-type="content-ref"></th><th data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>General store settings:</strong></td><td><a href="rest-api/store-profile/get-store-profile.md">get-store-profile.md</a></td><td><a href="rest-api/store-profile/update-store-profile.md">update-store-profile.md</a></td><td><a href="rest-api/store-profile/store-reports/">store-reports</a></td></tr><tr><td><strong>Orders:</strong></td><td><a href="rest-api/orders/search-orders.md">search-orders.md</a></td><td><a href="rest-api/orders/abandonned-carts/search-abandoned-carts.md">search-abandoned-carts.md</a></td><td><a href="rest-api/orders/calculate-order-details.md">calculate-order-details.md</a></td></tr><tr><td><strong>Products:</strong></td><td><a href="rest-api/products/search-products.md">search-products.md</a></td><td><a href="rest-api/products/product-variations/search-product-variations.md">search-product-variations.md</a></td><td><a href="rest-api/products/product-reviews/search-product-reviews.md">search-product-reviews.md</a></td></tr><tr><td><strong>Customers:</strong></td><td><a href="rest-api/customers/search-customers.md">search-customers.md</a></td><td><a href="rest-api/customers/customer-groups/search-customer-groups.md">search-customer-groups.md</a></td><td><a href="rest-api/customers/update-customer.md">update-customer.md</a></td></tr><tr><td><strong>Categories:</strong></td><td><a href="rest-api/categories/search-categories.md">search-categories.md</a></td><td><a href="rest-api/categories/manage-order-of-products-in-the-category/assign-products-to-the-category.md">assign-products-to-the-category.md</a></td><td><a href="rest-api/categories/category-images/upload-category-image.md">upload-category-image.md</a></td></tr><tr><td><strong>Discounts:</strong></td><td><a href="rest-api/discounts/promotions/search-promotions.md">search-promotions.md</a></td><td><a href="rest-api/discounts/promotions/create-promotion.md">create-promotion.md</a></td><td><a href="rest-api/discounts/discount-coupons/search-discount-coupons.md">search-discount-coupons.md</a></td></tr></tbody></table>

