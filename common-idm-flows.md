---
title: Identity Management Help
description: Common IDM Flows
---

[&larr; back to Overview](/)


## Login
The login url should be assembled by your Adapter. Please consult the [official docs](https://www.keycloak.org/docs/latest/securing_apps/#_oidc) to find your best fit.

## Logout
Logout is possible with and without user interaction.

If you want the user to confirm the logout interactively, you can direct her to:
```
https://identity-qa.vaillant-group.com/auth/realms/<REALM_ID>/protocol/openid-connect/logout
```


If you want to logout the user via AJAX, use the following URL.
```
https://identity-qa.vaillant-group.com/auth/realms/<REALM_ID>/protocol/openid-connect/logout?id_token_hint=<ID_TOKEN>
```
## Change Password
Use the URL below to let the user update her password. The user has to be logged in, in order to change her password. If the user isn't logged in, when visiting the change-password url, the login screen shows up first.

```
https://keycloak.qa.dsp.vaillant-group.cloud/auth/realms/<REALM_ID>/password/change?client_id=<CLIENT_ID>&redirect_uri=<REDIRECT_URI>
```
## Delete Account (B2C only)
Use the URL below to let the user delete her account. The user has to be logged in, in order to delete her account. If the user isn't logged in, when visiting the delete-account url, the login screen shows up first. The user has to confirm the delete action with her password.
```
https://identity-qa.vaillant-group.com/auth/realms/vaillant-germany-b2c/user-account/delete?client_id=playground-b2c&redirect_uri=www.example.org
```

## User Registration (Activation)
Self-service registration is not yet supported by the IDM. To this date, all services depend on specific user data in salesforce.
However, there are API endpoints you can call to activate a user that already has the necessary data inside of salesforce.

Consult the [API Documentation](api-documentation.html) page to see the available endpoints.