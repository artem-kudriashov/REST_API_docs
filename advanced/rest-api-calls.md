# REST API calls

Base URL: `https://app.ecwid.com/api/v3/{storeId}`&#x20;

Full list of endpoints and calls below.

#### Store profile, checkout extra fields, shipping options, payment options

<details>

<summary>Endpoint | Supported HTTP calls</summary>

<table data-header-hidden><thead><tr><th width="450.46875">Endpoint</th><th>Supported HTTP calls</th></tr></thead><tbody><tr><td><code>/profile</code> </td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:purple;"><code>PUT</code></mark></td></tr><tr><td><code>/profile/staffScopes</code></td><td><mark style="color:green;"><code>GET</code></mark></td></tr><tr><td><code>/profile/order_statuses</code> </td><td><mark style="color:green;"><code>GET</code></mark></td></tr><tr><td><code>/profile/order_status/{statusId}</code></td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:purple;"><code>PUT</code></mark></td></tr><tr><td><code>/profile/extrafields</code></td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:blue;"><code>POST</code></mark> </td></tr><tr><td><code>/profile/extrafields/{key}</code></td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:purple;"><code>PUT</code></mark> <mark style="color:red;"><code>DELETE</code></mark></td></tr><tr><td><code>/profile/logo</code></td><td><mark style="color:blue;"><code>POST</code></mark> <mark style="color:red;"><code>DELETE</code></mark></td></tr><tr><td><code>/profile/invoicelogo</code></td><td><mark style="color:blue;"><code>POST</code></mark> <mark style="color:red;"><code>DELETE</code></mark></td></tr><tr><td><code>/profile/emaillogo</code></td><td><mark style="color:blue;"><code>POST</code></mark> <mark style="color:red;"><code>DELETE</code></mark></td></tr><tr><td><code>/profile/shippingOptions</code></td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:blue;"><code>POST</code></mark> </td></tr><tr><td><code>/profile/shippingOptions/{shippingOptionId}</code></td><td><mark style="color:purple;"><code>PUT</code></mark> <mark style="color:red;"><code>DELETE</code></mark></td></tr><tr><td><code>/profile/paymentOptions</code></td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:blue;"><code>POST</code></mark> </td></tr><tr><td><code>/profile/paymentOptions/{paymentOptionId}</code></td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:purple;"><code>PUT</code></mark> <mark style="color:red;"><code>DELETE</code></mark></td></tr></tbody></table>

</details>

#### Store stats, deleted items history, store reports

<mark style="color:green;">`GET`</mark> `/reports/{reportType}`&#x20;

<mark style="color:green;">`GET`</mark> `/latest-stats`&#x20;

#### Orders

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/orders`&#x20;

<mark style="color:green;">`GET`</mark> `/orders/last`&#x20;

<mark style="color:green;">`GET`</mark> `/orders/deleted`

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/orders/{orderId}`&#x20;

<mark style="color:green;">`GET`</mark> `/orders/{orderId}/repeatURL`&#x20;

<mark style="color:green;">`GET`</mark> `/orders/{orderId}/invoice-pdf`&#x20;

<mark style="color:green;">`GET`</mark> `/orders/{orderId}/invoices`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/orders/{orderId}/extraFields`&#x20;

<mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/orders/{orderId}/extraFields/{extraFieldId}`&#x20;

<mark style="color:blue;">`POST`</mark> `/order/calculate`&#x20;

<mark style="color:blue;">`POST`</mark> `/orders/{orderId}/invoices/create-invoice`&#x20;

#### Abandoned carts

<mark style="color:green;">`GET`</mark> `/carts`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> `/carts/{cartId}`&#x20;

<mark style="color:blue;">`POST`</mark> `/carts/{cartId}/place`&#x20;

#### Recurring subscriptions

<mark style="color:green;">`GET`</mark> `/subscriptions`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> `/subscriptions/{subscriptionId}`

#### Products, product variations, brands, classes, swatches

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/products`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `products/{productId}/gallery/video/{galleryVideoId}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/combinations`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/combinations/{combinationId}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> `/products/sort`&#x20;

<mark style="color:green;">`GET`</mark> `/products/deleted`&#x20;

<mark style="color:purple;">`PUT`</mark> `/products/{productId}/inventory`&#x20;

<mark style="color:purple;">`PUT`</mark> `/products/{productId}/combinations/{combinationId}/inventory`&#x20;

<mark style="color:purple;">`PUT`</mark> `/products/{productId}/media`&#x20;

<mark style="color:blue;">`POST`</mark> `/products/filters`&#x20;

<mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/files`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/files/{fileId}`&#x20;

<mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/image`&#x20;

<mark style="color:blue;">`POST`</mark> `/products/{productId}/image/async`&#x20;

<mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/video`

<mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/gallery`&#x20;

<mark style="color:blue;">`POST`</mark> `/products/{productId}/gallery/async`&#x20;

<mark style="color:blue;">`POST`</mark> `/products/{productId}/gallery/video`

<mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/products/{productId}/combinations/{combinationId}/image`&#x20;

<mark style="color:blue;">`POST`</mark> `/products/{productId}/combinations/{combinationId}/image/async`&#x20;

<mark style="color:red;">`DELETE`</mark> `/products/{productId}/gallery/{galleryImageId}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/classes`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/classes/{classId}`&#x20;

<mark style="color:green;">`GET`</mark> `/brands`&#x20;

<mark style="color:green;">`GET`</mark> `/swatches`&#x20;

#### Product reviews

<mark style="color:green;">`GET`</mark> `/reviews`&#x20;

<mark style="color:green;">`GET`</mark> `/reviews/filters_data`&#x20;

<mark style="color:green;">`GET`</mark> `/reviews/deleted`&#x20;

<mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/reviews/{reviewId}`&#x20;

<mark style="color:purple;">`PUT`</mark> `/reviews/mass_update`&#x20;

#### Categories

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/categories`&#x20;

<mark style="color:green;">`GET`</mark> `/categoriesByPath`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/categories/{categoryId}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> `/categories/sort`

<mark style="color:blue;">`POST`</mark> <mark style="color:red;">`DELETE`</mark> `/categories/{categoryId}/image`&#x20;

<mark style="color:blue;">`POST`</mark> `/categories/{categoryId}/image/async`&#x20;

<mark style="color:blue;">`POST`</mark> `/categories/{categoryId}/assignProducts`&#x20;

<mark style="color:blue;">`POST`</mark> `/categories/{categoryId}/unassignProducts`&#x20;

#### Customers, customer groups, customer extra fields

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/customers`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/customers/{customerId}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/customers/{customerId}/contacts`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/customers/{customerId}/contacts/{contactId}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/store_extrafields/customers`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/store_extrafields/customers/{extrafield_key}`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/customer_groups`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/customer_groups/{groupId}`&#x20;

<mark style="color:green;">`GET`</mark> `/customers/deleted`&#x20;

#### Promotions, discount coupons

<details>

<summary>Endpoint | Supported HTTP calls</summary>

<table data-header-hidden><thead><tr><th width="449.84375">Endpoint</th><th>Supported HTTP calls</th></tr></thead><tbody><tr><td><code>/promotions</code> </td><td><mark style="color:green;"><code>GET</code></mark>  <mark style="color:blue;"><code>POST</code></mark> </td></tr><tr><td><code>/promotions/{promotionId}</code> </td><td><mark style="color:purple;"><code>PUT</code></mark> <mark style="color:red;"><code>DELETE</code></mark> </td></tr><tr><td><code>/discount_coupons/</code> </td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:blue;"><code>POST</code></mark> </td></tr><tr><td><code>/discount_coupons/{discountCouponId}</code> </td><td><mark style="color:green;"><code>GET</code></mark> <mark style="color:purple;"><code>PUT</code></mark> <mark style="color:red;"><code>DELETE</code></mark> </td></tr><tr><td><code>/coupons/deleted</code> </td><td><mark style="color:green;"><code>GET</code></mark></td></tr></tbody></table>

</details>

#### Domains

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> `/domains`&#x20;

<mark style="color:green;">`GET`</mark> `/domains/search`&#x20;

<mark style="color:blue;">`POST`</mark> `/domains/purchase`&#x20;

<mark style="color:blue;">`POST`</mark> `/domains/send_domain_verification_email`&#x20;

<mark style="color:blue;">`POST`</mark> `/domains/reset_domain_password`&#x20;

#### Dictionaries

<mark style="color:green;">`GET`</mark> `/countries`&#x20;

<mark style="color:green;">`GET`</mark> `/currencies`&#x20;

<mark style="color:green;">`GET`</mark> `/currencyByCountry`&#x20;

<mark style="color:green;">`GET`</mark> `/states`&#x20;

<mark style="color:green;">`GET`</mark> `/taxClasses`&#x20;

#### Staff accounts

<mark style="color:green;">`GET`</mark> <mark style="color:blue;">`POST`</mark> `/staff`&#x20;

<mark style="color:green;">`GET`</mark> <mark style="color:purple;">`PUT`</mark> <mark style="color:red;">`DELETE`</mark> `/staff/{staffAccountId}`&#x20;
