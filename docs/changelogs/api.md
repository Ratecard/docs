# API Changelog
All notable changes to the API will be documented in this file.

The format is partially based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this changelog adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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