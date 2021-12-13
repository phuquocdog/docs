# Feeds

### [Create a feed from url](https://docs.frm.fm/#/Feeds?id=create-a-feed-from-url) <a href="#create-a-feed-from-url" id="create-a-feed-from-url"></a>

To create a feed you have following the structer below:



| Property Name | Type   |                        Description                        | Default | Required |
| ------------- | ------ | :-------------------------------------------------------: | ------- | -------- |
| url           | string |            The source you want to add new feed            | n/a     | yes      |
| tags          | string |                The tags name for this feed                | n/a     | no       |
| name          | string |             The title you want to add new feed            | n/a     | no       |
| isPrivate     | int    | Option for public or private that feed, default is public | 0       | no       |

For example to create a new feed:

```
// Some code
feed.json
{
    "url" : "https://www.phuquoc.dog",
    "tags" : "pqd,phuquocdog,polkadot",
    "name": "Add demo create feed",
    "isPrivate" : 0
}
curl "https://api.phuuqoc.dog/feeds" \
    -X POST \
    -H "Authorization: Bearer 1234567890" \
    -H "Content-Type: application/json" \
    -d @feed.json
```

Result:

```
// Some code
{
  "data": {
    "id": 2986,
    "url": "https://phuquoc.dog",
    "thumb": {
      "id": 4347,
      "key": "feeds/b2c8f70b1c31707.png",
      "privacy": "public-read",
      "url": "https://cdn.phuquoc.dog/feeds/b2c8f70b1c31707.png",
      "expires": 1571092182,
      "originalFileName": "bf7e6f5d7d3ccbd202caca8161867c90.png",
      "fileSize": 128730,
      "cdn": "https://cdn.phuquoc.dog/feeds/b2c8f70b1c31707.png"
    },
    "name": "Add demo create feed",
    "createdOn": "2021-11-09 15:34:55",
    "updatedOn": null,
    "thumbWidth": null,
    "thumbHeight": null,
    "tags": "pqd,phuquocdog,polkado",
    "userFollowing": {
      {
        "id": 1,
        "username": "phuquocdog"
      }
    }
  }
}
```

### [Create a feed from the library](https://docs.frm.fm/#/Feeds?id=create-an-feed-from-library) <a href="#create-an-feed-from-library" id="create-an-feed-from-library"></a>

There are two-part to create feed this design like submitting an email form gmail:

* One for upload context with format json
* One for uploading media files with format multipart/form-data

First, you need to create metadata for the feed, Once the metadata is uploaded success you get a URL, which allows you to PUT. PUT is idempotent so you can retry failed uploads to your heart's content, replacing old attempts as you go.



| Property Name | Type   |                        Description                        | Default | Required |
| ------------- | ------ | :-------------------------------------------------------: | ------- | -------- |
| type          | string |                The type name for this feed                | n/a     | yes      |
| tags          | string |                The tags name for this feed                | n/a     | no       |
| name          | string |             The title you want to add new feed            | n/a     | no       |
| isPrivate     | int    | Option for public or private that feed, default is public | 0       | no       |

For example to create a new feed:

```
// Some code
feed.json
{
    "tags" : "pqd,phuquocdog",
    "name": "Add demo create feed via upload file",
    "isPrivate" : 0,
    "type" : "upload"
}
curl "htps://api.phuuqoc.dog/feeds" \
    -X POST \
    -H "Authorization: Bearer 123456789" \
    -H "Content-Type: application/json" \
    -d @feed.json
```

Result:

```
// Some code
{
    "data": {
        "id": 12,
        "url": "upload",
        "thumb": null,
        "thumbBgcolor": null,
        "name": "Add demo create feed via upload file",
        "artistName": null,
        "createdOn": "2021-11-09 06:08:59",
        "updatedOn": null,
        "tags": "pqd,phuquocdog",
        "thumbWidth": null,
        "thumbHeight": null,
        "urlSource": null,
        "userId": 662,
        "deleted": null,
        "userFollowing": [
            {
                "id": 1,
                "username": "phuquocdog"
            }
        ],
        "isSaveFeed": true
    }
}
```

Then call api upload file, see docs at [./Uploads.md](https://docs.frm.fm/#/./Uploads?id=create-an-file)



```
curl "https://api.phuquoc.dog/uploads?type=image" \
    -X POST \
    -F 'image=@/path/to/pictures/picture.jpg'
    -H "Authorization: Bearer 123456789" \
    -H "Content-Type: multipart/form-data" 
```

Result:

This result to use step create the feed above, in that case, we will be using `id=34` to update again



```
{
  "id": 34,
  "key": "thumbnail/fc8eeee33b594503216eaa9.jpg",
  "privacy": "public-read",
  "url": "http://cdn.phuquoc.dog/thumbnail/fc8eeee33b594503216eaa9.jpg",
  "expires": 1569683899,
  "originalFileName": "E899D833--454F-B90C.jpg",
  "fileSize": 305956
}
```

Then mobile dev team uses that result update again into the metadata feed. Of course, the  mobile dev team can upload files first, then use that result to create a metadata feed.



```
feed.json
{
   "thumb" : "34",
   "type: "upload"
}
curl "https://api.phuquoc.dog/feeds/12" \
    -X PUT \
    -H "Authorization: Bearer 123456789" \
    -H "Content-Type: application/json" \
    -d @feed.json
```

### [Delete a feed](https://docs.frm.fm/#/Feeds?id=delete-a-feed) <a href="#delete-a-feed" id="delete-a-feed"></a>

HTTP Request: `DELETE https://api.phuquoc.dog/feeds/{id}`

This endpoint allows you to delete a resource.

Deleting a resource removes it from all relation table and rate schemes! This cannot be undone so be careful

Special Query Parameters

| Parameter |            Description           | Example |
| --------- | :------------------------------: | ------: |
| id        | The ID of the resource to delete |    id=3 |

A successful delete will return like below:

```
// Some code
{
    "success": {
        "message": "Delete feed success",
        "code": 202
    }
}
```

### [Update a feed](https://docs.frm.fm/#/Feeds?id=update-a-feed) <a href="#update-a-feed" id="update-a-feed"></a>

HTTP Request: `PUT https://api.phuquoc.dog/feeds/{id}`

```
// Some code
feed.json
{
    "tags" : "filecoin,pqd,ips",
    "name": "Add demo update feed",
    "isPrivate" : 0
}
curl "https://api.phuquoc.dog/feeds/2986" \
    -X POST \
    -H "Authorization: Bearer 123456" \
    -H "Content-Type: application/json" \
    -d @feed.json
```

The result:

```
// Some code
{
  "data": {
    "id": 2986,
    "url": "https://phuquoc.dog",
    "thumb": {
      "id": 4347,
      "key": "feeds/b2c8f70b1c31707.png",
      "privacy": "public-read",
      "url": "https://cdn.phuquoc.dog/feeds/b2c8f70b1c31707.png",
      "expires": 1571092182,
      "originalFileName": "bf7e6f5d7d3ccbd202caca8161867c90.png",
      "fileSize": 128730,
      "cdn": "https://cdn.phuquoc.dog/feeds/b2c8f70b1c31707.png"
    },
    "name": "Add demo update feed,
    "createdOn": "2021-11-09 15:34:55",
    "updatedOn": null,
    "thumbWidth": null,
    "thumbHeight": null,
    "tags": "filecoin,pqd,ips",
    "userFollowing": {
      {
        "id": 1,
        "username": "phuquocdog"
      }
    }
  }
}

```

#### &#x20;[Save feed to user](https://docs.frm.fm/#/Feeds?id=save-feed-to-user)

That feature like retweet on twitter.com

HTTP Request: `POST https://api.phuquoc.dog/feeds/refeed`

``

| Property Name | Type |                        Description                        | Default | Required |
| ------------- | ---- | :-------------------------------------------------------: | ------- | -------- |
| urlId         | int  |              The url id you want to save feed             | n/a     | yes      |
| isPrivate     | int  | Option for public or private that feed, default is public | 0       | no       |

For example, to re-feed with url id = 17 and status is public, the json will be like that.

```
// Some code
feed.json
{
    "urlId" : "17",
    "isPrivate" : 0
}
curl "https://api.phuquoc.dog/feeds/refeed" \
    -X POST \
    -H "Authorization: Bearer 123456" \
    -H "Content-Type: application/json" \
    -d @feed.json@
```

### [Get Feeds favorite current user](https://docs.frm.fm/#/Feeds?id=get-feeds-favorite-current-user) <a href="#get-feeds-favorite-current-user" id="get-feeds-favorite-current-user"></a>

### &#x20;<a href="#get-feeds-favorite-current-user" id="get-feeds-favorite-current-user"></a>

This endpoint retrieves all favorite feeds from the current user. The results returned are paginated.

HTTP Request: `GET https://api.phuquoc.dog/feeds/favorite`

Special Query Parameters

| Parameter | Default | Description                                           |                         Example |
| --------- | :-----: | ----------------------------------------------------- | ------------------------------: |
| page      |  false  | Return results pertaining to that page                |                          page=3 |
| fields    |  false  | Allows you to return only attributes that you require | fields=artworkId,createdOn,name |
| limit     |    10   | The number of results returned per page               |                        limit=50 |

Sample request:

```
curl  -H "Content-Type: application/json" -X GET ${HOST}/feeds/favorite?limit=2&page=1
```

Sample response:

```
{
    "data": [
        {
            "id": 5360,
            "url": "http://vsco.co/media/593219df38ad40689e59b8bf?share=MTQ5NjQ1NTY2MA%3D%3D&display_rotate=enable",
            "thumb": {
                "id": 7201,
                "key": "feedthumbnail/1234444.png",
                "privacy": "public-read",
                "url": "https://cdn.phuquoc.dog/feedthumbnail/eedthumbnail/1234444.png",
                "expires": 1496488111,
                "originalFileName": "PNG.PNG",
                "fileSize": 811830,
                "cdn": "https://cdn.phuquoc.dog/feedthumbnail/eedthumbnail/1234444.png"
            },
            "name": "VSCO - morld",
            "tags": "",
            "thumbWidth": 600,
            "thumbHeight": 450,
            "createdOn": "2021-10-03 11:08:31",
            "updatedOn": null,
            "isPrivate": 0,
            "userFollowing": [
                {
                    "id": 6,
                    "username": "pqd"
                }
            ]
        },
        {
            "id": 3043,
            "url": "http://fast.com",
            "thumb": {
                "id": 4441,
                "key": "feedthumbnail/2de14aa4c3eb6f2a7d497efcf0ae4296.PNG",
                "privacy": "public-read",
                "url": "https://cdn.phuquoc.dog/feedthumbnail/2de14aa4c3eb6f2a7d497efcf0ae4296.PNG",
                "expires": 1484374814,
                "originalFileName": "PNG.PNG",
                "fileSize": 811830,
                "cdn": "https://cdn.phuquoc.dog/feedthumbnail/2de14aa4c3eb6f2a7d497efcf0ae4296.PNG"
            },
            "name": "Internet Speed Test | Fast.com",
            "tags": "",
            "thumbWidth": 600,
            "thumbHeight": 450,
            "createdOn": "2017-01-14 06:20:12",
            "updatedOn": null,
            "isPrivate": 1,
            "userFollowing": [
                {
                    "id": 888,
                    "username": "Tim002"
                },
                {
                    "id": 6,
                    "username": "pqd"
                }
            ]
        }
    ],
    "meta": {
        "pagination": {
            "total": 37,
            "count": 19,
            "per_page": 2,
            "current_page": 5,
            "total_pages": 19,
            "links": {
                "previous": 4,
                "next": 6
            }
        }
    }
}
```
