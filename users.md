# Users

### Create user <a href="#create-users" id="create-users"></a>

HTTP Request: `POST ${HOST}/users`

| Property Name | Type   |            Description           | Default | Required |
| ------------- | ------ | :------------------------------: | ------- | -------- |
| email         | string |        The email register        | n/a     | yes      |
| password      | string |   The password a user register   | n/a     | yes      |
| username      | string |   The username a user register   | n/a     | yes      |
| bio           | text   |      Bio information a user      | n/a     | no       |
| country       | init   | \*The country id a user register | n/a     | yes      |
| zone          | init   |    The zone id a user register   | n/a     | yes      |
| firstname     | string |   The firstname a user register  | n/a     | yes      |
| lastname      | string |   The lastname a user register   | n/a     | yes      |
| title         | string |     The title a user register    | n/a     | yes      |

* To get id all countries see Countries Docs
* To get id all zone, see Zone Docs

Sample request:

```
//user.json
{
    "email" : "hello@phuuqoc.dog",
    "password": "phuquocaewsome",
    "username": "phuquocdog",
    "firstname" : "PQD",
    "lastname": "Coin"
}
curl -d user.jon -H "Content-Type: application/json" -X POST https://api.phuquoc.dog/users
```

Sample response:

```
 {
     "data": {
         "id": 4,
         "roleId": 5,
         "username": "phuquocdog",
         "email": "hello@phuquoc.dog",
         "title": null,
         "firstname": "PQD",
         "lastname": "Coin",
         "image": null,
         "cover": null,
         "country": null,
         "zone": null,
         "address": null,
         "zipcode": null,
         "profile": null,
         "bio": null,
         "url": null,
         "amount": null,
         "deposited": null,
         "lastLogin": null,
         "active": null,
         "language": null,
         "specialRoles": null,
         "creationDate": "2021-12-1 08:12:35",
         "modifiedDate": null,
         "activeDate": null,
         "artistNameUrl": null,
         "organizational": null,
         "emailNotification": null,
         "deviceRegistered": null
     }
 }
```

#### Update user



HTTP Request: `PUT https://api.phuquoc.dog/users`

```
curl -d '{"fullName" : "Lackky", "bio" : " Iam developer", "phone" : "012345678"}'
\ -H "Content-Type: application/json" -X PUT https://api.phuquoc.dog/users
```

#### Update avatar

HTTP Request: `POST https://api.phuquoc.dog/users/avatar`

Request Body Payload

| Property Name | Type |                                       Description |
| ------------- | :--: | ------------------------------------------------: |
| file          | File | File is required, only support format image allow |

### Update password



HTTP Request: `POST https://api.phuquoc.dog/users/password`

Here example to update password current user:

```
curl -d '{"password": "filecoinawesome"}' 
\ -H "Content-Type: application/json" -X PUT  https://api.phuquoc.dog/password
```

### Reset password <a href="#reset-password" id="reset-password"></a>

Use the password API with the recovery endpoint to send a password recovery email (including link and recovery token) to the end-user.

HTTP Request: `GET https://api.phuquoc.dog/users/forgot_password`

```
{
    "email" : "user@phuquoc.dog"
}
curl  -X POST https://api.phuquoc.dog/forgot_password?key=xxx
-H "Content-Type: application/json" \
```

Result response

```
{
    "success": {
        "message": "You will receive a code to verify here so you can reset your account password.",
        "code": 200,
        "httpCode": 200
    }
}
```

The result of this request is password code random, and automatically included in the email to the end user. The link something like that

```
Hello PQD Coin

You have requested a password reset for the user hello@phuquoc.dog.

Please use this code to reset the password for the PQD coin
Here is your code: 341223
If you did not initiate this request, please ignore this email. 
```

Note that the password code random is not part of the response to the API call.

However, the password code random can be used in another POST request to reset the password.

The token is valid exactly once in the 24 hours after it is created. Once we have the token we can send a POST request

HTTP Request: `POST ${HOST}/users/reset_password`

```
{
    "hash" : "456324"
    "password" : "your new password"
}
```

Then the result:

```
{
    "token": "eAxoklokhaYULKLeyJpc3MiOiJcL3VzZXJzXC9yZXNldNzd29yZD9rZXk9Njc3YmQzZWI5N2M2NTFiMDNlNjc2NTI5MTQyNzc2Y2MiLCJpYXQiOjE1ODE0MzEwNDksImV4cCI6MTYxMjk2NzA0OSwiZGF0YSI6eyJpZCI6IjEiLCJlbWFpbCI6ImZjZHV5dGhpZW5AZ21haWwuY29tIn19.WEMYIf9Bk7BboM-08dYae74Aeca4crb0XegwtReAJCg",
    "expires": 1892967049
}
```
