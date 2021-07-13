# Outbound Webhooks: Subscriptions
In this article you'll find all subscriptions for outbound webhooks with an explanation for when they trigger and what they send to the URL specified in the webhook.

> A subscription is an event the webhook is subscribed to. When the word subscriptions is used it means a group of event triggers that the webhook listens for.

> Examples will only show the data relevant to their event. Refer to the linked models to see all the properties.

## About the request
In this section you'll find details regarding the request we send.

### Headers

- `Ratecard-Webhook-Secret` contains the secret of the webhook which can be found by going to the webhook's detail page in the app or by retrieving it from the API.

### Status codes
When the app or service to which we're sending the webhook doesn't return a response with a `2xx` message our webhook service will consider the call as failed. A maximum of 3 attempts will be made to successfully send the webhook call.

### Response time
If it takes longer than 3 seconds before we get a response from your app or service we will also consider the call as failed. 

## Messages
In this section you'll find all message subscriptions. 

> Every message subscription will always have an [message](../../../reference/api/models/message.v1.yaml) object attached to it in the payload.

### Events
<!-- 
type: tab
title: Sent
-->
- Name: `messages.sent`
- Triggers after a message is sent to a recipient
- Does not attach additional data
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "message": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "channel": "email",
      "from": "Ratecard",
      "to": "johndoe@ratecard.io",
      // ...
      "metadata": {
        "send_date": "2020-11-25T09:33:14.000000Z",
        "status": "not_opened",
        // ...
      },
      // ...
    }
  },
  "event": "messages.sent",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Opened
-->
- Name: `messages.opened`
- Triggers when the recipient views the message they've received
- Can't be triggered for text (sms) messages
- Won't trigger if the recipient blocks emails in their mail client
- Does not attach additional data
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "message": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "channel": "email",
      "from": "Ratecard",
      "to": "johndoe@ratecard.io",
      // ...
      "metadata": {
        "send_date": "2020-11-25T09:33:14.000000Z",
        "status": "opened",
        "time_till_status": 150,
        "views": 2,
        "first_view_date": "2020-11-25T09:33:14.000000Z",
        "time_to_open": 150,
        "last_view_date": "2020-11-25T09:33:14.000000Z",
        // ...
      },
      // ...
    }
  },
  "event": "messages.opened",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Clicked
-->
- Name: `messages.clicked`
- Triggers when a recipient has clicked on the review url in the message they received
- Does not attach additional data
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "message": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "channel": "email",
      "from": "Ratecard",
      "to": "johndoe@ratecard.io",
      // ...
      "metadata": {
        "send_date": "2020-11-25T09:33:14.000000Z",
        "status": "clicked",
        "time_till_status": 300,
        "views": 2,
        "first_view_date": "2020-11-25T09:33:14.000000Z",
        "time_to_open": 150,
        "last_view_date": "2020-11-25T09:33:14.000000Z",
        "clicks": 2,
        "first_click_date": "2020-11-25T09:33:14.000000Z",
        "time_to_click": 150,
        "last_click_date": "2020-11-25T09:33:14.000000Z",
        // ...
      },
      // ...
    }
  },
  "event": "messages.clicked",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- type: tab-end -->

## Feedback
In this section you'll find all feedback subscriptions.

> Every feedback subscription will always have an [feedback](../../../reference/api/models/feedback.v1.yaml) object attached to it in the payload.

### Events

<!-- 
type: tab
title: Created
-->
- Name: `feedback.created`
- Triggers when you new feedback is created for the first time
- Does not attach additional data
- Answers could be empty as sometimes feedback items get created before a recipient fills in any answers
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "review": true,
      "anonymous": true,
      // ...
      "respondent": {
        "id": "ea10916d-0684-4624-9d07-d341193554cf",
        "first_name": "John",
        "last_name": "Doe",
        "email": "johndoe@example.com",
        "phone": "612345678"
      },
      "form": {
        "id": "ea10916d-0684-4624-9d07-d341193554cf",
        "name": "My Form"
      },
      "answers": [
        {
          "question_id": "ea10916d-0684-4624-9d07-d341193554cf",
          "required": true,
          "hidden": false,
          "title": "How would you rate Ratecard?",
          "type": "rating",
          "value": 9
        }
      ],
      // ...
      "score": 8.5,
      "nps": 9,
      "duration": 300,
      // ...
      "created_at": "2020-11-25T09:33:14.000000Z",
      "updated_at": "2020-11-25T09:33:14.000000Z",
      "completed_at": "2020-11-25T09:33:14.000000Z"
    }
  },
  "event": "feedback.created",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Updated
-->
- Name: `feedback.updated`
- Triggers when existing feedback is updated/completed
- Does not attach additional data
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "review": true,
      "anonymous": true,
      // ...
      "respondent": {
        "id": "ea10916d-0684-4624-9d07-d341193554cf",
        "first_name": "John",
        "last_name": "Doe",
        "email": "johndoe@example.com",
        "phone": "612345678"
      },
      "form": {
        "id": "ea10916d-0684-4624-9d07-d341193554cf",
        "name": "My Form"
      },
      "answers": [
        {
          "question_id": "ea10916d-0684-4624-9d07-d341193554cf",
          "required": true,
          "hidden": false,
          "title": "How would you rate Ratecard?",
          "type": "rating",
          "value": 9
        }
      ],
      // ...
      "score": 8.5,
      "nps": 9,
      "duration": 300,
      // ...
      "created_at": "2020-11-25T09:33:14.000000Z",
      "updated_at": "2020-11-25T09:33:14.000000Z",
      "completed_at": "2020-11-25T09:33:14.000000Z"
    }
  },
  "event": "feedback.updated",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Received
-->
- Name: `feedback.received`
- Triggers when you receive new feedback
- Does not attach additional data
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "review": true,
      "anonymous": true,
      // ...
      "respondent": {
        "id": "ea10916d-0684-4624-9d07-d341193554cf",
        "first_name": "John",
        "last_name": "Doe",
        "email": "johndoe@example.com",
        "phone": "612345678"
      },
      "form": {
        "id": "ea10916d-0684-4624-9d07-d341193554cf",
        "name": "My Form"
      },
      "answers": [
        {
          "question_id": "ea10916d-0684-4624-9d07-d341193554cf",
          "required": true,
          "hidden": false,
          "title": "How would you rate Ratecard?",
          "type": "rating",
          "value": 9
        }
      ],
      // ...
      "score": 8.5,
      "nps": 9,
      "duration": 300,
      // ...
      "created_at": "2020-11-25T09:33:14.000000Z",
      "updated_at": "2020-11-25T09:33:14.000000Z",
      "completed_at": "2020-11-25T09:33:14.000000Z"
    }
  },
  "event": "feedback.received",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Closed
-->
- Name: `feedback.closed`
- Triggers when a user in your account closes an feedback item
- Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      // ...
      "closed": true,
      // ...
    },
    "user": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    }
  },
  "event": "feedback.closed",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Reopened
-->
- Name: `feedback.reopened`
- Triggers when a user in your account reopens an feedback item
- Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      // ...
      "closed": false,
      // ...
    },
    "user": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    }
  },
  "event": "feedback.reopened",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Assigned
-->
- Name: `feedback.assigned`
- Triggers when a user in your account gets assigned to an feedback item
- Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      // ...
      "assignee": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    },
      // ...
    },
    "user": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    }
  },
  "event": "feedback.assigned",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Replied
-->
- Name: `feedback.replied`
- Triggers when a user in your account replies to an feedback item
- Attaches the subject and message of the reply as properties to the payload
- Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
- Has been sent to the contact that gave the feedback
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "reply": {
      "subject": "My reply",
      "body": "This is a reply.",
    },
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      // ...
      "respondent": {
        "id": "ea10916d-0684-4624-9d07-d341193554cf",
        "first_name": "John",
        "last_name": "Doe",
        "email": "johndoe@example.com",
        "phone": "612345678"
      },
      // ...
    },
    "user": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    }
  },
  "event": "feedback.replied",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Noted
-->
- Name: `feedback.noted`
- Triggers when a user in your account adds a note to an feedback item
- Attaches the subject and message of the note as properties to the payload
- Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
- Is internal
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "note": {
      "subject": "My note",
      "body": "This is a note.",
    },
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      // ...
    },
    "user": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    }
  },
  "event": "feedback.noted",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- 
type: tab
title: Archived
-->
- Name: `feedback.archived`
- Triggers when a user in your account archives an feedback item
- Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "webhook": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My webhook"
  },
  "account": {
    "id": "ea10916d-0684-4624-9d07-d341193554cf",
    "name": "My account"
  },
  "payload": {
    "feedback": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      // ...
      "status": "archived"
      // ...
    },
    "user": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    }
  },
  "event": "feedback.archived",
  "created_at": "2020-11-25T09:33:14.000000Z",
  "updated_at": "2020-11-25T09:33:14.000000Z"
}
```
<!-- type: tab-end -->