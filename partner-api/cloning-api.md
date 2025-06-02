# Cloning API

The Ecwid Partner APIs allows an Ecwid reseller to create and manage accounts (stores) in Ecwid. In some cases, it may be convenient to have a single "template" store and clone it to create new stores — to make it easier pre-filling new stores with products, settings etc. The Ecwid Clone Store API can be used to do that.

{% hint style="warning" %}
Your app requires `CLONE_STORES` access scope to use this endpoint. Please [contact us](mailto:partneraccount@ecwid.com) to add it to the app's scope list.
{% endhint %}

### Requirements

The Ecwid Clone Store API will respond with an error message if something goes wrong, so you will detect an issues if there is one. Still, there are a few points you can check in advance to save time:

* **Get API keys.** The Clone API is a part of the Ecwid API v3. To access it, you will need to have Ecwid API v3. That includes the "_app ID_" and "_app secret_" keys with the API access level sufficient to clone store data. If you don't have the keys or your app doesn't have the appropriate access scope, please contact the Ecwid team.
* **Create/prepare a new store.** The Clone API doesn't create new stores — it just copies the store data from one store to another. If you want to create a duplicate store using some existing store as a template, your first step would be to create a new empty store. To create a new store, you will use either the Ecwid Partner API or the Ecwid API v3 or the reseller panel.
* **Make sure the target store is empty.** The clone data process requires the target store catalog to be empty — that means the store should contain zero products, categories and product types. Demo products and categories do not count — it's okay to have them in the target store. So, you're fine if you just create a new store and start cloning data from an existing store to it. But if the target store is not new and already has some products, you will have to remove them (or create a new blank store).

### Step 1. Initiate cloning — POST /stores/clone

The clone store API is asynchronous: at the first step, you request to clone one store's data into another; at the second step, you check the status of the task and get results.

This step will tell Ecwid to start copying data from one store (source store) to another (target store).

#### Endpoint

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/stores/clone`

#### Query params

* `sourceStoreId`: ID of the store, which data you want to copy to the target store
* `targetStoreId`: ID of the target store — the one that will be filled with the data if everythings goes well
* `cloneDemoCatalog`: if `true` clones sample products from the target store
* `scope`: defines what to copy from the source to the target store. Supported values:
  * `STORE\_SETTINGS` — Copy _only_ store settings including shipping settings, payment options, taxes, store administrator profile, design settings, marketplaces feed settings, invoice and mail settings and other. The following is not copied: email/password of the store owner, installed apps and their data.
  * `CATALOG` — Copy _only_ store product catalog including products, images, categories, product options and variations, product attributes.
  * — If not specified, call copies both store settings and the catalog.

#### Headers

* `X-Ecwid-App-Client-Id` - _client\_id_ ID of your Ecwid application (provided by the Ecwid team).
* `X-Ecwid-App-Secret-Key` - _client\_secret_ of your Ecwid application.

#### Request example

```http
POST /api/v3/stores/clone?sourceStoreId=1003&targetStoreId=9001&scope=CATALOG HTTP/1.1
Host: app.ecwid.com
X-Ecwid-App-Client-Id: client_id
X-Ecwid-App-Secret-Key: client_secret
```

#### Response

Ecwid will validate the input parameters and source/target stores to make a pre-flight check. If store data cannot be cloned for some reason, you will immediately get an error message in response. If everything is OKay, you will get a task ID (ticket), which you will use later to check the status of the task. Additionally, you will get a 'success' field containing either 'true' or 'false' so you can easily detect whether the request was successful. IMPORTANT: the success status means Ecwid has started to clone the data, it doesn't mean the cloning has been completed.

#### Response example (success)

```json
{
    "ticket": "352397e5-e9c0-4e90-ba43-252813aa14cb",
    "success": true
}
```

#### Response example (failure)

```json
{
    "success": false,
    "errorCode": "TARGET_PRODUCTS_NOT_EMPTY",
    "errorMessage": "Target store products should be empty"
}
```

#### Error messages

| AUTH\_APP\_DOESNT\_EXIST                          | Application does not exist                                                                                                   |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| TARGET\_CATEGORIES\_LIMIT                         | Target store categories limit will be exceeded                                                                               |
| TARGET\_PRODUCTS\_LIMIT                           | Target store products limit will be exceeded                                                                                 |
| TARGET\_DESTINATION\_ZONES\_LIMIT                 | Target store destination zones count will be exceeded                                                                        |
| UNKNOWN\_IMPORT\_FAILED\_TO\_START                | Failed to start import                                                                                                       |
| SOURCE\_NOT\_FOUND                                | Store #$sourceStoreId not found                                                                                              |
| UNKNOWN\_INTERNAL\_ERROR                          | Internal error                                                                                                               |
| SOURCE\_NOT\_RESPONDING                           | Source store failed to respond                                                                                               |
| TARGET\_NOT\_ALLOWED\_TO\_CLONE                   | Target store is not allowed to clone                                                                                         |
| TARGET\_NOT\_FOUND                                | Store #$targetStoreId not found                                                                                              |
| SOURCE\_NOT\_RESPONDING                           | Target store failed to respond                                                                                               |
| TARGET\_CATEGORIES\_NOT\_EMPTY                    | Target store categories should be empty                                                                                      |
| TARGET\_PRODUCT\_TYPES\_NOT\_EMPTY                | Target store product types should be empty                                                                                   |
| TARGET\_PRODUCTS\_NOT\_EMPTY                      | Target store products should be empty                                                                                        |
| TARGET\_ALREADY\_USED\_IN\_ANOTHER\_CLONE\_TICKET | Not allowed to clone to #99928003 while previous clone is still in progress with ticket 4a096838-0272-46ae-9c83-35242215161b |

### Step 2. Check status and get results — GET /stores/clone

Depending on the size of the source store, cloning will take from 1 to 15 minutes. To check the progress of the task, you can use the API endpoint described below.

#### Endpoint

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/stores/clone`

#### Query Params

* `ticket` - cloning task ID received at the first step

#### Headers

* `X-Ecwid-App-Client-Id` - _client\_id_ ID of your Ecwid application (provided by the Ecwid team).
* `X-Ecwid-App-Secret-Key` - _client\_secret_ of your Ecwid application.

#### Response

In response, Ecwid will tell the status of your task and provide additional details if the task is completed.

Fields in response:

* `status` identifies the current status of the task. Supported values:
  * `QUEUED` - The task is in the queue. Ecwid will soon start working on it. Check again later.
  * `IN_PROGRESS`- Data is being copied. Check again later.
  * `COMPLETED`- The data has been successfully copied to the target store.
  * `FAILED` - Something went wrong. See the errorMessage field for the details.
* `errorMessage` - If copying of data is unsuccessful, this field in response will contain an error message
* `clonedEntitiesMapping` - If cloning is completed, this field will show which products/categories in the source store correspond to the products/categories in the target store. You may want to use this field if you need to map direct links to the products or categories in the target store to those in the source store.

#### **Response examples**

```json
{
    "status": "IN\_PROGRESS"
}
```

```json
{
    "status": "COMPLETED",
    "clonedEntitiesMapping": {
        "products": {
            "12345": "54321", // old product ID: new product ID
            "67890": "09876" },
        "categories": {
            "12345": "54321", // old category ID: new category ID
            "67890": "09876"
        }
    }
}
```

### Cloning Instant Site

If you are using an Instant Site, you can also clone the contents and design settings of one site to another with an API call. API Reference: [clone-instant-site.md](../rest-api/instant-site/clone-instant-site.md "mention")
