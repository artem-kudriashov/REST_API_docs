# Get Instant Site text labels

<mark style="color:green;">`GET`</mark> `https://vuega.ecwid.com/api/v1/{storeId}/translation`

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

### Response JSON

A JSON object with the following fields:

<table><thead><tr><th width="199.8984375">Field</th><th width="199.609375">Type</th><th>Description</th></tr></thead><tbody><tr><td>editorTranslations</td><td>object editorTranslations</td><td>Map of text labels for the store Editor texts where the "key" is the label, and "value" is the text value. For example, <code>"Section.SEO.ChangeSeoSettings.button": "Change SEO Settings"</code>.</td></tr><tr><td>websiteTranslations</td><td>object websiteTranslations</td><td>Map of text labels for the store Editor texts where the "key" is the label, and "value" is the text value. For example, <code>"Pricing.NameYourPrice": "Free or your own price"</code>.</td></tr><tr><td>languageTranslations</td><td>object <a data-mention href="get-instant-site-text-labels.md#languagetranslations">#languagetranslations</a></td><td>Map of language codes for languages enabled in the store and their name translations where the "key" is the language two-digit ISO code, and "value" is the object that maps language code and name translation. Find a code example below.</td></tr></tbody></table>

#### languageTranslations

```json
"languageTranslations": {
        "en": {
            "Language.en": "English",
            "Language.cs": "Czech"
        },
        "cs": {
            "Language.en": "Angličtina",
            "Language.cs": "Čeština"
        }
    }
```
