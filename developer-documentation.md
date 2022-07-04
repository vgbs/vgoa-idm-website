---
title: Identity Management Help
description: Developer Documentation
---

[&larr; back to Overview](/)

## How To Start

What we need from you to set everything up:

* Are you using authentication in a frontend, a backend or both?
* Which Realms do you need access to:
    * Brand
    * Country
    * Environment (development / QA / production)
* List of your redirect URIs separated by realm
* What tech stack are you using

What you will get from us:

Basically all information that is needed in the oauth configuration of your tech stack. Namely:

* The SSO base URLs
* Your client credentials

## SSO Adapters

We are using a standard OAuth2 SSO implementation. Adapters are available for
most programming languages and technology stacks. There is not one generally
valid documentation for all. Generally, a good starting point is the offical
Keycloak Integration documentation which provides tutorials for different tech
stacks:

[Keycloak Securing Applications and Services Guide](https://www.keycloak.org/docs/latest/securing_apps/)

As we are supporting teams to implement, we will add more and more links to
available documentations:

* Java, Spring Boot: [Official Docs](https://spring.io/guides/tutorials/spring-boot-oauth2/)

## Available Information in the Token and the Userinfo

The JWT Tokens you get from the SSO contains several Vaillant-specific pieces
of information about the user. The following information are provided
automatically in each JWT:

```js
{
  "exp": int, // Expiration of this token (unix timestamp)
  "iat": int, // Issued at (unix timestamp)
  "auth_time": int, // time of authentication
  "jti": UUID, // Unique ID of this token
  "iss": String, // Issuer (URL of the originating REALM)
  "sub": String // Internal USER id
  // a few keycloak internals are skipped here
  "realm_access": {
    "roles": [
      // all salesforce web roles assigned to the contact (name and id)
      "Kompetenzpartner Programm 2019-2020",
      "a5p1r0000000DYjAAM",
      "HeizungOnline",
      "a5p690000008TvkAAE"
      // ...
    ]
  },
  // The following information are Vaillant specific
  // They are added to each token if the corresponding information
  // can be found in Salesforce. If not, the key will not be added
  // to the token.
  "salesforceContactId": "6301",
  "country": "DE",
  "brandName": "Vaillant",
  "email_verified": true,
  // deprecated - please use company.name from openid-connect userinfo endpoint (see below)
  "companyName": "First-Last GmbH",
  "preferred_username": "user@example.org",
  "locale": "de",
  "given_name": "First",
  "name": "First Last",
  "family_name": "Last",
  "email": "user@example.org",
  "salesforceAccountId": "1234",
  "salesforceBrandDetailContactId": "7981"
}
```

Additionally, the SSO provides a openid-connect userinfo endpoint to retrieve
additional information about a given user. As with the JWT, this userinfo
enpoint only provides information that is present in salesforce. If it is
missing, the key is omitted.

In case you need additional information in the userinfo response, feel free to
contact Daniel via Slack in our [Support Channel](https://vaillantgroup1874.slack.com/archives/C0386NABKTP).

These information are contained in the response of this endpoint:

### B2B

```js
{
  "salesforceContactId": "6301",
  "sub": String // Internal USER id
  "country": "DE",
  "salesforceLoyaltyId": "9955",
  "brandName": "vaillant",
  "email_verified": true,
  "preferred_username": "user@example.org",
  "locale": "de",
  "given_name": "First",
  "realm_access": {
    "roles": [
      "Kompetenzpartner Programm 2019-2020",
      "a5p1r0000000DYjAAM",
      "HeizungOnline",
      "a5p690000008TvkAAE"
    ]
  },
  "name": "First Last",
  // Company data = Salesforce account
  "company": {
    // if set the brand specific website, otherwise website from the account
    "website": "example.org",
    "address": {
      "country": "DE",
      "city": "Stadthausen",
      "street": "Straßenweg",
      "houseNumber": "123",
      "floor": "3",
      "flatNumber": "1B",
      "district": "Downtown",
      "county": "Example county",
      "postalCode": "12345",
      "extension": "B1337"
    },
    "contact": {
      "phone": "+49 123456",
      "additionalPhone": "+49 654321",
      "fax": "12345",
      "mobile": "123123213",
      "email": "user@example.org",
    },
    "name": "First-Last GmbH",
    "customerNumber": "11223",
    "taxNumber": "1337"
  },
  "title": "Dr",
  "salutation": "Herr",
  "family_name": "First",
  "email": "user@example.org",
  "phone": "1234",
  "mobile": "321313",
  "fax": "583585",
  "street": "Main street",
  "postalCode": "12345",
  "city": "Stadthausen",
  "county": "County1",
  "countryName": "DE",
  "extension": "abc",
  "salesforceAccountId": "1234",
  "salesforceBrandDetailContactId": "3344"
}
```

### B2C

```js
{
  "salesforceContactId": "6301",
  "sub": String // Internal USER id
  "country": "DE",
  "brandName": "vaillant",
  "email_verified": true,
  "preferred_username": "user@example.org",
  "locale": "de",
  "given_name": "First",
  "name": "First Last",
  "title": "Dr",
  "salutation": "Herr",
  "family_name": "First",
  "email": "user@example.org",
  "phone": "1234",
  "mobile": "321313",
  "fax": "583585",
  "street": "Main street",
  "postalCode": "12345",
  "city": "Stadthausen",
  "county": "County1",
  "countryName": "DE",
  "salesforceAccountId": "1234",
  "salesforceBrandDetailContactId": "3344"
}
```
