# Documentation changelog
All notable changes to the documentation will be documented in this file.

The format is partially based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), but will not follow semantic versioning as it will list the changes made to the documentation on the date thereof.

## 2021-03-09
### Fixed
- `public_url`, `embed_url`, `created_at` and `updated_at` columns missing from the Report model
  - Report endpoints have also been updated to now show these properties

## 2021-02-26
### Added
- Webhook call history
  - List of all webhook calls
  - List of webhook calls per webhook
  - Retrieve an webhook call
  - Retrieve an webhook call belonging to a webhook

### Changed
- Updated the feedback model and examples to match changes made to the API.
- Updated the webhook call model to match API changes.

### Fixed
- Feedback for message examples showing as null instead of the possible object.

## 2021-02-24
### Added
- More information regarding the [outbound webhook subscriptions](../webhooks/outbound/subscriptions.md) 
  - Headers
  - Response codes
  - Response time
- Embed URLs to the user, team, group, form and campaign models.

### Changed
- The outbound webhooks `feedback.noted` and `feedback.replied` their payloads have been updated to differentiate them from the message object other payloads contain.
  - `feedback.noted` previously had a property `subject` and `message` in the payload object. This is now replaced by a property called `note` containing the properties `subject` and `body` (previously `message`)
  - `feedback.replied` previously had a property `subject` and `message` in the payload object. This is now replaced by a property called `reply` containing the properties `subject` and `body` (previously `message`).

## 2021-02-15
### Changed
- Profile picture description for the user endpoints

## 2021-02-10
### Changed
- Smart field types now list team_members and departments field types, these are identical to the user and team types