# Localization (new)
In this article you'll learn about localization in the Ratecard API.

This featureset was built to support our customers that work with an international scope and future ambitions in mind. Previously we only supported a limited amount of languages in a non-scalable manner. In future endpoints localization will play a bigger role.

> **What benefit does localizing have?**
> 
> Localizing your API requests tells the API that all data you send and want to work with is in a specific language or region. The API will then be able to make associations based on the locale and automatically translate responses if said translation or data matching the locale is available.
>
> This is especially beneficial to applications working on a multi-lingual or multi-national scope.

## URI Localization
Localizing the URI can be done by prefixing the API version with a locale:
- Format: `GET https://api.ratecard.io/{locale?}/v1`
- Example: `GET https://api.ratecard.io/de_DE/v1`

## Header Localization
> In the future more headers will be added when localization functionality is implemented more broadly throughout the application.
#### `Accept-Language`
The Accept Language header is used as a substitute for the localized URI. Localized URIs take precedence over this header, so you should only use it when you're not localizing the URI.
- Example: `Accept-Language: en_US`

#### `Ratecard-Locale-Filters`
Locale filters are used to tell the API to only return list data that matches with the current locale, language and/or country. This currently applies to feedback and message endpoints.

##### Options
<!-- 
type: tab
title: Locale
-->
```
Ratecard-Locale-Filters: locale
```
Returns list data matching exact locale.

If you use this filter on the feedback list endpoint and your current locale is `es_ES: Spanish (Spain)` you will only see feedback given in Spanish in Spain.
<!-- 
type: tab
title: Language
-->
```
Ratecard-Locale-Filters: language
```
Return data matching the language of the locale.

If you use this filter on the feedback list endpoint and your current locale is `es_ES: Spanish (Spain)` you will see all feedback given in Spanish and Spanish speaking regions.
<!-- 
type: tab
title: Country
-->
```
Ratecard-Locale-Filters: country
```
Return data matching the country of the locale.

If you use this filter on the feedback list endpoint and your current locale is `es_ES: Spanish (Spain)` you will see all feedback given in Spain and languages spoken in Spain.
<!-- 
type: tab
title: Language + Country
-->
```
Ratecard-Locale-Filters: country_language
```
Return data matching the language or country of the locale.

If your locale is `es_ES: Spanish (Spain)` you will see all feedback given in Spanish, Spanish speaking regions or Spain and languages spoken in Spain. This is a combination of the language and country options their results.
<!-- type: tab-end -->

## Auto Translation
As part of the new localization features auto translation has been added. The only endpoint support auto translation currently is the feedback list endpoint.

[Read more here](./experimental.md#auto-translate)
