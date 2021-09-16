# Authentication
In this article you'll learn everything about authenticating with our API.
___
To be able to authenticate with our API you have to generate an access token in your account ([here](https://ratecard.io/app/settings/api)). If you don't have access to the Ratecard account and/or the API settings page please ask the owner/admin nof your account to supply you ewith this token.

<!--
type: tab
title: Bearer Auth
-->

```http
GET https://api.ratecard.io/v1/contacts
Connection: Keep-Alive
Authorization: Bearer <access_token>
Accept: application/json
```

<!--
type: tab
title: API Key (Header)
-->

```http
GET https://api.ratecard.io/v1/contacts
Connection: Keep-Alive
Ratecard-AccessToken: <access_token>
Accept: application/json
```

<!--
type: tab
title: API Key (Query Parameter)
-->

```
GET https://api.ratecard.io/v1/contacts?access_token=<access_token>
```

<!-- type: tab-end -->