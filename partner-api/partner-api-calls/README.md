# Partner API calls

**Partner API** (also called Reseller API) is only available to Ecwid reseller partners. It allows managing partner channel settings and stores on this channel.

This API is unavailable to the store owners.

### **Creating new Ecwid account**

This method allows you to create a new Ecwid store with some default settings on your partner channel. It works with both APIv3 and APIv1, though APIv1 is no longer supported. So we recommend using APIv3.

You need a **master application** for your partner channel and its API keys to use this request. If you don't have one yet, please contact your [partner manager](mailto:partneraccount@ecwid.com).

#### **Creating stores using API v3**

<mark style="color:blue;">`POST`</mark> `https://app.ecwid.com/api/v3/stores?returnApiToken={true/false}`

**Headers**

Both headers are _required_:

`X-Ecwid-App-Client-Id` - accepts client\_id of your master app\
`X-Ecwid-App-Secret-Key` - accepts client\_secret of your master app

**Request body**

The request body is JSON-formatted. It contains the `merchant` object with two fields inside (both are _required_):

| Field | Type   | Description          |
| ----- | ------ | -------------------- |
| email | string | Store owner’s email. |
| name  | string | Store owner’s name.  |

**Query parameters**

Set `returnApiToken` to `true` to receive an **access token** in the response alongside the Store ID (`id`). Having both, use API calls to manage store data.

Request example in HTTP and PHP:

```http
POST /api/v3/stores?returnApiToken=true HTTP/1.1
Host: app.ecwid.com
X-Ecwid-App-Client-Id: client_id
X-Ecwid-App-Secret-Key: client_secret
Content-Type: application/json

{
    "merchant": {
        "email": "example@example.com",
        "name": "John Doe"
    }
}
```

```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://app.ecwid.com/api/v3/stores?returnApiToken=true',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "merchant": {
        "email": "example@example.com",
        "name": "John Doe"
    }
}',
  CURLOPT_HTTPHEADER => array(
    'X-Ecwid-App-Client-Id: client_id',
    'X-Ecwid-App-Secret-Key: client_secret',
    'Content-Type: application/json',
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

?>
```

When creating a new store you can send multiple optional parameters to pre-configure the store. Please refer to this documentation for details: [Create store](create-store.md)

If you need to check if there is a store registered with the specified email, please use the following GET request:

<mark style="color:green;">`GET`</mark> `https://app.ecwid.com/api/v3/stores?email={email}`

**Headers**

Both headers are **required**:

`X-Ecwid-App-Client-Id` - to pass the ClientId\
`X-Ecwid-App-Secret-Key` - to pass the SecretKey

You should receive a 404 error, meaning there are no registered stores for this email. Please refer to the endpoint documentation for details: [Get store](get-store.md)

#### Creating stores using API v1

To create new Ecwid account just make a POST request to this URL: [https://my.ecwid.com/resellerapi/v1/register?register=y](http://www.google.com/url?q=https%3A%2F%2Fmy.ecwid.com%2Fresellerapi%2Fv1%2Fregister%3Fregister%3Dy\&sa=D\&sntz=1\&usg=AFQjCNHuOiRV3_J264Z-ThIMjYB7RXC6rA)

with these parameters:

\- **email**: store email, will be used as a login

\- **password**

\- **name**: Owner full name

\- **key**: API key

\- **plan:** internal name of the active partner plan to create the initial subscription for the store

\- **billing** (optional): set billing period for the account subscription. Possible values: _monthly,_ _annual_. If parameter is not set then _monthly_ value is used by default.

**- is\_trial** (optional): enables trial period for the store. Possible values: _false, true_.

Type of value should be **string (mandatory)**. Use this parameter to subscribe store to the trial version of paid plan. Number of days in trial period is set individually for every partner’s plan. If parameter is not set then _false_ value is used by default. Ecwid will not bill partner for the duration of free trial. After free trial expires partner will be billed according to selected plan rates. If customer did not subscribe for the services partner must suspend/delete account at the end of free trial period to avoid charges for this account.

\- **ip** (optional): IP address of owner. It will be used to detect owner’s location and automatically configuring store defaults (including time zone and default language) for that location. If you don’t know IP but know the country of the owner, just specify any IP belonging to the country to correctly pre-configure the store defaults.

**- timezone** (optional) Time zone of the store. (e.g. America/New\_York, Europe/London, Asia/Tokyo, Africa/Johannesburg see timezones in Ecwid backend for the full list).\
&#xNAN;**- defaultlanguage** (optional) Storefront default language. Two letter language code (e.g. en, fr, exceptions: es\_419, pt\_BR)

\- **profile\_id** (optional) assign a new store to the existing profile ID in Ecwid (see Profile-based Ecwid SSO for resellers for more details)

\- **returnProfileId** (optional) if set to 'true' profile ID will be returned in response in addition to the store ID. The profile ID format is a string starting with a 'p' and following with numbers. Example: p987654321

\- **external\_account\_id** (optional): ID of the external account (R-Series) connected to the created store

\- **Accept-Language** HTTP header can be used as usual to specify the store’s language. If missing, English language is used.

If a new account/store is created successfully, Ecwid will return the 200 OK HTTP status and this code:

```
<?xml version="1.0" encoding="UTF-8"?><ownerid>OWNERID</ownerid>
```

where OWNERID is an ID you should use in the widgets.

If Ecwid already has a store with the same email, the 409 status will be returned (in this case please use the _profile\_id_ parameter to create a new store).

If the e-mail isn't valid: 400

If API key isn't valid: 403

#### **Example in Java**

The following example demonstrates store creation in Java programming language. The following libraries are required to run the example:\
[Commons HttpClient 3.1](http://hc.apache.org/httpclient-3.x/), [Commons Codec](http://commons.apache.org/codec/), [Dom4j ](http://dom4j.sourceforge.net/)for parsing the response.

```java
import org.apache.commons.httpclient.*;
import org.apache.commons.httpclient.methods.*;
import org.apache.commons.httpclient.methods.multipart.*;
import org.apache.commons.httpclient.params.*;
import org.dom4j.Document;
import org.dom4j.io.SAXReader;

/**
 * Example Java code for creating a store using reseller API.
 */
public class TestClient {
    public static void main(String[] args) throws Exception {
        HttpClient client = new HttpClient();
        PostMethod post = new PostMethod("https://my.ecwid.com/resellerapi/v1/register?register=y");
        Part[] parts = {
                new StringPart("email", "test@example.com"),
                new StringPart("name", "Tester Tester"),
                new StringPart("password", "tester"),
                new StringPart("key", "12345"),
                new StringPart("plan", "ECWID_FREE"),
                };
        HttpMethodParams params = new HttpMethodParams();
        post.setRequestEntity(new MultipartRequestEntity(parts, params));

        if (client.executeMethod(post) != 200) {
            System.err.println("Error creating store: " + post.getStatusLine());
            return;
        }
        
        SAXReader reader = new SAXReader();
        Document doc = reader.read(post.getResponseBodyAsStream());
        int ownerid = Integer.parseInt(doc.getRootElement().getText());

        System.out.println("Successfully created: "+ownerid);
    }
}
```

### **Changing the account subscription**

You can change the account subscription for the account previously created by you with the help of **/resellerapi/v1/register** API call (see above). Changing the subscription will stop the current subscription and create a new one for the plan provided.

To change the plan make a POST request to this URL:

[https://my.ecwid.com/resellerapi/v1/subscribe](https://my.ecwid.com/resellerapi/v1/subscribe)

with the following parameters:

* **ownerid**: the Ecwid store ID, as an integer number
* **key**: your reseller API key previously used to create the account
* **plan**: the internal name of the active partner plan to create the initial subscription for the store
* **billing** (optional): set billing period for the account subscription. Possible values: _monthly,_ _annual_. If parameter is not set then _monthly_ value is used by default.

To unsubscribe from the current plan to the default one make a POST request to this URL:

[https://my.ecwid.com/resellerapi/v1/unsubscribe](https://my.ecwid.com/resellerapi/v1/unsubscribe)

with these parameters:

* **ownerid**: the Ecwid store ID, as an integer number
* **key**: your reseller API key previously used to create the account

This will stop your current subscription for the account and bring it back to the free plan, defined for the partner. The same result can be achieved by calling **/subscribe** and specifying your default plan name in the **plan** parameter.

If the request succeeds, the response 200 OK is returned, and the new expiration date is provided in the following XML format:

```
<subscribe-response>
<expirationDate>2012-05-20T06:44:53.627-04:00</expirationDate>
</subscribe-response>
```

If the new subscription has no expiration date, the empty xml is returned:

```
<subscribe-response/>
```

If the request fails, the response will contain the reason for the failure, for example:

```
HTTP ERROR 400

Problem accessing /400. Reason:

Plan 'TEST' not found for partner TestPartner
```

### **Suspending/resuming a user account**

You can suspend or resume a user account you have previously created with the **/resellerapi/v1/register** API call (see above). Suspending a user account prevents the storefront from showing any products or creating orders. Suspended accounts allow users to use their Control Panel though.

To suspend, make a POST HTTP request to the following URL:

[https://my.ecwid.com/resellerapi/v1/suspend](https://my.ecwid.com/resellerapi/v1/suspend)

To resume a previously suspended account, make the following POST HTTP request:

[https://my.ecwid.com/resellerapi/v1/resume](https://my.ecwid.com/resellerapi/v1/resume)

The parameters for both calls are the following:

* **ownerid** - the Ecwid store ID, as an integer number
* **key** - your reseller API key which was used to create the account

On success, both calls return HTTP status 200. Suspending an already suspended account and resuming an already active account makes no effect and returns status code 200.

### **Deleting a user account**

If you want to delete an account, you should make a POST HTTP request to the following URL:

[https://my.ecwid.com/resellerapi/v1/delete](https://my.ecwid.com/resellerapi/v1/delete)

The parameters for this call are the following:

* **ownerid** - the Ecwid store ID you want to delete
* **key** - your reseller API key

On success, you will see HTTP status 200. If you cannot delete an account (e.g. it wasn't created by you), the 403 HTTP error will be returned.

Important notice: deleting account does not remove its billing records. At the end of the billing cycle you will be invoiced for the period that account was active.

### **Getting info about the store**

If you want to get info about one of partner’s stores you should make a POST HTTP request to the following URL:

[https://my.ecwid.com/resellerapi/v1/stores](https://my.ecwid.com/resellerapi/v1/stores)

The parameters for this call are the following:

* **store.id** - the Ecwid store ID information you want to get. **store.ids** for multiple stores
* **key** - your reseller API key

On success, it will return HTTP status 200 and a small XML document containing basic information about the store and its subscription and billing.

### **Checking a user account status**

You can query status information on an account created previously by the **/resellerapi/v1/register** API call (see above). Make a POST HTTP request to the following URL:

[https://my.ecwid.com/resellerapi/v1/status](https://my.ecwid.com/resellerapi/v1/status)

The parameters are:

* **ownerid** - the Ecwid store ID, as an integer number
* **key** - your reseller API key which was used to create the account

On success, the call returns HTTP status 200 and the XML listing apps installed, information about the store subscription and billing, plan features enabled/disabled, shipping and payment configuration, tax settings and zones:

* **ownerid** - echoes the ownerid in the request
* **profile\_id -** Ecwid profile ID associated with this store
* **suspended** - “true” if the store was suspended
* **closed** - “true” is the store was closed by the user
* **email** - the current email of the account
* **name** - the person name in the account profile
* **traffic** - amount of web traffic consumed by the store since the start of the month
* **storage** - amount of billable storage occupied by the store, including store images and files.
* **shippingAndTaxSettings** - current zones, shipping and tax settings
* **account-type** - information about the subscription. The most useful tag there is subscription/originalProduct, which contains the current user’s plan.
* **carrier-settings** - (deprecated)
* **paymentmethods** - payment method list
* **total** - total of all orders in the store currency, except unfinished orders.
* **currency** - store currency ISO code
* **productCount** - product count
* **categoryCount** - category count
* **source** - value of _source_ parameter that was defined during account creation. If not defined the tag is missing

If the store with such ID does not exist, the call returns HTTP status 404.

If the store does not belong to your API key, the call returns HTTP status 403.

### **How to clone a store using the Ecwid Clone Store API**

The Ecwid Partner APIs allows an Ecwid reseller to create and manage accounts (stores) in Ecwid. In some cases, it may be convenient to have a single "template" store and clone it to create new stores — to make it easier pre-filling new stores with products, settings etc. The Ecwid Clone Store API can be used to do that.

Please refer to this documentation for details: [cloning-api.md](../cloning-api.md "mention")

### **Getting a list of all stores that are registered for the given partner**

To retrieve a list of your customers’ stores, make a POST request to the following endpoint URL: [https://app.ecwid.com/resellerapi/v1/stores](https://app.ecwid.com/resellerapi/v1/stores)

Include the following parameters:

* **date.from** Stores created _after_ the given date/time will be returned. The date/time is given either as a UNIX timestamp or a ‘YYYY-MM-DD’ string.
* **store.id** (optional). If specified, select a store with the given ID. **store.ids** for multiple stores
* **url.substring** (optional). If specified, limits stores only to those having certain substring in their URL.
* **email.substring** (optional) If specified, limits stores only to those having certain substring in their email.
* **date.to** (optional). If specified, limits stores to those created _before_ the given date/time. The date/time is given either as a UNIX timestamp or a ‘YYYY-MM-DD’ string.
* **timezone** (optional, default is ‘GMT’). The name if the timezone used to parse date.from and date.to fields.
* **suspended** (optional). If specified, lists only stores with the given “suspended” status. Possible values are: “y”, “yes”, “1”, “true”, “t”, “n”, “no”, “0”, “false”, “f”.
* **order** (optional, defaults to “id"). Specifies criteria used to sort stores. One of “id”, “email”, “url”, “traffic”, “storage”, ”date”, “id\_desc”, “email\_desc”, “url\_desc”, “traffic\_desc”, “storage\_desc”, ”date\_desc”.
* **key**. Your partner API key.
* **offset** (optional, default is "0"). Starting offset of the result window. Used to create pagination.
* **limit** (options, defaults to “20"). Number of stores to return, an integer value in the range \[0; 100].

On success, returns store list in the following format:

```xml
<storeList>
 <stores>
   <id>STORE ID</id>
   <channelId>PARTNER ID</channelId>
   <name>Store name</name>
   <nick>Store owner's nickname</nick>
   <email>Store owner's email</email>
   <url>Store URL</url>
   <planName>Name of partner plan</planName>
   <planChangeableByReseller>either 'true' or 'false'</planChangeablebyReseller>
   <planExpiration>Plan expiration date</planExpiration>
   <suspended>'Suspended' status, either 'true' or 'false'</suspended>
   <test>’true’ for test accounts and ‘false’ for others</test>
   <trial>’true’ for trial subscriptions and ‘false’ for life</test>
   <traffic>Traffic consumed since start of the month, bytes</traffic>
   <storage>Storage consumed by the store data, bytes</storage>
   <registered>Store registration date</registered>
 </stores>
...more store data...

 <total>TOTAL NUMBER OF STORES MATCHING CRITERIA</total>
</storeList>
```

On error, returns one of the following HTTP status:

* **403** - wrong API key
* **412** - wrong parameter format
* **500** - internal error

### **Getting the list of partner plans, available for subscription**

You can get the list of active partner plans, available for subscription. To get them make a POST request to this URL:

[https://my.ecwid.com/resellerapi/v1/plans?key=](https://my.ecwid.com/resellerapi/v1/plans?key=)

If the request succeeds, the response code 200 is returned, and the response body will contain the list of plans in XML format:

```xml
<planList>
    <plans>
        <active>true</active>
        <canUserCancel>true</canUserCancel>
        <channelId>TestPartner</channelId>
        <ecwidBilling>true</ecwidBilling>
        <id>3</id>
        <maxCategoryCount>1500</maxCategoryCount>
        <maxProductCount>30000</maxProductCount>
        <monthlyPrice>17.0</monthlyPrice>
        <name>TEST_PLAN_NAME</name>
        <premiumFeatures>true</premiumFeatures>
        <sendCancellationEmailToBillingManager>true</sendCancellationEmailToBillingManager>
        <suspendWhenExpired>false</suspendWhenExpired>
        <title>Test Plan Title</title>
        <trialDays>14</trialDays>
    </plans>
...
</planList>
```

If the request fails, the reason for the failure is returned.

### **Single sign-on (SSO) using Partner Key mechanism**

Please note that [Single Sign On to control panel using the Developer API](./#single-sign-on-to-the-control-panel-using-the-developer-api-and-store-access-tokens) is now available and has more functionality. We recommend switching to the Developer API SSO.

In order to login a user into Ecwid store control panel, the control panel should be opened through the following URL:

`https://my.ecwid.com/cp/partner-login?ownerid=[ID]&t=[TIMESTAMP]&login_sha256token=[TOKEN]&place=[PAGE_HASH]&logout_url=[LOGOUT_URL]&upgrade_url=[UPGRADE_URL]&lang=[LANGUAGE_CODE]&inline&profile_id=[PROFILE_ID]`

where:

* `my.ecwid.com` domain may be different if your Ecwid admin URL uses a custom domain.
* `ID` - Store ID, e.g. `1003`
* `PROFILE_ID` - Login to a specified profile ID (see Profile-based Ecwid SSO for resellers for more details), optional param.
* `TIMESTAMP` - UNIX timestamp of a token creation time. Time should be in UTC and timestamp should be in seconds.
* `TOKEN` - the token itself that is a _SHA256_ hash, created by concatenation of the following parameters: `timestamp` + `store_id` + `channel_id` + `partner_api_key`. The token must be generated in **lowercase**.

Token generation params:

* `PAGE_HASH` - (optional) the hash part of control panel page’s URL-address that should be opened after sign-on (Dashboard page if was not defined). If page hash is using additional parameters, they should also be used in this request. E.g. place=order:id=V8SQC
* `LOGOUT_URL` - Ecwid will redirect a user to this URL if his/her session is expired. Usually it is URL of a partner’s control panel or “log in” page.
* `UPGRADE_URL` - allows setting an upgrade URL for every partner’s store. Ecwid will redirect a user to this URL if he/she clicks any upgrade button within store Control panel (e.g. [http://take.ms/l7qnX](http://take.ms/l7qnX) ). For more information on upgrade URLs format refer to Define upgrade URLs
* `LANGUAGE_CODE` - a two letter language code for the store control panel
* `inline` - (optional) displays control panel in iframe friendly manner with header and footer removed

The `UPGRADE_URL` parameter works in the following way:

* When passing a value via `UPGRADE_URL` - that value is assigned as Upgrade URL for that particular store.
* When passing empty value via `UPGRADE_URL` - a current Upgrade URL for that store is reset. In this case, one of two options is possible:

1. If `Channel_Upgrade_URL` (URL that is set for a partner on the Ecwid side) is set, Ecwid will redirect a user to that `Channel_Upgrade_URL`.
2. If `Channel_Upgrade_URL` is not set, a user will not be redirected anywhere and just see a popup with an explanatory text: [screenshot example](http://take.ms/2ymqu)

* If `UPGRADE_URL` is not passed at all - a current Upgrade URL (that was set earlier) is used.
* `send_postmessage_on_upgrade_button_click` Enables sending postmessage when upgrading. Possible values: false, true. Optional param.

Ecwid admin is often embedded in a partner service in a form of an iframe. In this case, when a merchant clicks upgrade button, Ecwid can send a postmessage to the "parent" window and then the partner admin interface handles it accordingly. For example, the partner can show a popup where the merchant chooses a plan and then is directed to finish the upgrading process [http://take.ms/aZrjQ](http://take.ms/aZrjQ).

Please note that when both `upgrade_url` and `send_postmessage_on_upgrade_button_click` parameters are passed in the SSO URL simultaneously then postmessages only will be sent.

When clicking **Upgrade** buttons, Ecwid sends `postmessage` in the following format:

```
{
  event: 'upgrade-link-click',
  feature: 'coupons',
  plan: 'PARTNER_PLAN_NAME'
}
```

where

`feature` - name of a feature an upgrade button was clicked for;

`plan` - name of a plan where the feature is available.

Please note that the option to send upgrade `postmessage` can be enabled or disabled on the partner channel level. Contact your partner manager to enable or disable it.

Request limitations:

* A token is valid for 5 minutes from the time specified in the timestamp.
* The URL provided works with HTTPS only, not HTTP.
* SSO session will expire in 27 hours after the last active RPC request from the control panel. So if the control panel is open in your browser it will keep sending heartbeats and the session will not expire.

PHP code sample:

```php
<?php
$time = time();
$store_id = STORE-ID;
$channel_id = "YOUR-CHANNEL-ID";
$apikey = "YOUR-API-KEY";
$token = $time . $store_id . $channel_id . $apikey;
$token = sha256($token);

echo "https://my.ecwid.com/cp/partner-login?ownerid=$store_id&t=$time&login_sha256token=$token&place=order&logout_url=http://example.com&upgrade_url=http://billing.com" . "\n";
?>
```

### **Embedding Ecwid Control Panel**

For seamless customer experience it is possible to embed Ecwid control panel into a third party product using seamless iframe. Please make sure that you are using the Ecwid SSO for seamless customer experience. The iframe will automatically adjust its height depending on the content of control panel page. Below is an example of simple HTML page with embedded Ecwid control panel:

```javascript
<html>
  <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
    </head>
  
<body>

<h1>Sample of Ecwid control panel embedding</h1>


<script type='text/javascript'>//<![CDATA[ 
window.onload=function(){
 // Create IE + others compatible event handler
    var eventMethod = window.addEventListener ? "addEventListener" : "attachEvent";
    var eventer = window[eventMethod];
    var messageEvent = eventMethod == "attachEvent" ? "onmessage" : "message";
 
    // Listen to message from child window
    eventer(messageEvent,function(e) {
        $('#ecwid-frame').css('height', e.data.height + 'px');
    },false);
 
    $(document).ready(function(){
              $('#ecwid-frame').css('height', '700px');
 
        $('#ecwid-frame').attr('src', 'https://my.ecwid.com/cp/CP.html?inline');
    });
 
}//]]>  
 
</script>
 
 
      <div id="wrap">
        <iframe seamless id="ecwid-frame" frameborder="0" width="100%" height="700" scrolling="no"></iframe>
    </div>

  </body>
</html>
```

### **Implementing Custom Save Button**

You can natively implement buttons in your product to save changes in the Ecwid control panel. This is useful if you display an Ecwid control panel in a webview of a mobile app or want to have your original controls to save changes.

_Please note that Save page functions described below won’t work when the control panel is embedded in an iframe._

To hide Ecwid save button use parameter: _hide\_save\_button=true_ when embedding control panel _e.g._ [_https://my.ecwid.com/cp/CP.html?inline\&hide\_save\_button=true_](https://my.ecwid.com/cp/CP.html?inline\&hide_save_button=true)

To control saving data in Ecwid control panel please use the following Javascript API functions:

_EcwidControlPanel.onSavePageDataRequired(callback)_ - Ecwid will fire this callback when it detects that data was changed and requires saving.

_EcwidControlPanel.savePageData()_ - save unsaved data in Ecwid control panel.

_EcwidControlPanel.onSavePageData(callback)_ - callback is fired when data is saved.\
&#xNAN;_&#x45;cwidControlPanel.revertUnsavedPageData()_ - discard unsaved data in Ecwid control panel.\
&#xNAN;_&#x45;cwidControlPanel.onRevertUnsavedPageData(callback)_ - callback is fired when data is discarded.

**Note**: when customer leaves Ecwid control panel with unsaved changes it will display popup with warning to save changes even if save button is hidden.

### **Static Embedding of Ecwid Widget**

In some cases it is necessary to load Ecwid widgets simultaneously with loading of a web page. This way of loading is called Static loading. For example, sitebuilders can load Ecwid widgets statically when customers publish their websites (with a store) live.

Please refer to the following articles to find [more information](https://support.ecwid.com/hc/en-us/articles/115004678945-Ecwid-for-any-website) regarding the Ecwid widgets including embed codes:

**\[IMPORTANT]:**

* **Use a correct domain in the script.js**

In the articles below the _ecwid.com_ is used in the script.js ([https://app.ecwid.com/script.js?...](https://app.ecwid.com/script.js?...))

Please note that this correct for partners who use ecwid.com as the domain for their store Control panel.

If another domain is set as the domain for partner stores Control panel, in this case a partner should use that custom domain in the script.js.

Please contact with Ecwid Partner team and clarify your domain for the store CP and other questions regarding the script.js if any.

* **Call the script.js only once!**

Please note that the script.js ([https://app.ecwid.com/script.js](https://app.ecwid.com/script.js)) should be called only once before loading of the widgets or simultaneously with loading of the first widget (but only once!).

### **Dynamic Embedding of Ecwid Widget**

In some cases it is necessary to dynamically create and destroy Ecwid widget within HTML page. This is useful for dynamic sitebuilders that switch to online store page without actually reloading page (e.g. making it visible). You should use window.ecwid\_dynamic\_widgets variable to enable dynamic widget creating in Ecwid. See the example below that shows how to create and destroy Ecwid widget through javascript functions.

Please note that this method allows to embed the **Product browser widget** only. If you need to embed other widgets dynamically, please, use the code for deferred widget initialization (next point).

Please note that this method is slower than direct embedding of Ecwid widget so you should use it only if you need dynamic widget creation.

```javascript
<div id="my-store-1003"></div>
<script>
window.ecwid_script_defer = true;
window.ecwid_dynamic_widgets = true;

   if (typeof Ecwid != 'undefined') Ecwid.destroy(); 
   window._xnext_initialization_scripts = [{
        widgetType: 'ProductBrowser',
        id: 'my-store-1003',
        arg: ["categoriesPerRow=3","views=grid(3,3) list(10) table(20)","categoryView=grid","searchView=list"]
      }];

  if (!document.getElementById('ecwid-script')) {
      var script = document.createElement('script');
      script.charset = 'utf-8';
      script.type = 'text/javascript';
      script.src = 'https://app.ecwid.com/script.js?1003';
      script.id = 'ecwid-script'
      document.body.appendChild(script);
    } else {
      ecwid_onBodyDone();
    }

</script>
```

### **Deferred Initialization of Ecwid Widget**

Sometime it is necessary to delay widget initialization while host page finish initialization procedures. This is useful when host site is built dynamically using libraries such as React js.

Use this integration code for deferred widget initialization:

```javascript
<div id="my-store-1003"></div>
<div id="productBrowser"></div>
<script>
window.ecwid_script_defer = true;
var script = document.createElement('script');
script.charset = 'utf-8';
script.type = 'text/javascript';
script.src = 'https://app.ecwid.com/script.js?1003';
document.getElementById('my-store-1003').appendChild(script);
window._xnext_initialization_scripts = [
    { widgetType: 'ProductBrowser', id: 'productBrowser', arg: [
        '"categoriesPerRow=3","views=grid(4,4) list(10) table(20)","categoryView=grid","searchView=list","style=","responsive=yes","id=productBrowser"'
    ] }
];</script>
```

### **Improving SEO with Static Pages**

Ecwid widgets are indexed by Google. However Google is indexing HTML pages faster and deeper than dynamic Javascript widgets. So as a measure to improve indexing you can use [Static Store Pages API](../../rest-api/storefront-widget-details/static-store-pages/) to add indexable HTML content to your store.

This method will work only if your page with Ecwid widget is generated dynamically with a server side script e.g. Python, PHP, ASP etc. You need to add a piece of code to your page that fetches the HTML version of a store page and insert it into your page. Static Store Pages API also returns Meta tags and Open Graph tags it is highly recommended to insert them into your page as well.

![](https://files.readme.io/6199613-Aspose.Words.4a5514c5-c86a-4e64-82a1-c7d31db86adf.002.png)

You should do it dynamically each time the store page is loaded in the customer’s browser. Google bot will continue following links in the static page and will index the entire product catalog.

Store customers will be interacting with the dynamic Ecwid widget. To prevent customers from seeing a static copy of the store page you need to add a Javascript code that will hide the static part.

You can use the code example provided below for hiding static content:\
html\_selector - is a HTML selector of the static content.

```html
<script data-cfasync="false" data-no-optimize="1" type="text/javascript">
	function createClass(name,rules) {
		var style = document.createElement('style');
		style.type = 'text/css';
		document.getElementsByTagName('head')[0].appendChild(style);
		if(!(style.sheet||{}).insertRule)
			(style.styleSheet || style.sheet).addRule(name, rules);
		else
			style.sheet.insertRule(name+'{'+rules+'}',0);
	}
	createClass('#html_selector', 'display:none;');
</script>
<div id=’#html_selector’> 
	Static HTML code here
</div>
```

Sample code in PHP for extracting productid and categoryid from SEO friendly URL

```php
<?
$pattern =  '!.*-(p|c)([0-9]+)(\/.*|\?.*)?$!';
if( preg_match( $pattern, $current_url, $matches ) ) {
	return array();
}
$modes = array(
	'p' => 'product',
	'c' => 'category'
);
return array( 'mode' => $modes[$matches[1]], 'id' => $matches[2] );
?>
```

Returned values:

mode = product - this is a product page

mode = category - this is a category page

mode is empty - this is a home page

id - productid or categoryid. Use it when calling the Static Pages API.

We recommend to cache static content on your side to provide better site performance. You should use the [Store Changes Stats API](../../rest-api/store-profile/store-reports/get-latest-store-update-stats.md) endpoint to determine when the cache becomes obsolete. _productsUpdated and categoriesUpdated_ fields provide an indication when it is necessary to refresh cache.

### **Centering popups in iframe (storefronts and stores’ control panel)**

Ecwid can be embedded to a website in many ways. Sometimes a storefront can be inserted in an iframe container due to the limitations of a platform. To make sure that all popup windows such as customer account login popup are displayed in the center of an iframe, use the example code below **in a main frame of your page.** The example can be used for the storefront and the stores’ control panel.

Example of centering popups:

```javascript
<script src='https://d1e443hvef5jf2.cloudfront.net/static/iframeintegration.js'></script>
<script type='text/javascript'>

window.addEventListener('load',  function(e) {
  setupEcwidPopupCentering('#myframe');
});

</script>
```

setupEcwidPopupCentering() function accepts one argument, which is the ID of an iframe element, where Ecwid storefront is loaded. In order to work, setupEcwidPopupCentering() function needs to have iframeintegration.js file loaded for that frame.

### **Tracking customer navigation in embedded control panel**

Each time customer opens new page in embedded Ecwid control panel it sends following postmessage to the parent window:

```json
{
    'action': 'pageLoad',
    'data': {
      'page': {
          'title': 'Catalog',
          'path': 'products',
        }
    },
    'height': 1200
}
```

This functionality is useful when creating deep product integration with Ecwid. For example change content of parent window depending on the page opened in Ecwid control panel.

### **Color Management for Ecwid Widget (Chameleon)**

When embedding Ecwid widget into a website there is an easy way to make sure that Ecwid colors matching site colors. There are two options to define colors for Ecwid stores: automatic and manual.

* **Automatic color detection**

You should add the following data structure before Ecwid widget integration:

```javascript
<div><script type="text/javascript">
window.ec = {
config: {
chameleon: {
colors: 'auto'
}
}
}
```

Ecwid will change its main colors depending on website colors and will automatically calculate all intermediate colors in the interface to make sure that all elements are legible and have good contrast.

Please note that for some website themes the automatic mechanism may detect colors not ideally.

We recommend checking how colors were detected.

Please note that if Ecwid widgets are embedded into an iframe, the automatic mechanism will not work. In this case additional actions are required, please get in touch with Ecwid Bizdev team for more information on this.

In cases when the automatic mechanism cannot be used, please use the manual mechanism:

* **Manual color defining**

Allows to define colors for Ecwid stores manually. Example of data structure that should be added before Ecwid widget integration:

```css
window.ec ={

config:{

chameleon:{

'color-link': '#ffffff' ,

'color-button': '#00ff00',

'color-foreground': '#a1d3de' ,

//Set widget background transparency through alpha channel

'color-background': 'rgba(29,29,29,0)' ,

'color-price': '#df0739'

}

}

}
```

**Turn off automatic background color in gallery**

When the automatic Ecwid background color in the gallery does not work well, please use the parameter below to switch off automatic background color and use the color set manually.

ec.config.chameleon.colors.gallery.use\_exact\_colors = true

### **Accessing Ecwid Developer API**

Ecwid provides many REST API calls for managing data in Ecwid stores.

If certain permissions are granted partner can access Developer API on behalf of customers. This is useful for building various types of integrations with third party products, consolidating customer data, building reports etc.

To access Developer API for a store it is necessary to retrieve access token that is unique for every store. Normally receiving access token requires manual permission granted by the store owner. However, for Ecwid partners, there is an alternative flow that allows generating access token without explicit confirmation from your users.

Before accessing the Developer API, you must ensure that this functionality is set and enabled for your partner account. You will need the following access credentials that should be provided to you by Ecwid: **client\_id** and **client\_secret.** If you do not have this data please get in touch with Ecwid representative.

**Receiving access token (alternative flow for partners)**

To receive token for online store make a POST request to the following endpoint:

[**https://my.ecwid.com/api/oauth/token/{ownerid}**](https://my.ecwid.com/api/oauth/token/%7Bownerid%7D) and send the following parameters:

| client\_id     | required | Application ID              |
| -------------- | -------- | --------------------------- |
| client\_secret | required | Application secret key      |
| grant\_type    | required | Must be authorization\_code |

{ownerid} in the endpoint path should be replaced with the Store ID number.

Please make sure that the correct domain **my.ecwid.com** is used to make POST request!

Ecwid responds with a JSON-formatted data containing the access token and additional information. Please refer to[ ](http://api.ecwid.com/%23get-access-token)this [reference](broken-reference) to parse the response.

Important: an access token does not expire. So you will need to retrieve the token only once per store and then use it as many times as you need. In other words, you should save the token in your system and use it for all API calls instead of generating it every time you access the store over API.

After receiving access token partner should use it to access REST API as described in the API documentation above.

### **Using Ecwid Developer API**

In case of error, Ecwid responds with an error HTTP status code and, optionally, JSON-formatted body containing error description.

There are tables with detailed descriptions of the returned HTTP codes in each corresponding HTTP request’s section.

Also, there are several general errors related to requests of various types:\
`402 The store is suspended` error is returned when the request is made to the suspended store.\
`403 Token doesn't exist` error is returned when the request is made using the incorrect or invalid token.

#### **Single Sign On to the control panel using the Developer API and store access tokens**

Use the following endpoint to display Ecwid control panel and automatically log in customer into it:

`my.{domain}/api/v3/{ownerId}/sso?token={token}&timestamp={timestamp}&signature={signature}`&#x20;

Make sure SSO access to Control Panel is available only to authorized users. SSO URL contains a REST API token allowing access to store data. Therefore, SSO requests shouldn't be available to users not logged in on your side.

Parameters:

* **domain** - if your instance of Ecwid is located on custom domain please insert it here. Otherwise domain should be ecwid.com
* **ownerId** - unique numeric identifier of the store. Also known as StoreID
* **token** - ApiToken that was generated during store creation. Also could be received via oAuth endpoint or via Partner API
* **timestamp** - UNIX timestamp for current date and time e.g. 1492688357
* **signature** - is sha256 hash from concatenation of ownerid, token, timestamp and app\_secret without spaces between them: sha256(ownerid+token+timestamp+app\_secret). Signature should be generated without sha256 secret key. _Please generate the signature in lowercase (mandatory!)_
* **place, inline, logout\_url, upgrade\_url, send\_postmessage\_on\_upgrade\_button\_click** - see parameter description in Single sign-on (SSO) using token mechanism
* **disable\_scroll\_on\_page\_switch**=true - (optional) disables automatic scrolling to the top after a page switch
* **hide\_visit\_storefront\_menu**=true - (optional) hides the Visit storefront link [http://take.ms/ztmFq](http://take.ms/ztmFq)
* **hide\_help\_menu**=true - (optional) hides the Help menu [http://take.ms/lhoJD](http://take.ms/lhoJD). The Help menu is usually hidden for White-label partners.
* **hide\_profile\_menu**=true - (optional) hides the Profile menu (round icon with pop-up menu). [Screenshot](http://take.ms/PuAbJ)
* **hide\_profile\_header**=true - (optional) hides all three elements: Visit storefront, Help menu, Profile menu.
* **hide\_page\_header**=true - (optional) hides pages’ headers (text).
* **hide\_footer**=true - (optional) hides the footer.
* **hide\_back\_button**=true - (optional) hides the Back button.
* **hide\_dashboard\_background\_image**=true - (optional) hides the background image in the new dashboard and replaces it with grey background.
* **hide\_staff\_accounts\_header\_menu**=true - (optional) hides “My stores” link in the dashboard header. “\*\*My stores” link allows opening admin panel of stores where a user is logged in when using the Staff accounts feature.
* **hide\_vertical\_navigation\_menu** - (optional) - hides main product navigation menu. This is useful when partner wants to implement navigation menu in host application outside iframe. Possible values: false, true. Ecwid will send post message _navigationMenuUpdated_ after initial load of control panel and each time when menu is changed. Host application where Ecwid is embedded should listen for this message and use its data to build menu.
* **session\_tag** - (optional) arbitrary string that identifies a session. Used for SSO session invalidation (logging out customer).

```json
{
   'action': 'navigationMenuUpdated',
   'data': {
     navigationMenuItems: [
       {
         'title': 'Catalog',
         'path': 'products',
         'items': {
           {
             'title': 'Products',
             'path': 'products'
           },
           {
             'title': 'Categories',
             'path': 'category:id=0&mode=edit'
           },
           {
             'title': 'Product Types',
             'path': 'product-classes'
           }
         }
       },
 
       {
         'title': 'Sales',
         'path': 'orders'
         ...
       },
 
       ...
     ]
   }
   'height': 1200 
}
```

If you need to use external menu outside the iframe you can use the following code to open necessary page in iframe without reloading it:

```javascript
 window.ecwidOpenAdminPage = function (place) {
       jQuery('#ecwid-frame')[0].contentWindow.postMessage(JSON.stringify({
            ecwidAppNs: "your-app-namespace",
            method: "openPage",
            data: place
       }), "*") 
}
```

You can populate "place" variable with necessary target e.g. orders, products, etc

If authorization is successful then customer will be redirected to control panel otherwise 403 error will be returned.

If you need to disable scrolling while navigating between pages in the admin panel, you will need to use the optional parameter `openWithoutScrolling`.

If the address of the needed page is without parameters, then you need to add `:openWithoutScrolling=true`. If there are any parameters, you need to add `&openWithoutScrolling=true`.

For example, to open the “Orders” page without scrolling while navigating between pages, you can use the following code:

```javascript
jQuery("#ecwid-frame")[0].contentWindow.postMessage(
  JSON.stringify({
    method: "openPage",
    data: "orders:openWithoutScrolling=true",
  }),
  "*"
);
```

To open the “Order Editor” page without scrolling while navigating between pages, you can use the following code:

```javascript
jQuery("#ecwid-frame")[0].contentWindow.postMessage(
  JSON.stringify({
    method: "openPage",
    data: "app:name=ecwid-edit-orders&openWithoutScrolling=true",
  }),
  "*"
);
```

#### **SSO session invalidation**

Use this call to invalidate the SSO session (log out customer).

When you log in a user via APIv3 SSO, make sure that you are sending an optional session\_tag string parameter.

When you need to log out a user, please do POST request to `https://app.ecwid.com/api/v3/{storeId}/sso-logout?token=token`

```json
Use this JSON as its body:

{
    "sessionTag": "SESSION-TAG-VALUE"
}
```

### **Product API extensions for partners**

Extensions list:

* Managing list of enabled payment processors
* Managing [storeURL](https://support.ecwid.com/hc/en-us/articles/360017059699-Configuring-general-settings-for-your-store#store-location--url-)

**Setting values in the store profile**

As a partner, you can set additional parameters that are unavailable to regular users using REST API /products.

To modify store profile you should use PUT HTTP request to the following endpoint URL:

`http://app.ecwid.com/api/v1/<ownerId>/profile?secure_auth_key=`

In the body of request you should add JSON document, which may contain the following fields:

* **enabledOnlineProcessors** - enabled online payment processors for given ownerId. Possible values are:
  * \[] - allow all processors;
  * \[“NONE”] - forbid all online payment processors;
  * \[“processor1”, “processor2”, “processor3”] - allow all offline payment processors and all listed online payment processors.

It is possible to turn on payment processors, that will be supported in future. For example, you can enable “amex” for all your clients in advance and as soon as it will be released, this payment will appear in all stores automatically.

* **storeUrl** - set store URL. Possible values are:
  * null - do not change store URL;
  * “” - reset store URL value;
  * new value of store URL. Must be valid URL beginning with “http://” or “https://”.

Response:

If storeUrl is not valid URL or does not start with “http://” or “https://”, server will respond with error 400 Bad Request.

If JSON with fields enableOnlineProcessors or storeUrl sent with customer API key, server will respond with error 403 Forbidden.

Examples of JSON document:

```json
{
	"enabledOnlineProcessors": [ "new1", "new2"],
“storeUrl”: “http://storename.com”
}
```

\- enables all offline payment processors, online processors “new1” and “new2”, when they will be added to Ecwid and sets store URL to “[http://storename.com](http://storename.com)”.

**Getting values through Product API**

You can also get information about extended fields of store profile us API. To do so make GET HTTP request to the following endpoint URL:

`http://app.ecwid.com/api/v1/<ownerId>/profile?secure_auth_key=`

Among all default fields, additional field **enabledOnlineProcessors** will be listed. Possible values are:

* \[] - allow all processors;
* \[“NONE”] - forbid all online payment processors;
* \[“processor1”, “processor2”, “processor3”] - allow all offline payment processors and all listed online payment processors.

Upon requesting Product API with customer API key or anonymously, field enabledOnlineProcessors will not be listed.

### **Setting language of control panel**

By default Control panel will automatically switch to the correct language depending on customer language setting in the web browser. However you can override this behaviour and display control panel in certain language. Use lang parameter to when when accessing control panel:

e.g. [https://my.ecwid.com/cp/?lang=es](https://my.ecwid.com/cp/?lang=es)

Use two letter language code to select necessary language:

| Language              | code   |
| --------------------- | ------ |
| French:               | fr     |
| German:               | de     |
| Italian:              | it     |
| Dutch:                | nl     |
| Spanish:              | es     |
| Brazilian Portuguese: | pt\_BR |
| Indonesian:           | id     |
| Czech:                | cs     |
| Hungarian:            | hu     |
| Turkish:              | tr     |
| Bulgarian:            | bg     |
| Norwegian:            | no     |
| Swedish:              | sv     |
| Danish:               | da     |
| Polish:               | pl     |
| Finnish:              | fi     |

Please contact your [Partner manager](mailto:partneraccount@ecwid.com) for more details.

### **Billing Rules**

To better understand Ecwid will bill you for the services, please refer [to this document](https://portal.ecwid.com/hubfs/Partner%20Program%20Docs/Partner%20Billing%20FAQ.pdf).

### **Trial plans in Ecwid**

Ecwid allows to create new stores subscribed to the trial version for the paid plan, if this functionality was enabled during partner creation. It is possible to define number of trial days for paid plan and the plan itself for which trial subscription will be available.

**\*Note:** Number of trial days and the trial subscription availability are defined by Ecwid and can’t be managed through Partner API.\*

**How to subscribe to trial plan?**

Subscription to trial plan can be done together with new account creation only. (See: Create new Ecwid account) There is no way to subscribe existing store to trial version of paid plan.

Among with general parameters required for the new account creation you will need to pass the following:

* **is\_trial = true** This parameter will mark the account as a “trial”
* **plan =** Name of the plan for trial subscription (Usually discussed in contract and can’t be changed afterwards).

**What is next?**

When the request on new trial account creation is received, Ecwid creates new account and subscribes it to the paid plan with the expiration date calculated as:

**date of subscription + number of trial days**

Our internal script will check all trial subscriptions periodically and switch them to “Live” mode automatically, when trial period is over. All trial subscriptions are converted to Live paid subscription automatically and you will be billed for them accordingly.

### **Define upgrade URLs**

There are lot of upgrade URLs in Ecwid interface they trigger upgrades when customer want to use certain functionality that is not available for the current plan. Normally they just lead to Ecwid plans page but partner can redefine them and point to alternative location e.g. to partner’s billing page where customer can manage their subscription.

This URL can be setup globally for all stores during initial deployment just specify it in partner questionnaire.\
You can also define Upgrade URL as parameter when doing SSO.

### **Profile-based Ecwid SSO**

#### **Definitions**

**Partner** — Ecwid's reseller partner who provides their customers with Ecwid stores.

**User** — Partner's customer (seller)

**Ecwid store** — an Ecwid store with unique 'store ID' property.

**Ecwid control panel** — a web page allowing the user to manage a particular Ecwid store.

**Ecwid profile ID** — a special unique property that identifies the owner of an Ecwid store. Each profile ID can be assigned to several stores meaning this person can open different Ecwid control panels under the same login session.

#### **Intro. What problem are we solving here?**

Ecwid Control Panel can be embedded into the partner product seamlessly. Some partners allow users to create several Ecwid stores under one partner account. For example, a user can have several sites created under their account on the partner side and they need a separate store added to each site. In this case, the partner may want to allow opening different Ecwid control panels in different browser tabs — e.g. to allow the user to manage each site and store in a separate tab.

Normally, Ecwid doesn't allow users to be logged in different accounts in the same browser — each new login will override the previous ones so that all opened control panels will display the same Ecwid account.

The doc below explains how to have several different Ecwid accounts opened in the same browser.

#### **Profile-based SSO API Basics**

The solution relies on a special internal property of Ecwid accounts — _'profile ID'_. Several Ecwid stores can be assigned to the same profile ID, which tells Ecwid those actually belong to the same person and can be opened in the same browser session with no need to log out and log in again.

Ecwid automatically generates and stores that profile ID when a new store is created. However, it's possible to specify the profile ID for a newly created store so that it's assigned to an existing profile ID.

When using the Ecwid SSO API, it's possible to pass the profile ID parameter to let Ecwid know the control panel is being opened under specific profile ID. If other stores under the same profile ID are opened in the same browser, they won't be logged out — everything will work well.

Below are the details on how to do that for new and existing customers.

#### **How to make it work for new users**

**Partner gets an Ecwid profile ID when creating first Ecwid store for the user**

When the partner creates the first Ecwid store for the user via the Ecwid Partner API (the _`/resellerapi/v1/register`_ endpoint), the partner should pass a special parameter _'returnProfileId=true'_ to the request to make Ecwid return the generated profile ID of that store. When the store is created, the corresponding profile ID will be returned in response in addition to the store ID. The profile ID format is a string starting with a 'p' and following with numbers. Example: _p987654321._

The partner should store that profile ID corresponding to the user on their side.

Request:

<mark style="color:blue;">`POST`</mark> `https://my.ecwid.com/resellerapi/v1/register?register=y&returnProfileId=true`

Response:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<store>
  <ownerid>12345</ownerid>
  <profileid>p987654321</profileid>
</store>
```

**Partner specifies the profile ID when creating new Ecwid stores for the existing user**

If the same user requests to create another Ecwid store (e.g. to add a store to their another site), the partner should pass the existing profile ID in the request query to the Ecwid Partner API. This will assign a new store to the same profile ID in Ecwid.

Request:

<mark style="color:blue;">`POST`</mark> `https://my.ecwid.com/resellerapi/v1/register?register=y&profile_id=p98765`

**Partner passes the profile ID parameter in SSO request when logging in the user to an Ecwid control panel**

When opening the Ecwid control panel using the Ecwid SSO API, partner should pass the profile\_id query parameter to make Ecwid log that user into the specific profile ID.

Request:

<mark style="color:green;">`GET`</mark> `https://my.ecwid.com/cp/partner-login?ownerid=[ID]&profile_id=p98765`

That's it. Several logins to Ecwid control panel with the same profile ID can work in the same browser without interrupting each other.

**Example**

Let's say a customer creates several sites in the partner product (e.g. sitebuilder) and adds a new store to each site.

1. `john@partner-sitebuilder.com` requests to add a store to their site A

* The partner checks if the user already has an Ecwid profile ID assigned. This is a new customer, so let's say there is no Ecwid profile ID on file.
* The partner uses the Ecwid Partner API to register a new store and specifies _'returnProfileId=true'_ in the request
* Ecwid returns the _store ID 123_ and the _profile ID p98765_ for the new store
* The partner saves the Ecwid profile ID in the user record to keep the link between `john@partner-sitebuilder.com` and Ecwid profile ID p98765 in the system.

2. `john@partner-sitebuilder.com` requests to add a store to their another site — site B

* The partner checks if the user already has an Ecwid profile ID assigned. This time, the Ecwid profile ID is there — it's _p98765_.
* The partner uses the Ecwid Partner API to register a new store and specifies \_'profile\_id=\_p98765 in the request
* Ecwid creates a new store and assigns it to the existing profile instead of generating a new profile. The response specifies the new _store ID 456._ Now, two stores in Ecwid are assigned to that profiel: store ID 123 and store ID 456.

3. `john@partner-sitebuilder.com` opens store control panels in the partner UI.

* The user manages the site A in one browser tab, and the site B in another browser tab
* To display the Ecwid control panel, the partner uses the Ecwid SSO API and passes the profile\_id parameter in request.
* The control panel A and the control panel B work simultaneously in different browser tabs.

#### **How to make it work for the existing users**

Partner's existing Ecwid stores were registered before the above mentioned API became available. All of those stores have different profile IDs assigned, even the stores of the same customer are separate. To make the new approach working for the old users, the partner needs to re-assign profile ID for those existing users who run several Ecwid stores.

Below is an instruction on how to do that for each particular user.

**Partner finds Ecwid stores belonging to the user and their profile IDs**

Partner should check the Ecwid stores belonging to a user and get their profile IDs. This can be done via the /status endpoint of the Partner API. The profile ID field will present in the XML response.

Request:

<mark style="color:blue;">`POST`</mark> `https://my.ecwid.com/resellerapi/v1/status`

Response (XML):

```xml
…
<profileid>p987654321</profileid>
…
```

**Partner assigns the same profile ID for all Ecwid stores belonging to the user**

Now the partner has a list of stores and profile IDs assigned to them. Partner should choose any of those profile IDs (e.g. the first one) and assign it to all stores of that customer, so that all stores have the same profile ID.

To change the profile ID of the store, the Ecwid's Partner API _/change-store-profile_ endpoint can be used. It requires the following parameters:

* key: the Partner reseller key
* ownerid: the store ID
* src\_profile: the old profile ID
* dst\_profile: the new profile ID

The partner will get 200 OK in response if the profile ID has re-assigned.

Request:

<mark style="color:blue;">`POST`</mark> `https://my.ecwid.com/resellerapi/v1/change-store-profile?ownerid=123&key=abc123&src_profile=p98765&dst_profile=p55555`

When it's done for all stores of the user, the new profile-based SSO API can be used as explained above.

#### **Note on security**

When the same profile ID is specified for several stores, it tells Ecwid that the user associated with that profile ID can manage all of those stores without extra login/password. So, partners should be careful when assigning profile ID to avoid unintentionally giving a wrong user access to the store data.
