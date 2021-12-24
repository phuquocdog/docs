# Page 1

### Retrieves all followers

This endpoint retrieves all followers. The results returned are paginated.

HTTP Request: `GET ${HOST}/followers/me`

Special Query Parameters

| Parameter | Default | Description                             |  Example |
| --------- | :-----: | --------------------------------------- | -------: |
| page      |  false  | Return results pertaining to that page  |   page=3 |
| limit     |    10   | The number of results returned per page | limit=50 |

Sample request gets two items:

```
// Some code
curl  -H "Content-Type: application/json" -X GET https://api.phuquoc.dog/followers/me?limit=2&page=1&key=xxx
```

Sample response:

```
// Some code
{
    "data": [
        {
            "id": 3,
            "roleId": 4,
            "username": "akita",
            "email": "akita@gmail.com",
            "title": Fan,
            "firstname": Akita,
            "lastname": null,
            "image": null,
            "cover": null,
            "country": null,
            "zone": null,
            "address": null,
            "zipcode": null,
            "profile": null,
            "bio": null,
            "url": null,
            "amount": 0,
            "deposited": 0,
            "lastLogin": "2020-01-14 02:59:41",
            "active": 1,
            "language": "en",
            "specialRoles": 1048576,
            "creationDate": "2021-11-18 11:32:14",
            "modifiedDate": "2021-11-19 16:33:16",
            "activeDate": "2021-11-18 11:32:14",
            "artistNameUrl": "akita",
            "organizational": 0,
            "emailNotification": 1,
            "deviceRegistered": 1
        },
        {
            "id": 9,
            "roleId": 4,
            "username": "shiba",
            "email": "shiba@gmail.com,
            "title": null,
            "firstname": "Fan",
            "lastname": "Shiba",
            "image": {
                "id": 149,
                "key": "avatar/shiba.jpg",
                "privacy": "public-read",
                "url": "https://cdn.phuquoc.dog/avatar/shiba.jpg",
                "expires": 1431967400,
                "originalFileName": "skydivefilip-square.jpg",
                "fileSize": null,
                "cdn": "https://cdn.phuquoc.dog/avatar/shiba.jpg"
            },
            "cover": 5,
            "country": null,
            "zone": null,
            "address": "London",
            "zipcode": null,
            "profile": null,
            "bio" : "Decentralized social network and NFT platform for pets ",
            "url": "http://fvda.co.uk",
            "amount": 0,
            "deposited": 0,
            "lastLogin": "2020-01-09 10:07:10",
            "active": 1,
            "language": "en",
            "specialRoles": 65536,
            "creationDate": "2015-04-30 13:33:53",
            "modifiedDate": "2016-10-19 13:08:10",
            "activeDate": "2015-07-04 00:00:00",
            "artistNameUrl": "filip_visnjic",
            "organizational": 0,
            "emailNotification": 1,
            "deviceRegistered": 1
        }
    ],
    "meta": {
        "pagination": {
            "total": 2,
            "count": 1,
            "per_page": 2,
            "current_page": 1,
            "total_pages": 1,
            "links": {}
        }
    }
}
```

### Get followers to specify user <a href="#get-followers-specify-user" id="get-followers-specify-user"></a>

This endpoint retrieves all followers by a specific user. The results returned are paginated.

HTTP Request: `GET ${HOST}/followers/user/{username|userId}`

Special Query Parameters



| Parameter | Default | Description                             |  Example |
| --------- | :-----: | --------------------------------------- | -------: |
| page      |  false  | Return results pertaining to that page  |   page=3 |
| limit     |    10   | The number of results returned per page | limit=50 |

Sample request get two item with user `eric`

```
curl  -H "Content-Type: application/json" -X GET ${HOST}/followers/user/pqd?limit=2&page=1&key=xxx
```

### Retrieves all following.

This endpoint retrieves all following. The results returned are paginated.

HTTP Request: `GET ${HOST}/following/me`

Special Query Parameters

| Parameter | Default | Description                             |  Example |
| --------- | :-----: | --------------------------------------- | -------: |
| page      |  false  | Return results pertaining to that page  |   page=3 |
| limit     |    10   | The number of results returned per page | limit=50 |

Sample request gets two items:

```
// Some code
curl  -H "Content-Type: application/json" -X GET ${HOST}/following/me?limit=2&page=1&key=xxx
```

### Get the following specific user

This endpoint retrieves all followers by specific the user. The results returned are paginated.

HTTP Request: `GET ${HOST}/following/user/{username|userId}`

Special Query Parameters

| Parameter | Default | Description                             |  Example |
| --------- | :-----: | --------------------------------------- | -------: |
| page      |  false  | Return results pertaining to that page  |   page=3 |
| limit     |    10   | The number of results returned per page | limit=50 |

Sample request get one item with user `pqd`

```
// Some code
curl  -H "Content-Type: application/json" -X GET ${HOST}/following/user/pqd?limit=1&page=1&key=xxx
```

Sample response:

```
// Some code
{
    "data": [
        {
            "id": 4,
            "roleId": 5,
            "username": "shiba",
            "email": "shiba@gmail.com",
            "title": null,
            "firstname": null,
            "lastname": null,
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
            "lastLogin": "2021-12-15 07:37:02",
            "active": 1,
            "language": "en",
            "specialRoles": 851971,
            "creationDate": "2021-12-1 07:37:02",
            "modifiedDate": "2021-12-3 07:37:02",
            "activeDate": "2021-12-15 07:37:02",
            "artistNameUrl": null,
            "organizational": null,
            "emailNotification": 1,
            "deviceRegistered": 1
        }
    ],
    "meta": {
        "pagination": {
            "total": 3,
            "count": 2,
            "per_page": 2,
            "current_page": 1,
            "total_pages": 2,
            "links": {
                "next": 2
            }
        }
    }
}
```

### Create a new following



HTTP Request: `POST ${HOST}/following`

| Property Name | Type |            Description            | Default | Required |
| ------------- | ---- | :-------------------------------: | ------- | -------- |
| userId        | int  | The user id you want to following | n/a     | yes      |

For example, to create the following user with id = 10the json will be like that.

```
follow.json
{
    "userId" : "10",
}
curl "${HOST}/following" \
    -X POST \
    -H "Authorization: Bearer 123456" \
    -H "Content-Type: application/json" \
    -d @follow.json
```

Result:

```
// Some code
{
    "data": {
        "id": 11,
        "roleId": 4,
        "username": "bitcoin",
        "email": "bitcoin@gmail.com",
        "title": null,
        "firstname": null,
        "lastname": null,
        "image": null,
        "cover": null,
        "country": null,
        "zone": null,
        "address": null,
        "zipcode": null,
        "profile": null,
        "bio": null,
        "url": null,
        "amount": 0,
        "deposited": 0,
        "lastLogin": "2021-12-16 16:20:06",
        "active": 1,
        "language": "en",
        "specialRoles": 0,
        "creationDate": "2021-12-06 16:20:06",
        "modifiedDate": "2021-12-06 16:20:06",
        "activeDate": "2021-12-06 16:20:06",
        "artistNameUrl": "bitcoin",
        "organizational": 0,
        "emailNotification": 1,
        "deviceRegistered": 1
    }
}
```
