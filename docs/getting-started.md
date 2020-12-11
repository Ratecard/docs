# Getting Started

## Introduction
>Ratecard API is a paid feature. [Register](http://ratecard.io/register?source=API-docs) for a free trial or upgrade to a paid plan to make use of it.

Ratecard API lets you collect feedback and reviews on autopilot, and is used for:
- Experience Management
- Performance Management
- Reputation Management


## Authorization

Generate an access token within within your account ([here](https://ratecard.io/app/settings/api)), or ask the owner/admin of your account to supply you with this token. Apply an authorization header with the token to get access to your account(s) within the scope(s) defined for this particular token.

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
title: API Key (Query Parameter)
-->

```
GET https://api.ratecard.io/v1/contacts?access_token=<access_token>
```

<!--
type: tab
title: API Key (Auth Header)
-->

```http
GET https://api.ratecard.io/v1/contacts
Connection: Keep-Alive
Ratecard-AccessToken: <access_token>
Accept: application/json
```

<!-- type: tab-end -->