# Introduction to webhooks
In this article you will learn what Ratecard webhooks are, how they work, and what you can do with them. To start we have two types of webhooks, inbound and outbound. With inbound webhooks you send data to us and with outbound webhooks we send data to you.

## The webhook object
This is the webhook object. It can be fully configured through the API or in our app.

```yaml json_schema
$ref: '../../models/webhook.v1.yaml'
```

> You can find webhooks under API in the top right (user) menu in our app if your role is admin or owner.

## Inbound webhooks
Inbound webhooks are basically a wrap around our API (with predefined or additional behaviour in some cases). They provide a way to integrate with our app or send data to it without making a full integration with the API. The URL property of the webhook will be the URL you or your app will send data to with a `POST` request. The `events` property is called actions in our app as you will perform actions with the webhook when it is inbound.

The URL of the inbound webhook is the same URL as the regular webhooks API endpoint, our API will know the difference between 

## Outbound webhooks
Outbound webhooks send data to an URL you specify based on the events the webhook is subscribed to, which is why we call the `events` property 'subscriptions' in our app. When an event happens e.g. `messages.sent` we will `POST` the relevant data surrounding the message and the event to the URL you've defined.