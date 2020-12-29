# Introduction to Filtering
In this article you'll learn about filtering in the Ratecard API. 

Each model in the API has a predefined set of properties that can be filtered on. This can be done in a very basic way by key value pair as a GET parameter in the URL (e.g. `first_name=John`) or via the *filter* parameter to build advanced filters with expressions and functions similar to a MySQL or SQL WHERE clause with a function like syntax (e.g. `filter=equals(first_name, 'John'))`):

## Basic Filtering
Basic filtering is the most simple way to filter data in the API by key value pair(s) in the URL to match one or more properties of the model. For example we retrieve John and Jane Doe from the list of contacts.

```js
/contacts?first_name=John|Jane&last_name=Doe
```

Breaking down the example we can see that we use a pipe (vertical bar) between John and Jane (comma can also be used when the pipe is not present). This tells the API we want to use an `in` condition, meaning that the first name has to be either John or Jane in this case. For the last name we only want *Doe*, which translates to an `equals` condition because we want it to match the exact value.

## Basic expression filtering
Basic expression filtering extends the basic filters with functions. For example we want to retrieve feedback that was created between today and 30 days ago:

```js
/feedback?created_at=between(now(), now('-30 day'))
```

Breaking down the example we see the `between` conditional function being used with 2 arguments. Let's take a look at the between function first. In a regular filter expression it would take 3 arguments, but when used in a basic expression filter the first argument will be the property, which is `created_at` in this case (this goes for all other functions as well). The second and third arguments are both the `now` function. This function returns the current date, which can optionally take an argument to modify the date. It can only be used as an argument of a conditional function.

As an additional example let's turn the first example into a basic filter expression:
```js
/contacts?first_name=in('John', 'Jane')&last_name=equals('Doe')
```

[See all expressions]('./expressions.md')

## Advanced Expression Filtering
If you are familiar with query languages such as MySQL it will essentialy be building a WHERE clause when building a full filter expression. Advanced expression filters use the `filter` parameter in the URL. Let's go through a few examples.

Example 1, we want all feedback with a score that's greater than 8 given by people with Dutch or English as their form language:
```js
/feedback?filter=and(greaterThan(score, 8), in(locale, 'nl', 'en'))
/feedback?filter=and(gt(score, 8), in(locale, 'nl', 'en'))
```

Example 2, we want all messages with feedback that have a score thats greater or equal to 9 connected to johndoe@example.com or janedoe@example.com
```js
/messages?filter=and(equals(metadata.status, 'feedback'), greaterThanOrEqualTo(feedback.score, 9), in(connected_user.email, 'johndoe@example.com', 'janedoe@example.com'))
/messages?filter=and(eq(metadata.status, 'feedback'), ge(feedback.score, 9), in(connected_user.email, 'johndoe@example.com', 'janedoe@example.com'))
```

[See all expressions]('./expressions.md')

## Filtering on Smart Fields
Smart fields provided a unique challenge when building the expression filters, especially with regards to performance and their dynamic nature. The only endpoint that currently supports smart field filters is the group contact endpoint. 

> Smart field filters are currenctly available in basic (expression) filter format only. This is subject to change in the future.

Let's take a look at an example contact with smart fields:
```json
{
  "id": "ea10916d-0684-4624-9d07-d341193554cf",
  "first_name": "John",
  "last_name": "Doe",
  "email": "johndoe@ratecard.io",
  // ...
  "smart_fields": {
    "owner": {
      "id": "ea10916d-0684-4624-9d07-d341193554cf",
      "name": "John Doe",
      "email": "johndoe@ratecard.io"
    },
    "jobTitle": "Accountant",
    "region": "Amsterdam"
  },
  //...
}
```
If this contact was in a group of 5000 contacts it would be hard to find them without knowing their basic info, but what if we knew their smart field values, then we can narrow our search down like so:
```js
/contacts?smart_fields.owner=endsWith('@ratecard.io')&smart_fields.jobTitle=Accountant&region=Amsterdam
```