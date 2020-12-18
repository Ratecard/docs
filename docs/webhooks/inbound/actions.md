# Actions
In this article you'll find all actions for inbound webhooks with the data you're expected to send to each.

## Structure
In this section you'll see the structure of the inbound webhooks. 

Each individual action will be an object with an action property telling our webhook how to process the payload property that is also required. If an action is given without payload, vise versa, or when one of them is empty we will reject the data. The payload property will be an object in most cases (tab 1), but some actions allow an array of objects in their payload such as the contact and user create actions to process a batch of data (tab 2).

The inbound webhooks also support multi actions (tab 3). Multi actions are useful when limiting the amount of requests sent or to handle multiple things at once.

_View the examples to see how each works_

<!-- 
type: tab
title: Single action
-->
```json
{
  "action": "<action_name>",
  "payload": {
    // Object that the action requires
  }
}
```
<!-- 
type: tab
title: Single action (batch)
-->
```json
{
  "action": "<action_name>",
  "payload": [
    {
      // Array of objects that the action requires
    }
  ]
}
```
<!-- 
type: tab
title: Multi action
-->
```json
{
  "actions": [
    {
      "action": "<action_name>",
      "payload": {
        // Object that the action requires
      }
    },
    {
      "action": "<action_name>",
      "payload": [
        {
          // Array of objects that the action requires
        }
      ]
    }
  ]
}
```
<!-- 
type: tab
title: Examples
-->
Single action to add John Doe to My Group:
```json
{
  "action": "contacts.create",
  "payload": {
    "first_name": "John",
    "last_name": "Doe"
    "email": "johndoe@example.com",
    "groups": [
      { "name": "My Group" }
    ]
  }
}
```
Single action to add John Doe and Jane Doe to My Group:
```json
{
  "action": "contacts.create",
  "payload": [
    {
      "first_name": "John",
      "last_name": "Doe"
      "email": "johndoe@example.com",
      "groups": [
        { "name": "My Group" }
      ]
    },
    {
      "first_name": "Jane",
      "last_name": "Doe"
      "email": "janedoe@example.com",
      "groups": [
        { "name": "My Group" }
      ]
    }
  ]
}
```
Multi action to add John Doe to My Group and anonymize Jane Doe:
```json
{
  "actions": [
    {
      "action": "contacts.create",
      "payload": {
        "first_name": "John",
        "last_name": "Doe"
        "email": "johndoe@example.com",
        "groups": [
          { "name": "My Group" }
        ]
      }
    },
    {
      "action": "contacts.anonymize",
      "payload": [
        "janedoe@example.com"
      ]
    }
  ]
}
```
<!-- type: tab-end -->

## Contacts
In this section you'll find all contact actions

### Events
<!-- 
type: tab
title: Create
-->
Add one contact to your account
- Name: `contacts.create`
- Payload is the same object as the add a new contact API endpoint ([view endpoint](../../../reference/api/openapi.v1.yaml/paths/~1contacts/post))
```json
{
  "action": "contacts.create",
  "payload": {
    "first_name": "John",
    "last_name": "Doe"
    "email": "johndoe@example.com",
    "groups": [
      { "name": "My Group" }
    ]
  }
}
```
<!-- 
type: tab
title: Create (batch)
-->
Add one or more contacts to your account
- Name: `contacts.create`
- Payload is an array that accepts contact objects in the same format as the add a new contact API endpoint ([view endpoint](../../../reference/api/openapi.v1.yaml/paths/~1contacts/post))
```json
{
  "action": "contacts.create",
  "payload": [
    {
      "first_name": "John",
      "last_name": "Doe"
      "email": "johndoe@example.com",
      "groups": [
        { "name": "My Group" }
      ]
    }
  ]
}
```
<!-- 
type: tab
title: Anonymize
-->
Make one or more contacts anonymous in your account. Once anonymous you will no longer see their contact info (e.g.: name, email) appear in our app, api and public company profiles.

- Name: `contacts.anonymize`
- Payload is an array
- Accepts:
  - Contact email
  - Contact id
  - Object with contact external id and type (e.g. for synced contacts with Bullhorn or Carerix)
```json
{
  "action": "contacts.anonymize",
  "payload": [
    "johndoe@example.com",
    "ea10916d-0684-4624-9d07-d341193554cf",
    {
      "external_id": "123456789",
      "external_type": "Contact"
    }
  ]
}
```
<!-- 
type: tab
title: Unsubscribe
-->
Unsubscribe one or more contacts from your account. Once unsubscribed they will no longer receive emails or text (sms) messages.

- Name: `contacts.unsubscribe`
- Payload is an array
- Accepts:
  - Contact email
  - Contact id
  - Object with contact external id and type (e.g. for synced contacts with Bullhorn or Carerix)
```json
{
  "action": "contacts.unsubscribe",
  "payload": [
    "johndoe@example.com",
    "ea10916d-0684-4624-9d07-d341193554cf",
    {
      "external_id": "123456789",
      "external_type": "Contact"
    }
  ]
}
```
<!-- 
type: tab
title: Unsubscribe (group)
-->
Unsubscribe one or more contacts from one or more groups in your account. Once unsubscribed they will no longer receive emails or text (sms) messages from the group(s) they're unsubscribed from.

- Name: `contacts.unsubscribe`
- Payload is an object with 2 properties: `contacts` and `groups`
- Contacts accepts:
  - Contact email
  - Contact id
  - Object with contact external id and type (e.g. for synced contacts with Bullhorn or Carerix)
- Groups accepts:
  - Group email
  - Group id
  - Group public id (which is part of the email)

```json
{
  "action": "contacts.unsubscribe_group",
  "payload": {
    "contacts": [
      "johndoe@example.com",
      "ea10916d-0684-4624-9d07-d341193554cf",
      {
        "external_id": "123456789",
        "external_type": "Contact"
      }
    ],
    "groups": [
      "Y62lTnv3",
      "Y62lTnv3@group.ratecard.io",
      "ea10916d-0684-4624-9d07-d341193554cf"
    ]
  }
}
```
<!-- 
type: tab
title: Delete
-->
Delete one or more contacts from your account. 

- Name: `contacts.delete`
- Payload is an array
- Accepts:
  - Contact email
  - Contact id
  - Object with contact external id and type (e.g. for synced contacts with Bullhorn or Carerix)
```json
{
  "action": "contacts.delete",
  "payload": [
    "johndoe@example.com",
    "ea10916d-0684-4624-9d07-d341193554cf",
    {
      "external_id": "123456789",
      "external_type": "Contact"
    }
  ]
}
```
<!-- type: tab-end -->