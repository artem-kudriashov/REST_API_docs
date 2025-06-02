# Preview Instant Site changes

Generate a link to preview the unpublished changes made to the Instant Site.

### Step 1. Get a draft token

Get a token with the `draft_code` parameter: [get-instant-site-api-token.md](get-instant-site-api-token.md "mention")

### Step 2. Open Instant Site in preview mode

Create the following URL using Instant Site token and your site URL: `{siteUrl}?draft&signature={signature}`

where:

* `{siteUrl}` – URL of your Instant Site.
* `{signature}` – Instant Site token generated with the `draft_code` type.

For example: `https://store1003.company.site?draft&signature=cde456***`. Now you can open the resulting link to see your Instant Site in Preview mode.
