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
