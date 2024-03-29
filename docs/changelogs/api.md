# API Changelog
All notable changes to the API will be documented in this file.

The format is partially based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this changelog adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## \[1.2.0] - 2021-09-16
### Added
- Localization

### Changed
- Query logic to give a significant speed boost to feedback and message endpoints.

### Fixed
- User & Team answers containing complete model data when they should only show id, name & email.
- API error responses causing redirect to documentation instead of returning JSON.

## \[1.1.2] - 2021-08-31
### Fixed
- Fallback to default value when a smart field value couldn't resolve to an object.

## \[1.1.1] - 2021-07-12
### Changed
- Reminders are now excluded from message statistics.
- Form questions with multiple users or teams are now mapped correctly.
- API & webhook source linking will not happen anymore if an object already has a source when being created/updated.
- Contact last name no longer required when creating/updating contacts.

### Fixed
- Event source not being linked when a group contact is created.
- Test messages showing up in message statistics.
- Group filters ignoring smart field names
  - Group filter only worked on base fields, before. Now it checks for smart field names, e.g. "Feedback (Y/N)", instead of custom tag names, e.g. "feedback".
- Matrix question mapping

## \[1.1.0] - 2021-06-08
### Added
- Campaign relation to [Feedback](../../reference/api/models/feedback.v1.yaml)
- Message relation to [Feedback](../../reference/api/models/feedback.v1.yaml)
- Resource expansion via the `expand` query parameter.
  - Example: `/feedback?expand=respondent` to get the full respondent relation
  - Expandable models and properties:
    - [Feedback](../../reference/api/models/feedback.v1.yaml)
      - `respondent`
      - `campaign`
      - `message`
      - `assignee`
      - `form`
    - [Message](../../reference/api/models/message.v1.yaml)
      - `feedback`
      - `campaign`
      - `connected_user`
      - `form`
      - `connectable`
      - `recipient`
  - Nested expansion
    - Example: `/feedback?expand=messages,messages.campaign` to get the entire message with it's associated campaign related to the feedback item
- Extended expression filtering for expandable relations
  - See: [List all feedback](/reference/api/openapi.v1.yaml/paths/~1feedback/get) for a list of additional query paremeters that can also be used for expression filtering
  - More endpoints will soon be updated to support this
- JSON support for `GET` endpoints
  - `fields`, `except`, `expand` & `sort` can all be given as a comma separated string or array
  - `page` & `show` can both be given as a number or numeric string
  - Expressions can be added with the following notations in JSON
    - Dot: `{ "respondent.name": "John Doe" }`
    - Underscore: `{ "respondent_name": "John Doe" }`
    - Object: `{ "respondent": { "name": "John doe" } }`
  - Additionally the `GET` query parameters also support multiple input types now
    - Dot: `respondent.name=John+Doe`
    - Underscore: `respondent_name=John+Doe`
    - Object: `respondent[name]=John+Doe`
- Randomized sorting with `sort=rand()`
  - Could be used for an UI element that randomly shows a set of items.

### Changed
- Answers for feedback will now be properly mapped to objects
  - Previously answers of type `multiple_choice` and `matrix` would return as a json encoded string
- Backend configuration and routes will now be cached which could result in a minor performance gain per request

### Fixed
- Some expressions with wrong configuration not working as intended

## \[1.0.17] - 2021-06-07
### Added
- Notification settings for accounts

## \[1.0.16] - 2021-05-28
### Added
- User default settings to the user creation endpoint.
  - These default settings can be configured in the account settings in the Ratecard app.
  - Newly created users will now have these defaults instead of the previous system defaults, unless they're given upon creation in the JSON.

## \[1.0.15] - 2021-05-27
### Changed
- Event statuses regarding contact updates were too strict.
  - The status will now always be contact updated when a call is succesful.

## \[1.0.14] - 2021-05-17
### Fixed
- Webhooks not being created/sent due to a version mistmatch with an underlying library.

## \[1.0.13] - 2021-05-06
### Added
- Campaign pauses / flags
  - When a contact is added to a group with active campaigns a message can be scheduled; when the campaign exceeds a flag limit it will be paused and mails regarding the pause will be sent to all relevant parties.

## \[1.0.12] - 2021-04-14
### Added
- Feedback and message list endpoints for forms.
- Expressions for feedback answers in the feedback list(s).

### Changed
- Feedback lists now include approved feedback in the results.

### Fixed
- Incorrect not found messages.

## \[1.0.11] - 2021-03-30
### Changed
- Sources can now be edited for contacts and groups.
  - When not specified `API` will be the fallback source.
- Precision for auto campaign scheduling when adding contacts to a group
- Behaviour for message resources
  - Now more performant when fields are excluded

### Fixed
- Incorrect source mapping for Groups & Contacts.
- Triggers not getting removed from schedule when a contact is deleted or removed from a group.
- Empty object returning where null should be in the recipient email field when it is not present in a message.

## \[1.0.10] - 2021-03-22
### Added
- Expressions for Reports
- Sorting for Reports
- `source` property to contacts and groups
  - A source represents the origin of the data (e.g. Dynamics CRM)
- `source`, `external_id` and `external_type` properties of contact can now be added/updated
  - Source can also be added/updated for the a group 

- `external_id` identifier of the contact in another system _(e.g. 123456 in Carerix)_
- `external_type` type of the contact in another system _((e.g. "Candidate" in Carerix)_

### Changed
- Behaviour update for the except and fields query parameters for reports `GET` endpoints to speed up the API response time when fields that contain sub queries are excluded from the response
  - Previously everything was still executed on the background

### Fixed
- `protection_enabled` property of Reports returning an integer whilst it should be returned as a boolean
- Smart field mapper not auto mapping smart fields

## \[1.0.9] - 2021-03-16
### Added
- Account update endpoint.
  - `PUT: /v1/accounts/{id}`.
  - You can now fully update your account as it is shown in the `GET` responses minus the automatically generated or static variables.
- The `brand_color` and `accent_color` of the account have been added to the `branding` object in a new `colors` object to the Account model.

### Changed
- All images will now be uploaded to the CDN.
- Image URLs returned by the API can now contain CDN URLs.
  - `Account`, `Campaign`, `Form` and `User` `GET` responses will contain CDN image URLs if their files were uploaded to the CDN.

### Fixed
- Image validation requiring images to be exactly 2048KB.
  - This has now been corrected to be the maximum image size for image file uploads.
  - This did not affect base64 image strings.
- Error saving user when an image as a file was uploaded.
  - `profile_picture` was not extracted correctly from the input data.
  - This did not affect base64 `profile_picture` uploads.
- `uuid` having null as value in campaign `GET` responses

## \[1.0.8] - 2021-03-04
### Fixed
- 500 errors caused by null values for profile pictures on the user
s `POST` and `UPDATE` endpoints. Null values will now be ignored and validation works as intended again.
- `profile_picture` on user results always showing a `ratecard.io` URL when it should be a `cdn.ratecard.info` URL.

## \[1.0.7] - 2021-03-01
### Added
- Support for `assigned_to` and `is_closed` report filters.
  - These can currently only be configured in the app

## \[1.0.6] - 2021-02-26
### Added
- Webhook call history
  - List of all webhook calls
  - List of webhook calls per webhook
  - Retrieve an webhook call
  - Retrieve an webhook call belonging to a webhook

### Changed
- The `message` property of replies and notes for feedback items has been renamed to `body` to follow the recent changes to the webhooks.
- Updated the webhook call with an exception property
  - Contains error messages that are thrown or caught by our systems

## \[1.0.5] - 2021-02-24
### Changed
- The outbound webhooks `feedback.noted` and `feedback.replied` their payloads have been updated to differentiate them from the message object other payloads contain.
  - `feedback.noted` previously had a property `subject` and `message` in the payload object. This is now replaced by a property called `note` containing the properties `subject` and `body` (previously `message`)
  - `feedback.replied` previously had a property `subject` and `message` in the payload object. This is now replaced by a property called `reply` containing the properties `subject` and `body` (previously `message`).

### Fixed
- Error thrown when generating embed URLs for objects in outbound webhook payloads.

## \[1.0.4] - 2021-02-15
### Added
- The profile picture attribute for the user model now accepts images in the form of a base64 string too

### Fixed
- Report error caused by a missing share type

## \[1.0.3] - 2021-02-12
### Added
- Profile picture file upload

### Changed
- Swapped out the old smart field mapper on the contacts endpoints with the new one

## \[1.0.2] - 2021-02-11
### Added
- API source will now be added to newly created contacts

### Changed
- Reworked the smart field mapper to be more flexible and accurate

### Fixed
- Newly created users not being added to the account they should belong to
- Smart field error on the group contact endpoint

## \[1.0.1] - 2021-02-10
### Fixed
- Missing type check causing errors when adding contacts with smart fields through the group contact endpoint(s)