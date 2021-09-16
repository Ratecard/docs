# Guidelines
This article contains guidelines and information regarding our API.

## Scoping
When creating access tokens scopes have to be selected. These scopes determine which resources may be accessed with the access token. We recommend that only the necessary scopes are selected so no endpoints can be accessed outside of what the token is used for.

## Rate Limits
The Ratecard API currently has one form of limiting which is rate limiting. This is to prevent bad code or high concurrency on the requesting application's end from consuming too many resources. If your application goes over the limit you'll receive a 429 response with the following json body:
```json
{
    "message": "Too Many Attempts."
}
```

### Headers
#### All Responses
The following headers are present on all responses
- `X-RateLimit-Limit`: the number of requests allowed per minute.
- `X-RateLimit-Remaining`: the number of request remaining in before encountering a 429 error.
#### 429 Response
The following headers are only present on 429 responses
- `X-RateLimit-Reset`: the timestamp for when you're allowed to send requests again.
- `Retry-After`: the amount of time in seconds until your application's timeout is revoked.