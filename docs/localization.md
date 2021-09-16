# Localization (new)
In this article you'll learn about localization in the Ratecard API.

This featureset was built to support our customers that work with an international scope and future ambitions in mind. Previously we only supported a limited amount of languages in a non-scalable manner. In future endpoints localization will play a bigger role.

## Requests
In this section you'll learn how to localize requests to the API.

Localizing a request to the API can by done in 2 ways. The first way is prefixing the URI with a locale and the second way is by passing an `Accept-Language` header with a single locale as value. We also support a couple of additional headers.

### URI localization
Localizing the URI can be done by prefixing the API version with a locale:
- Format: `GET https://api.ratecard.io/{locale?}/v1`
- Example: `GET https://api.ratecard.io/de_DE/v1`

### Header localization
