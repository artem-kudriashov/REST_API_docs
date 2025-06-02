# Purchase domain

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/{storeId}/domains/purchase`&#x20;

### Required access scopes

Your app must have the following **access scopes** to make this request: `buy_domains`

### Path params

All path params are required.

| Param   | Type   | Description     |
| ------- | ------ | --------------- |
| storeId | number | Ecwid store ID. |

### Request JSON

A JSON object with the following fields:

| Field               | Type   | Description                                                |
| ------------------- | ------ | ---------------------------------------------------------- |
| domainName          | string | Domain name for purchase.                                  |
| firstName           | string | First name of domain owner.                                |
| lastName            | string | Last name of domain owner.                                 |
| email               | string | Email address of domain owner.                             |
| street              | string | Street address.                                            |
| city                | string | City address.                                              |
| countryCode         | string | A two-letter ISO code of country where domain owner lives. |
| postalCode          | string | Postal code or ZIP code.                                   |
| stateOrProvinceCode | string | State code (e.g. `NY`) or a region name.                   |
| phone               | string | Phone number of domain owner.                              |
| companyName         | string | The company name used in domain purchase.                  |

### Response JSON

A JSON object with the following fields:

| Field                   | Type                   | Description                                                                                                                      |
| ----------------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| id                      | number                 | Internal ID of purchased domain                                                                                                  |
| name                    | string                 | Purchased domain name, e.g. "mysuperstore.com"                                                                                   |
| status                  | string                 | Status of purchased domain                                                                                                       |
| connectedToInstantSite  | boolean                | Shows if this domain is connected to Instant Site. Available values: `true`, `false`                                             |
| primaryDomain           | boolean                | Shows if this domain is the main one. Available values: `true`, `false`                                                          |
| redirectToPrimaryDomain | boolean                | Shows if this domain redirects to the main one. Displays only if the `"primaryDomain": false`. Available values: `true`, `false` |
| purchaseDate            | string                 | Date of domain purchase                                                                                                          |
| expirationDate          | string                 | Date of domain expiration                                                                                                        |
| renewalDate             | string                 | Date of next charge for domain renewal                                                                                           |
| autorenew               | boolean                | Shows if automatic renewal charge is enabled. Available values: `true`, `false`                                                  |
| domainOwnerInfo         | object domainOwnerInfo | Domain owner details specified in purchase process                                                                               |
| billingInfo             | object billingInfo     | Domain billing information                                                                                                       |

#### domainOwnerInfo

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
