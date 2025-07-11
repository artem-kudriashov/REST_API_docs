# Add SSO to the website

### Get started

You will need to go through these steps to get started with the SSO for your store:

* have [a registered application](https://developers.ecwid.com/register) for Ecwid with `create_customers` access scope
* install that app in your Ecwid store using instructions from Ecwid
* use application keys (`client_*`) for the SSO features

### Pass user data to Ecwid

To enable Storefront Single Sign-on (SSO) on merchant's website, you need to pass encrypted user information to Ecwid JavaScript API. The user data itself needs to be prepared and encrypted on the server. See [SSO Payload](ref:single-sign-on-sso#section-sso-payload) for the details.

Then, in the code of the store web page, you should send the encrypted user data to Ecwid. There are two ways you can do that:

1. Declaring a `ecwid_sso_profile` JS variable on the store web page containing the user information
2. Dynamically sending a user info to Ecwid by means of the `Ecwid.setSsoProfile()` JS API method

#### ecwid\_sso\_profile

You can inform Ecwid of the logged in user on your site in the `ecwid_sso_profile` JavaScript variable declared on the store pages. The `ecwid_sso_profile` variable can be declared anywhere in a web page, either before the Ecwid's script.js or after. The `ecwid_sso_profile` is initialized **once** – when Ecwid loads on the page.

Send user information in an SSO payload to Ecwid:

```javascript
var ecwid_sso_profile = '93n3ufncucndndner9872h34b43ird8djd8d8 8787aa437a4aaa3ds8787 1421317550';
```

#### Ecwid.setSsoProfile()

The above mentioned SSO approach with setting `ecwid_sso_profile` variable works well when login/logout actions on the site are done along with the page reload. If a website utilizes AJAX for login/logout functionality, the page won't be reloaded and thus `ecwid_sso_profile` will not be updated instantly. In this case, you can use `Ecwid.setSsoProfile()` API method.

The `Ecwid.setSsoProfile()` method does exactly the same as setting of the `ecwid_sso_profile` variable, but can be used multiple times within the same "session".

Here is how you will use that:

* Handle all logins/logouts events on the page
* When a user is logged in, send an AJAX request to your server to retrieve SSO payload
* Execute `Ecwid.setSsoProfile()` function and pass the retrieved SSO payload as parameter

Sign in a user dynamically without page reloading by means of `Ecwid.setSsoProfile()`:

```javascript
// This is supposed to be executed after a user is logged in on your site

// Retrieve SSO payload from the server
var ssoPayload = ... 

Ecwid.setSsoProfile(ssoPayload);
```

> 📘
>
> **Ecwid.setSsoProfile** works only when Ecwid is in SSO mode, that is, when the global variable 'ecwid\_sso\_profile' is also defined. Make sure 'ecwid\_sso\_profile' is defined at least as empty string, like this: ecwid\_sso\_profile = '' .

#### When no one is logged in

To specify that no user is logged in, pass an empty payload either to the `ecwid_sso_profile=''` variable or to `Ecwid.setSsoProfile("")` method. Ecwid will 'understand' that nobody is logged in at the moment and log out the current user if any.

### Sign the SSO payload

When you pass user information to Ecwid either in `ecwid_sso_profile` JS variable or with `Ecwid.setSsoProfile()` method, you need to create and sign the payload. SSO payload contains of the following parts connected with a space character:

Generate SSO payload and send it to Ecwid to log the user in Ecwid (Example)

```php
<?php
    $client_secret = "A1Lu7ANIhKD6A1Lu7ANIhKD6ADsaSdsa"; // example value
    $message = base64_encode("{appClientId: 'my-cool-app', userId:'234', profile: { email:'test@example.com', billingPerson: { name: 'John Doe' } }}"); // example values
    $timestamp = time();
    $hmac = hash_hmac('sha256', "$message $timestamp", $client_secret);

    echo "<script> var ecwid_sso_profile = '$message $hmac $timestamp'; </script>";
?>
```

#### Message

The message is a Base64-encoded JSON string containing user profile fields and the application ID. See the `Message` field format explained below.

> 📘
>
> Parameters in **bold** are mandatory

| Field           | Type      | Description                                                                                                                                                                                                                                                                                                                                |
| --------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **appClientId** | string    | Your application's **client\_id** value. Example: `my-cool-app`                                                                                                                                                                                                                                                                            |
| **userId**      | string    | Any string identifying the user in the 3rd-party authentication system. Examples: `72551`, `johnsmith87`. The combination of appClientId and userId identifies the customer profile in Ecwid connected with your site.                                                                                                                     |
| **profile**     | _Profile_ | User information. If a customer with the given combination of `appClientId` and `userId` already associated with some customer in your Ecwid store, the profile on file will be merged with the provided fields. Exception is the customer address book (`shippingAddresses`), which is only filled once when profile is created in Ecwid. |

**Profile**

| Field             | Type                    | Description                     |
| ----------------- | ----------------------- | ------------------------------- |
| **email**         | string                  | Customer email                  |
| billingPerson     | <_Person_>              | Customer's billing name/address |
| shippingAddresses | Array<_Person_>         | Customer address book items     |
| registered        | number (UNIX timestamp) | Registration date               |

**Person**

| Field               | Type   | Description                  |
| ------------------- | ------ | ---------------------------- |
| **name**            | string | Customer full name           |
| companyName         | string | Customer company name        |
| street              | string | Street                       |
| city                | string | City                         |
| countryCode         | string | Country code (2-letter code) |
| countryName         | string | Country name                 |
| postalCode          | string | Postal code (zip code)       |
| stateOrProvinceCode | string | State/province code          |
| phone               | string | Phone number                 |

**Signature**

The signature should be generated by HMAC **SHA256** encryption of the Base64-encoded profile data and timestamp. Use your **client\_secret** as a signature key. The secret key is provided when you register an application.

Every message should have different signature. If a message has a signature that has already been seen recently, Ecwid denies the sign-on request.

**Timestamp**

UNIX timestamp. The system clock on your server must be in sync with the actual time, otherwise signatures generated by your server will fail to validate in Ecwid. Ecwid allows this timestamp to be up to 10 minutes late. The timestamp ensures that the message cannot be intercepted and misused later.

### FAQ

**Q: Is SSO available to all stores?**

Single Sign On is available for [paid Ecwid users only](https://www.ecwid.com/pricing). If an Ecwid store has no paid subscription, Ecwid stops processing SSO requests for that store and will behave as if no user is logged in.

**Q: How do I know that SSO is working?**

When `ecwid_sso_profile` variable is set on a page, Ecwid will hide the Sign In and Sign Out links in a storefront. However in some cases this doesn't mean that the SSO functionality is working successfully.

To make sure that Single Sign On functionality is working, customer in merchant's store should be able to do any action that any logged in customer would do: add shipping addresses to their address book, use prefilled details on checkout, etc.

Another clear indicator can be the email field in the payment method selection of the checkout process. If your storefront has this field hidden, then the Single Sign On is working correctly in your store.

When troubleshooting this issue, please make sure to check if the **client\_secret** that you specified in your code is correct. You can find out more about it in the **Signature** section above.

**Q: Can I use SSO for existing customer account in a store?**

Ecwid does not allow two customers with the same email address in one store. If a customer with the same email already exists and has different SSO appClientId/userId, or does not have them at all, then Ecwid will fail to create a customer account and will behave as if no user is logged in.

For example, If you have a customer `customer@example.com` from Facebook, you cannot have another `customer@example.com` signing in using SSO. Ecwid will simply ignore `customer@example.com` passed in SSO.
