# Flows

## Client Credentials Grant

[Official Documnetation](https://oauth.net/2/grant-types/client-credentials/)

Client credentials usus server-to-server authentication to obtain an access token on behalf of a user.

### 1. Setup Client Credentials

* Login to the CMS
* Go to OAuth in the left navigation menu
* Create a new client
* Give the client a name 
* Set "Grants" to "client_credentials"
* Press "Create". The other two fields will be automatically populated.

You should now have a new client with a populated secret and identifier. You can test authorisation using the following curl request:



### 2. Authorise

```
curl --location --request GET 'https://example.com/oauth2/authorise' \
--header 'Content-Type: application/json' \
--data-raw '{
	"grant_type": "client_credentials",
	"client_id": "<client-identifier>",
	"client_secret": "<client-secret>"
}'
```

You should receive an access token in the response.

```
{
    "token_type": "Bearer",
    "expires_in": 3600,
    "access_token": "<an access token>"
}
```

### 3. Authenticate

Now that the client has an access token, they can use this to authenticate with the resource server or application. How you do this will depend on what type of application you're creating. 

This module comes with an Authentication middlware which is backed up by a default validator for a Bearer token. This is extremely useful for API validation. To set this up you need to configure the middleware in your own config.

app/_config/auth.yml
```
---
Name: myrequestprocessors
After:
  - requestprocessors
---
SilverStripe\Core\Injector\Injector:
  SilverStripe\Control\Director:
    properties:
      Middlewares:
        AuthenticationMiddleware: %$AdvancedLearning\Oauth2Server\Middleware\AuthenticationMiddleware
```

> **WARNING** This is work in progress. Not all flows are documented and flows that are may be incomplete.
