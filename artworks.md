# Artworks

### [Get All Artworks](https://docs.frm.fm/#/Artworks?id=get-all-artworks) <a href="#get-all-artworks" id="get-all-artworks"></a>

This endpoint retrieves all artworks. The results returned are paginated.

HTTP Request: `GET https://api.phuquoc.dog/artworks`

Special Query Parameters

| Parameter | Default | Description                                           |                         Example |
| --------- | :-----: | ----------------------------------------------------- | ------------------------------: |
| page      |  false  | Return results pertaining to that page                |                          page=3 |
| fields    |  false  | Allows you to return only attributes that you require | fields=artworkId,createdOn,name |
| limit     |    10   | The number of results returned per page               |                        limit=50 |
| sort      |   desc  | Sort artworks                                         |                        sort=asc |

Sample request gets two items:

```
curl GET https://api.phuquoc.dog/artworks?key=57819db00e710314f64fc1de6cd56ca7&limit=2
```

Results:

```
{
    "data": [
        {
            "id": 10,
            "artistId": 2,
            "name": "Awesome artwork 02",
            "artistName": "Phuquoc Doge",
            "artworkCategoryId": 1,
            "image": {
                "id": 28,
                "key": "thumbnail/fb4cb59ea3b03a627a7ea5cc1492ce77.jpg",
                "privacy": "public-read",
                "url": "https://cdn.phuquocdoge.com/thumbnail/fb4cb59ea3b03a627a7ea5cc1492ce77.jpg",
                "expires": 1626901761,
                "originalFileName": "chameleon_sl5uty.jpg",
                "fileSize": 118828,
                "cdn": "https://cdn.phuquocdoge.com/thumbnail/fb4cb59ea3b03a627a7ea5cc1492ce77.jpg",
                "isVideo": false
            },
            "imageBgcolor": null,
            "previewImages": [],
            "artworkNameUrl": "awesome-artwork-02",
            "isPrivate": 0,
            "status": 1,
            "price": 2000,
            "currency": "usd",
            "video": null,
            "videoLink": "https://media.niftygateway.com/video/upload/q_auto:good,w_500/v1615427766/A/WhIsBe/chameleon_sl5uty.mp4",
            "currentVersionId": 10,
            "draftVersionId": null,
            "createdOn": "2021-07-11 14:13:57",
            "modifiedOn": "2021-07-11 14:14:42",
            "humanPrice": "$2,000.00",
            "humanPriceJPY": "¥213,264",
            "metadata": null,
            "artistOrder": null,
            "streamingUrl": null,
            "numberOfEditions": "Open",
            "videoThumbnail": null,
            "users": {
                "id": 2,
                "roleId": 5,
                "username": "phuquocdog",
                "email": "hello@phuquoc.dog",
                "title": null,
                "firstname": "PQD",
                "lastname": null,
                "image": {
                    "id": 9,
                    "key": "avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "privacy": "public-read",
                    "url": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "expires": 1626639683,
                    "originalFileName": "phuquocoge.png",
                    "fileSize": 10553,
                    "cdn": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "isVideo": false
                },
                "cover": null,
                "country": null,
                "zone": null,
                "address": null,
                "zipcode": null,
                "profile": null,
                "bio": "Decentralized dogs social network, it is the best social network for pets, where you can share photos and videos of your pet's life, rescue puppies, adopt a pet, find pet friendly places and take advantage of our useful pet services. Join the moon mission.",
                "url": null,
                "amount": null,
                "deposited": null,
                "lastLogin": null,
                "active": 1,
                "language": null,
                "specialRoles": 0,
                "creationDate": "2021-06-30 08:00:18",
                "modifiedDate": null,
                "activeDate": "2021-06-30 08:00:18",
                "artistNameUrl": null,
                "organizational": 0,
                "emailNotification": 1,
                "deviceRegistered": 0
            },
            "artist": {
                "id": 2,
                "roleId": 5,
                "username": "phuquocdog",
                "email": "hello@phuquoc.dog",
                "title": null,
                "firstname": "PQD",
                "lastname": null,
                "image": {
                    "id": 9,
                    "key": "avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "privacy": "public-read",
                    "url": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "expires": 1626639683,
                    "originalFileName": "phuquocoge.png",
                    "fileSize": 10553,
                    "cdn": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "isVideo": false
                },
                "cover": null,
                "country": null,
                "zone": null,
                "address": null,
                "zipcode": null,
                "profile": null,
                "bio": "Decentralized dogs social network, it is the best social network for pets, where you can share photos and videos of your pet's life, rescue puppies, adopt a pet, find pet friendly places and take advantage of our useful pet services. Join the moon mission.",
                "url": null,
                "amount": null,
                "deposited": null,
                "lastLogin": null,
                "active": 1,
                "language": null,
                "specialRoles": 0,
                "creationDate": "2021-06-30 08:00:18",
                "modifiedDate": null,
                "activeDate": "2021-06-30 08:00:18",
                "artistNameUrl": null,
                "organizational": 0,
                "emailNotification": 1,
                "deviceRegistered": 0
            }
        },
        {
            "id": 12,
            "artistId": 2,
            "name": "Geo galaxy",
            "artistName": "Phuquoc Doge",
            "artworkCategoryId": 2,
            "image": {
                "id": 30,
                "key": "thumbnail/14a5f1b72d2bacdaa67f40515d0a3d04.jpg",
                "privacy": "public-read",
                "url": "https://cdn.phuquocdoge.com/thumbnail/14a5f1b72d2bacdaa67f40515d0a3d04.jpg",
                "expires": 1626945382,
                "originalFileName": "cd56b1267498994271e48cb70d2dfc06.jpg",
                "fileSize": 856919,
                "cdn": "https://cdn.phuquocdoge.com/thumbnail/14a5f1b72d2bacdaa67f40515d0a3d04.jpg",
                "isVideo": false
            },
            "imageBgcolor": null,
            "previewImages": [],
            "artworkNameUrl": "geo-galaxy",
            "isPrivate": 0,
            "status": 1,
            "price": 1500,
            "currency": "usd",
            "video": null,
            "videoLink": null,
            "currentVersionId": 12,
            "draftVersionId": null,
            "createdOn": "2021-07-12 02:21:20",
            "modifiedOn": "2021-07-12 02:21:41",
            "humanPrice": "$1,500.00",
            "humanPriceJPY": "¥159,948",
            "metadata": null,
            "artistOrder": null,
            "streamingUrl": null,
            "numberOfEditions": "Open",
            "videoThumbnail": null,
            "users": {
                "id": 2,
                "roleId": 5,
                "username": "phuquocdog",
                "email": "hello@phuquoc.dog",
                "title": null,
                "firstname": "PQD",
                "lastname": null,
                "image": {
                    "id": 9,
                    "key": "avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "privacy": "public-read",
                    "url": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "expires": 1626639683,
                    "originalFileName": "phuquocoge.png",
                    "fileSize": 10553,
                    "cdn": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "isVideo": false
                },
                "cover": null,
                "country": null,
                "zone": null,
                "address": null,
                "zipcode": null,
                "profile": null,
                "bio": "Decentralized dogs social network, it is the best social network for pets, where you can share photos and videos of your pet's life, rescue puppies, adopt a pet, find pet friendly places and take advantage of our useful pet services. Join the moon mission.",
                "url": null,
                "amount": null,
                "deposited": null,
                "lastLogin": null,
                "active": 1,
                "language": null,
                "specialRoles": 0,
                "creationDate": "2021-06-30 08:00:18",
                "modifiedDate": null,
                "activeDate": "2021-06-30 08:00:18",
                "artistNameUrl": null,
                "organizational": 0,
                "emailNotification": 1,
                "deviceRegistered": 0
            },
            "artist": {
                "id": 2,
                "roleId": 5,
                "username": "phuquocdog",
                "email": "hello@phuquoc.dog",
                "title": null,
                "firstname": "PQD",
                "lastname": null,
                "image": {
                    "id": 9,
                    "key": "avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "privacy": "public-read",
                    "url": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "expires": 1626639683,
                    "originalFileName": "phuquocoge.png",
                    "fileSize": 10553,
                    "cdn": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                    "isVideo": false
                },
                "cover": null,
                "country": null,
                "zone": null,
                "address": null,
                "zipcode": null,
                "profile": null,
                "bio": "Decentralized dogs social network, it is the best social network for pets, where you can share photos and videos of your pet's life, rescue puppies, adopt a pet, find pet friendly places and take advantage of our useful pet services. Join the moon mission.",
                "url": null,
                "amount": null,
                "deposited": null,
                "lastLogin": null,
                "active": 1,
                "language": null,
                "specialRoles": 0,
                "creationDate": "2021-06-30 08:00:18",
                "modifiedDate": null,
                "activeDate": "2021-06-30 08:00:18",
                "artistNameUrl": null,
                "organizational": 0,
                "emailNotification": 1,
                "deviceRegistered": 0
            }
        }
    ],
    "meta": {
        "pagination": {
            "total": 6,
            "count": 3,
            "per_page": 2,
            "current_page": 1,
            "total_pages": 3,
            "links": {
                "next": 2
            }
        }
    }
}
```

### Get an Artwork the user <a href="#get-a-artwork-by-user" id="get-a-artwork-by-user"></a>



HTTP Request: `GET https://api.phuquoc.dog/artworks/user/{username|id}`

For example to get artwork with username eric

```
curl  -X GET ${HOST}/artworks/user/phuqocdog?limit=2
-H "Content-Type: application/json" \
-H "Authorization : Bearer eyJ0eXAiOi"
```

### Get a Specific Artwork <a href="#get-a-specific-artwork" id="get-a-specific-artwork"></a>

The same people endpoint is used with a filter applied to return only a specific artwork. We've also specifically requested the fields we need to improve speed and readability

HTTP Request: `GET https://api.phuquoc.dogartworks/{id}`

For example to get artwork with id = 145

```
curl  -X GET https://api.phuquoc.dog/artworks/12?key=57819db00e710314f64fc1de6cd56ca7
-H "Content-Type: application/json" \
-H "Authorization : Bearer eyJ0eXAiOi"
```

Result:

```
{
    "data": {
        "id": 12,
        "artistId": 2,
        "name": "Geo galaxy",
        "artistName": "Phuquoc Doge",
        "artworkCategoryId": 2,
        "image": {
            "id": 30,
            "key": "thumbnail/14a5f1b72d2bacdaa67f40515d0a3d04.jpg",
            "privacy": "public-read",
            "url": "https://cdn.phuquocdoge.com/thumbnail/14a5f1b72d2bacdaa67f40515d0a3d04.jpg",
            "expires": 1626945382,
            "originalFileName": "cd56b1267498994271e48cb70d2dfc06.jpg",
            "fileSize": 856919,
            "cdn": "https://cdn.phuquocdoge.com/thumbnail/14a5f1b72d2bacdaa67f40515d0a3d04.jpg",
            "isVideo": false
        },
        "imageBgcolor": null,
        "previewImages": [],
        "artworkNameUrl": "geo-galaxy",
        "isPrivate": 0,
        "status": 1,
        "price": 1500,
        "currency": "usd",
        "video": null,
        "videoLink": null,
        "currentVersionId": 12,
        "draftVersionId": null,
        "createdOn": "2021-07-12 02:21:20",
        "modifiedOn": "2021-07-12 02:21:41",
        "humanPrice": "$1,500.00",
        "humanPriceJPY": "¥159,948",
        "metadata": null,
        "artistOrder": null,
        "streamingUrl": null,
        "numberOfEditions": "Open",
        "videoThumbnail": null,
        "users": {
            "id": 2,
            "roleId": 5,
            "username": "phuquocdog",
            "email": "hello@phuquoc.dog",
            "title": null,
            "firstname": "PQD",
            "lastname": null,
            "image": {
                "id": 9,
                "key": "avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                "privacy": "public-read",
                "url": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                "expires": 1626639683,
                "originalFileName": "phuquocoge.png",
                "fileSize": 10553,
                "cdn": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                "isVideo": false
            },
            "cover": null,
            "country": null,
            "zone": null,
            "address": null,
            "zipcode": null,
            "profile": null,
            "bio": "Decentralized dogs social network, it is the best social network for pets, where you can share photos and videos of your pet's life, rescue puppies, adopt a pet, find pet friendly places and take advantage of our useful pet services. Join the moon mission.",
            "url": null,
            "amount": null,
            "deposited": null,
            "lastLogin": null,
            "active": 1,
            "language": null,
            "specialRoles": 0,
            "creationDate": "2021-06-30 08:00:18",
            "modifiedDate": null,
            "activeDate": "2021-06-30 08:00:18",
            "artistNameUrl": null,
            "organizational": 0,
            "emailNotification": 1,
            "deviceRegistered": 0
        },
        "artist": {
            "id": 2,
            "roleId": 5,
            "username": "phuquocdog",
            "email": "hello@phuquoc.dog",
            "title": null,
            "firstname": "PQD",
            "lastname": null,
            "image": {
                "id": 9,
                "key": "avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                "privacy": "public-read",
                "url": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                "expires": 1626639683,
                "originalFileName": "phuquocoge.png",
                "fileSize": 10553,
                "cdn": "https://cdn.phuquocdoge.com/avatar/c81e728d9d4c2f636f067f89cc14862c.png",
                "isVideo": false
            },
            "cover": null,
            "country": null,
            "zone": null,
            "address": null,
            "zipcode": null,
            "profile": null,
            "bio": "Decentralized dogs social network, it is the best social network for pets, where you can share photos and videos of your pet's life, rescue puppies, adopt a pet, find pet friendly places and take advantage of our useful pet services. Join the moon mission.",
            "url": null,
            "amount": null,
            "deposited": null,
            "lastLogin": null,
            "active": 1,
            "language": null,
            "specialRoles": 0,
            "creationDate": "2021-06-30 08:00:18",
            "modifiedDate": null,
            "activeDate": "2021-06-30 08:00:18",
            "artistNameUrl": null,
            "organizational": 0,
            "emailNotification": 1,
            "deviceRegistered": 0
        }
    }
}
```

### Delete an Artwork <a href="#delete-a-artwork" id="delete-a-artwork"></a>



HTTP Request: `DELETE https://api.phuquoc.dog/artworks/{id}`

This endpoint allows you to delete a resource.

Deleting a resource removes it from all relation tables and rate schemes! This cannot be undone so be careful

Special Query Parameters

| Parameter |            Description           | Example |
| --------- | :------------------------------: | ------: |
| id        | The ID of the resource to delete |   id=50 |

A successful delete will return the following JSON:

```
{
    "success": {
        "message": "Delete artwork success",
        "code": 202
    }
}
```

### &#x20;<a href="#delete-a-artwork" id="delete-a-artwork"></a>
