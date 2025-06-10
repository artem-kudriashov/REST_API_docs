# Get Instant Site profile (apiv1)

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/profile`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Header</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token-apiv1.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="238.53125">Field</th><th width="137.38671875">Type</th><th>Description</th></tr></thead><tbody><tr><td>siteId</td><td>string</td><td>Ecwid store ID</td></tr><tr><td>locale</td><td>string</td><td>Site locale that matches the default website language.</td></tr><tr><td>enabledLanguages</td><td>array of strings</td><td>List of enabled languages.</td></tr><tr><td>storeName</td><td>string</td><td>Name of the website used in SEO and visible in browser tabs.</td></tr><tr><td>tracking</td><td>object <a href="get-instant-site-profile-apiv1.md#tracking">tracking</a></td><td>Information about enabled tracking systems on Instant Site.</td></tr><tr><td>countryCode</td><td>string</td><td>Two-digit country code of the store location.</td></tr><tr><td>postalCode</td><td>string</td><td>ZIP code of the store location.</td></tr><tr><td>email</td><td>string</td><td>Email specified as the "store email" in the Instant Site editor.</td></tr><tr><td>dateFormat</td><td>string</td><td>Date format used on the website, for example, <code>"dd.MM.yyyy"</code>.</td></tr><tr><td>timeFormat</td><td>string</td><td>Time format used on the website, for example, <code>"HH:mm:ss"</code>.</td></tr><tr><td>timezoneOffsetInMinutes</td><td>number</td><td>Offset of the store time from the UTC +0 in minutes.</td></tr><tr><td>storeClosed</td><td>boolean</td><td>Defines if the store is closed. <br><br>If a store is closed, it shows a "Closed for maintenance" banner instead of the product browser on the storefront.</td></tr><tr><td>storeSuspended</td><td>boolean</td><td>Defines if the store is suspended. <br><br>If a store is suspended, its product browser is still available on the storefront, but dthe checkout (and therefore the ability to place orders) is disabled.</td></tr><tr><td>isTemplateSite</td><td>boolean</td><td>Defines if a store is used as a template for one of the Site template applications.</td></tr><tr><td>siteUrl</td><td>string</td><td>Main website URL.</td></tr><tr><td>subscription</td><td>object <a href="get-instant-site-profile-apiv1.md#subscription">subscription</a></td><td>Information about store subscription without any payment details.</td></tr><tr><td>latestPublishTimestamp</td><td>number</td><td>UNIX timestamp of the latest published change for the Instant Site, for example, <code>1739945860</code>.</td></tr><tr><td>onboarding</td><td>object onboarding</td><td>Internal onboarding settings.</td></tr><tr><td>vertical</td><td>string</td><td>Answer to the question "What type of products will you be selling?" that defines sample products added to the store.<br><br>Supported values: <code>apparel</code>, <code>art</code>, <code>auto</code>, <code>books</code>, <code>electronics</code>, <code>food_restaurant</code>, <code>food_ecommerce</code>, <code>gifts</code>, <code>hardware</code>, <code>health</code>, <code>home</code>, <code>jewelry</code>, <code>office</code>, <code>pet</code>, <code>services</code>, <code>sports</code>, <code>streaming</code>, <code>subscription_product</code>, <code>toys</code>, <code>tobacco</code>, <code>adult</code>, <code>notsure</code>, <code>other</code>.</td></tr><tr><td>previewTemplateInsideEditor</td><td>boolean</td><td>Defines if the Instant Site preview opens inside the editor or on a separate page.</td></tr><tr><td>featureFlags</td><td>object featureFlags</td><td>List of internal features and their states.</td></tr><tr><td>isDraftChanged</td><td>boolean</td><td>Defines if current draft is different from the published version.</td></tr><tr><td>hideEcwidLinks</td><td>boolean</td><td>Defines if Ecwid branding links are visible.</td></tr><tr><td>selectedSiteTemplateId</td><td>string</td><td>Internal ID of the currently selected Site template. </td></tr></tbody></table>

#### tracking

| Field                      | Type    | Description                                       |
| -------------------------- | ------- | ------------------------------------------------- |
| googleUniversalAnalyticsId | string  | Google Analytics ID assigned to the Instant Site. |
| heapEnabled                | boolean | State of the internal heap feature.               |

#### subscription

<table><thead><tr><th width="365.43359375">Field</th><th width="89.48046875">Type</th><th>Description</th></tr></thead><tbody><tr><td>channelId</td><td>string</td><td>Google Analytics ID assigned to the Instant Site.</td></tr><tr><td>channelType</td><td>string</td><td>State of the internal heap feature.</td></tr><tr><td>planName</td><td>string</td><td>Internal name of the store billing plan.</td></tr><tr><td>planPeriod</td><td>string</td><td>Billing period. One of: <code>monthly</code>, <code>yearly</code>.</td></tr><tr><td>isPaid</td><td>boolean</td><td>Defines if the store is on a paid (<code>true</code>) or free (<code>false</code>) plan.</td></tr><tr><td>isAllowNewCookieBanner</td><td>boolean</td><td>Defines if the cookie banner is enabled on the storefront.</td></tr><tr><td>maxPageNumber</td><td>number</td><td>Max number of pages for the Instant Site. Default value: <code>100</code>.</td></tr><tr><td>isMultilingualStoreFeatureEnabled</td><td>boolean</td><td>Defines if the multilingual feature is enabled for the store.</td></tr><tr><td>isAdvancedDiscountsFeatureAvailable</td><td>boolean</td><td>Defines if the promotions (advanced discounts feature) are enabled in the store.</td></tr><tr><td>isBasicEcommerceFeatureEnabled</td><td>boolean</td><td>Defines if the checkout is enabled in the store.</td></tr><tr><td>isRichTextEditorEnabled</td><td>boolean</td><td>Defines if the "rich text" feature is enabled for text fields in the Instant Site editor.</td></tr><tr><td>isTemplateMarketFeatureEnabled</td><td>boolean</td><td>Defines if the Site templates market is enabled in the Instant Site editor.</td></tr><tr><td>isAccessToControlPanel</td><td>boolean</td><td>Defines if access to the Ecwid admin is enabled for the store.</td></tr><tr><td>isStorefrontAgeConfirmationFeatureEnabled</td><td>boolean</td><td>Defines if the age confirmation popup is enabled on the storefront.</td></tr></tbody></table>

