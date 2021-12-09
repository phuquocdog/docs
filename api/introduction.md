# Introduction

### [Introduction](https://docs.frm.fm/#/?id=introduction) <a href="#introduction" id="introduction"></a>

Welcome to the Phu Quoc Dog REST API documentation site!

You can use our REST API to access and modify the data within your PQD account. This includes all the information within your artworks, feed and invoices that you can use to import / export data or create integrations with other systems and software that you use.

#### [API Access Control Lists (ACL)](https://docs.frm.fm/#/?id=api-access-control-lists-acl) <a href="#api-access-control-lists-acl" id="api-access-control-lists-acl"></a>

#### &#x20;<a href="#api-access-control-lists-acl" id="api-access-control-lists-acl"></a>

Default to get resource from PQD you need authentication to get token or use api key, then you can use resource see [Auth](https://docs.frm.fm/#/./Auth)

* API key to use GET request method
* Token key to use when we need POST or PUT, DELETE action

Default to get resource from PQD you need authentication to get token or use api key, then you can use resource see [Auth](https://docs.frm.fm/#/./Auth)

* API key to use GET request method
* Token key to use when we need POST or PUT, DELETE action

#### [Retrieving Records](https://docs.frm.fm/#/?id=retrieving-records) <a href="#retrieving-records" id="retrieving-records"></a>

To retrieve one or more records you should issue a GET request to the relevant endpoint.

You must include an API key with every API request. In the following example, replace YOUR\_API\_KEY with your API key.

```
curl -X GET https://api.phuquoc.dog/artworks?key=123456777
```

Requesting from the endpoint root (eg /artworks or /feed) will retrieve a paginated list of records.

If you'd like just a single record you can issue an ?id= parameter (eg /artworks?id=1).

Filtering can also be achieved on most endpoints by adding additional fields into the parameter string (eg /artworks?id=5\&status\_id=3\&filter\_operator=AND).

You can restrict the fields returned by a GET request by issuing a list of only the fields you'd like (eg /artworks?id=5\&fields=id,name,start,end).

#### [Creating / Updating a Record](https://docs.frm.fm/#/?id=creating-updating-a-record) <a href="#creating-updating-a-record" id="creating-updating-a-record"></a>

Generally speaking you should issue a POST to create a new record and a PUT to update an existing record.

However the PQD API is quite forgiving and will allow a new record to be created if a PUT is issued without an ID parameter and a POST to update a record if you supply an ID parameter.

It is currently only possible to create or update one record per request.

#### [Deleting a Record](https://docs.frm.fm/#/?id=deleting-a-record) <a href="#deleting-a-record" id="deleting-a-record"></a>

To delete a record you should issue a DELETE with the ID of the record you wish to delete. Deletion is permanent and cannot be undone.

It is currently only possible to delete one record per request.

#### [Authentication](https://docs.frm.fm/#/?id=authentication) <a href="#authentication" id="authentication"></a>

Regardless of the authentication method you choose, phuquoc.dog expects the Bearer Authentication Token to be included in all API requests to the server.

You can either include the token in a header that looks like the following:

Authorization: Bearer 1234567890

Alternatively you can send the token via a query parameter in the URL like the following:

```
https://api.phuquoc.dog/ENDPOINT?access_token=1234567890
```

If you need some resource do not need authentication by username and password, but you need have a api key access form PQD, contact them to get it once we have you can access like below

```
curl -X GET https://api.phuquoc.dog/artworks?key=xxxxx
```

#### [Version API](https://docs.frm.fm/#/?id=version-api) <a href="#version-api" id="version-api"></a>

Some API required prefix version api, for example use prefix v1,v2 https://api.phuquoc.dog/v1/artworks but I chose method API design google keep no prefix version, if you want to defined version we should chose API Gateway like kong gateway, It will be helper team developer and devops team work better.

In the feature maybe we use Kong Gateway: Its proxy lets you serve multiple versions of the same API and provides reporting on how your users are using different versions. Working out who’s using an old version can then help you form a strategy to phase out deprecated versions.
