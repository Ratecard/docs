# Subscriptions
In this article you'll find all subscriptions for outbound webhooks with an explanation for when they trigger and what they send to the URL specified in the webhook.

> A subscription is an event the webhook is subscribed to. When the word subscriptions is used it means a group of event triggers that the webhook listens for.

## Messages
In this section you'll find all message subscriptions. 

> Every message subscription will always have an [message](../../../reference/api/models/message.v1.yaml) object attached to it in the payload.

- `messages.sent`
  - Triggers after a message is sent to a recipient
  - Does not attach additional data
- `messages.opened`
  - Triggers when the recipient views the message they've received
  - Can't be triggered for text (sms) messages
  - Won't trigger if the recipient blocks emails in their mail client
  - Does not attach additional data
- `messages.clicked`
  - Triggers when a recipient has clicked on the review url in the message they received
  - Does not attach additional data

## Feedback
In this section you'll find all feedbac subscriptions.

> Every feedback subscription will always have an [feedback](../../../reference/api/models/feedback.v1.yaml) object attached to it in the payload.

- `feedback.received`
  - Triggers when you receive new feedback
  - Does not attach additional data
- `feedback.closed`
  - Triggers when a user in your account closes an feedback item
  - Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
- `feedback.reopened`
  - Triggers when a user in your account reopens an feedback item
  - Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
- `feedback.assigned`
  - Triggers when a user in your account reopens an feedback item
  - Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
- `feedback.replied`
  - Triggers when a user in your account reopens an feedback item
  - Attaches the subject and message of the reply as properties to the payload
  - Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
  - Has been sent to the contact that gave the feedback
- `feedback.noted`
  - Triggers when a user in your account reopens an feedback item
  - Attaches the subject and message of the note as properties to the payload
  - Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload
  - Is internal
- `feedback.archived`
  - Triggers when a user in your account reopens an feedback item
  - Attaches the _id_, _name_, and _email_ of the user that performed the action to a property named _user_ in the payload