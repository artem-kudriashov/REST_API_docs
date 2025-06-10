# Create Instant Site page

<mark style="color:blue;">`POST`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/page`

### Required access scopes

Your app must have the following **access scopes** to make this request: `manage_instant_site`

### Path params

All path params are **required**.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Headers

The **Authorization** header is required.

<table><thead><tr><th width="138.484375">Field</th><th width="86.42578125">Type</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td>string</td><td>Token for Instant Site API calls. <a href="../get-instant-site-api-token-apiv1.md">Get token</a><br><br>Requires a token with <code>grant_type=authorization_code</code> type.</td></tr></tbody></table>

### Request JSON

A JSON object with the following fields:

<table><thead><tr><th width="210.3515625">Field</th><th width="119.7421875">Type</th><th>Description</th></tr></thead><tbody><tr><td>title</td><td>string</td><td>Name of the page visible to the store owner in Instant Site editor.</td></tr><tr><td>urlPath</td><td>string</td><td>Page path on the website, for example, <code>"/legal"</code>.</td></tr><tr><td>visible</td><td>boolean</td><td>Defines if the page is enabled and visible on the storefront.</td></tr><tr><td>visibleHeader</td><td>boolean</td><td>Defines if the page header is enabled and visible on the storefront.</td></tr><tr><td>visibleFooter</td><td>boolean</td><td>Defines if the page footer is enabled and visible on the storefront.</td></tr><tr><td>visibleAnnouncementBar</td><td>boolean</td><td>Defines if the announcement bar ah the page top is enabled and visible on the storefront.</td></tr><tr><td>seoTitle</td><td>string</td><td>Page title for search crawlers and SEO tools. If specified, overrides <code>title</code> for them.</td></tr><tr><td>seoDescription</td><td>string</td><td>Page description for search crawlers and SEO tools.</td></tr><tr><td>shareImage</td><td>string</td><td>Image that is shown when the page link with the preview is shared in social media.</td></tr><tr><td>indexed</td><td>boolean</td><td>Defines if the page should be indexed by web search services.</td></tr><tr><td>isAvailableToEdit</td><td>boolean</td><td>Defines if the page can be edited through the Instant Site editor in Ecwid admin.</td></tr><tr><td>tileIds</td><td>array of strings</td><td>List of tile IDs that are enabled on this page. Order of tiles in this list is applied to the page (first tile at the top, last - at the bottom).</td></tr></tbody></table>

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="149.6171875">Field</th><th width="150.29296875">Type</th><th>Description</th></tr></thead><tbody><tr><td>pageId</td><td>string</td><td>Internal ID of the created page.</td></tr></tbody></table>



