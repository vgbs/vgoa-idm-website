---
title: Identity Management Help
description: Developer Documentation
---

[&larr; back to Overview](/)

## SSO Adapters

We are using a standard OAuth2 SSO implementation. Adapters are available for most programming languages and technology stacks. There is not one generally valid documentation for all. As we are supporting teams to implement, we will add more and more links to available documentations:

* Java Spring: Link

## Userinfo API

You can use the userinfo resource to get relevant data from the user to start off.

```
qa base-server-url: https://idm-qa.vaillant-group.com
production base-server-url: https://idm.vaillant-group.com
```

### Request GET /userinfo

Retrieves the consented UserInfo and other claims about the logged-in subject (end-user).

#### Parameters

* `Authorization`: The access token received after login.

### Response 200

```
{
    "companyName": "string",
    "salesforceAccountId": "string",
    "customerNumber": "string",
    "companyAddress": "string",
    "companyPhone": "string",
    "companyMobile": "string",
    "companyFax": "string",
    "companyEmail": "string",
    "companyWebsite": "string",
    "salesforceLoyaltyId": "string",
    "name": "string",
    "salesforceContactId": "string",
    "email": "string",
}
```

## How To Start

What we need from you to set everything up:

* Frontend or backend authentification method
* Realm
    * Brand
    * Country
    * Environment (development / QA / production)
* List of your redirect URIs separated by realm

What you will get from us:

* Your SSO base URL
* Your client credentials