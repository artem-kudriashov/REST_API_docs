# Search store domains

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/{storeId}/domains`&#x20;

<details>

<summary>Request and response example</summary>

Request:

```curl
curl --location 'https://app.ecwid.com/api/v3/1003/domains' \
--header 'Authorization: Bearer secret_ab***cd'
```

Response:

```json
{
    "instantSiteDomain": {
        "primaryInstantSiteDomain": "1003",
        "ecwidSubdomain": "1003",
        "instantSiteIpAddress": "101.202.303.404",
        "instantSiteUrl": "https://1003.company.site"
    },
    "purchasedDomains": []
}
```

</details>

### Required access scopes

Your app must have the following **access scopes** to make this request: `read_store_profile`, `buy_domains`

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Query params

All query params are optional.

<table data-full-width="false"><thead><tr><th width="187">Name</th><th width="97">Type</th><th>Description</th></tr></thead><tbody><tr><td>responseFields</td><td>string</td><td>Specify the exact fields to receive in response JSON. If not specified, the response JSON will have all available fields for the entity.<br><br>For example: <code>?responseFields=instantSiteDomain(instantSiteIpAddress)</code></td></tr></tbody></table>

Example of using `responseFields` param:

{% tabs %}
{% tab title="Request" %}
```
curl --location 'https://app.ecwid.com/api/v3/1003/profile?responseFields=instantSiteDomain(instantSiteIpAddress)' \
--header 'Authorization: Bearer secret_ab***cd'
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "instantSiteDomain": {
        "instantSiteIpAddress": "18.213.217.106"
    }
}
```
{% endtab %}
{% endtabs %}

### Headers

The **Authorization** header is required.

<table><thead><tr><th>Header</th><th width="252">Format</th><th>Description</th></tr></thead><tbody><tr><td>Authorization</td><td><code>Bearer secret_ab***cd</code></td><td>Access token of the application.</td></tr></tbody></table>

{% include "../../.gitbook/includes/rest-api-response-json.md" %}

| Field             | Type                                                                          | Description                                             |
| ----------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------- |
| instantSiteDomain | object [instantSiteDomain](search-store-domains.md#instantsitedomain)         | Details for the currently enabled store domain.         |
| purchasedDomains  | array of objects [purchasedDomains](search-store-domains.md#purchaseddomains) | List with details for each domain bought for the store. |

#### instantSiteDomain

| Field                          | Type   | Description                                                                                                                                                                              |
| ------------------------------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| primaryInstantSiteDomain       | string | Main domain for the Instant Site, based on the `ecwidSubdomain`                                                                                                                          |
| primaryInstantSiteDomainStatus | string | Possible values: `connected` if the `primaryInstantSiteDomain` is connected to the Instant Site and works already, `pending` if the `primaryInstantSiteDomain` is still being configured |
| ecwidSubdomain                 | string | Subdomain of the default Instant Site URL.                                                                                                                                               |
| instantSiteIpAddress           | string | IP address used to connect a custom domain with the Instant Site. It's also available in the Control Panel on the `#website-overview:section=mobile-domain` page.                        |
| instantSiteUrl                 | string | Current Instant Site URL, based on the `ecwidSubdomain`                                                                                                                                  |
| thirdPartyVendorDomain         | string | Custom domain specified in the Control Panel settings. Has the same value as the `customDomain` in the Instant Site Info.                                                                |

#### purchasedDomains

| Field                   | Type                                                                        | Description                                                                                                                      |
| ----------------------- | --------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| id                      | number                                                                      | Internal ID of purchased domain                                                                                                  |
| name                    | string                                                                      | Purchased domain name, e.g. "mysuperstore.com"                                                                                   |
| status                  | string                                                                      | Status of purchased domain                                                                                                       |
| connectedToInstantSite  | boolean                                                                     | Shows if this domain is connected to Instant Site. Available values: `true`, `false`                                             |
| primaryDomain           | boolean                                                                     | Shows if this domain is the main one. Available values: `true`, `false`                                                          |
| redirectToPrimaryDomain | boolean                                                                     | Shows if this domain redirects to the main one. Displays only if the `"primaryDomain": false`. Available values: `true`, `false` |
| purchaseDate            | string                                                                      | Date of domain purchase                                                                                                          |
| expirationDate          | string                                                                      | Date of domain expiration                                                                                                        |
| renewalDate             | string                                                                      | Date of next charge for domain renewal                                                                                           |
| autorenew               | boolean                                                                     | Shows if automatic renewal charge is enabled. Available values: `true`, `false`                                                  |
| domainRegistrantInfo    | object [domainRegistrantInfo](search-store-domains.md#domainregistrantinfo) | Domain owner details specified in purchase process                                                                               |
| billingInfo             | object [billingInfo](search-store-domains.md#billinginfo)                   | Domain billing information                                                                                                       |

#### domainRegistrantInfo

| Field               | Type   | Description                                                                                                                                                                          |
| ------------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| verificationStatus  | string | `"verified"` if the verification is complete                                                                                                                                         |
| firstName           | string | First name of domain owner                                                                                                                                                           |
| lastName            | string | Last name of domain owner                                                                                                                                                            |
| email               | string | Email address of domain owner                                                                                                                                                        |
| street              | string | Street address                                                                                                                                                                       |
| city                | string | City address                                                                                                                                                                         |
| countryCode         | string | A two-letter ISO code of country where domain owner lives                                                                                                                            |
| postalCode          | string | Postal code or ZIP code                                                                                                                                                              |
| stateOrProvinceCode | string | State code (e.g. `NY`) or a region name. See valid codes here: [https://api-docs.ecwid.com/reference/list-of-state-codes](https://api-docs.ecwid.com/reference/list-of-state-codes). |
| phone               | string | Phone number of domain owner                                                                                                                                                         |
| companyName         | string | The company name used in domain purchase                                                                                                                                             |

#### billingInfo

| Field                            | Type   | Description                                               |
| -------------------------------- | ------ | --------------------------------------------------------- |
| totalRenewalDomainPrice          | number | Total price for domain renewal                            |
| renewalDomainPrice               | number | Price of domain                                           |
| renewalTax                       | number | Tax for domain price                                      |
| whoisPrivacyFeaturePrice         | number | Price for the "whois Privacy" feature                     |
| currency                         | string | Currency for domain renewal, e.g. `"USD"`                 |
| totalRenewalDomainPriceFormatted | string | Formatted total price for domain renewal, e.g. `"$99.00"` |
