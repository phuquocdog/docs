# Authentication

The API supports Basic Authentication as defined in [RFC2617](http://www.ietf.org/rfc/rfc2617.txt) with a few slight differences. The main difference is that the RFC requires unauthenticated requests to be answered with `401 Unauthorized` responses. In many places, this would disclose the existence of user data. Instead, the Phu Quoc Dog API responds with `404 Not Found`. This may cause problems for HTTP libraries that assume a `401 Unauthorized` response. The solution is to manually craft the `Authorization` header.

We recommend you use OAuth tokens to authenticate to the Phu Quoc Dog API.

#### Via username and password <a href="#via-username-and-password" id="via-username-and-password"></a>

| Property Name   | Type    | Description               |
| --------------- | ------- | ------------------------- |
| emailOrUsername | string  | User or Email is required |
| password        | stringi | Password is required      |

Sample request:

```
//user.json
{
    "emailOrUsername" : "hello@phuquoc.dog",
    "password": "phuuqocdogawesome",
}
curl -d user.json -H "Content-Type: application/json" -X POST https://phuquoc.dog/auth
```

Sample response:

```
// Some code
{
     "message": "Successful Login",
     "token": "phquucqass.fff.lLk3P7wyIVSYFZ4FNml1pT57CZUPF9hiwh3NJCAK2mU",
     "expiresIn": 1565130133
 }
```

#### Authenticating for SAML SSO <a href="#authenticating-for-saml-sso" id="authenticating-for-saml-sso"></a>

**Note:** Integrations and OAuth applications that generate tokens on behalf of others are automatically authorized.

// TODO

#### Working with two-factor authentication <a href="#working-with-two-factor-authentication" id="working-with-two-factor-authentication"></a>

// TODO
