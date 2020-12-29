# Filtering: Expressions
In this article you'll learn about expressions and the functions used to build them, followed by additional examples for each of the three ways to filter, an endpoint to test (advanced) expressions (without defined properties), and a glossary containing some additional descriptions.

## Expressions
An **expression** in the Ratecard API is a combination of functions, string literals and/or defined properties. Generally these expressions will be found in GET API endpoints that return collections of items such as a list of contacts. If you've read the introduction to filtering you've come to know that these expressions are implemented in three different ways throughout these endpoints. Let's dive deeper into how this all works in our API in order to make it as clear as possible how everything works.

## Logical Functions
Logical functions combine other boolean expressions.

- `and(e, e, [,..., e])` true when all expressions are true; requires at least two expressions.
- `or(e, e, [,..., e])` true when at least one expressions is true; requires at least two expressions.

## Relational Functions
Relational functions compare two or more expressions.

> All relational functions require a defined property (dp) for their first argument (e.g. first_name for contacts). Defined properties will be listed at their respective API endpoints (e.g. `GET /v1/contacts`).

- `equals(dp, e, [,..., e])` true when all expressions are equal to the defined property; requires at least one expression.
- `notEquals(dp, e, [,..., e])` true when all expressions are not equal to the defined property; requires at least one expression.
- `lessThan(dp, e)` true when the defined property is less than the given expression; requires one expression.
- `lessThanOrEqualTo(dp, e)` true when the defined property is less than or equal to the given expression; requires one expression.
- `greaterThan(dp, e)` true when the defined property is greater than the given expression; requires one expression.
- `greaterThanOrEqualTo(dp, e)` true when the defined property is greater than or equal to the given expression; requires one expression.
- `contains(dp, e)` true when the defined property contains given expression; requires one expression.
- `notContains(dp, e)` true when the defined property does not contain given expression; requires one expression.
- `startsWith(dp, e)` true when the defined property starts with given expression; requires one expression.
- `notStartsWith(dp, e)` true when the defined property does not start with given expression; requires one expression.
- `endsWith(dp, e)` true when the defined property does not end with given expression; requires one expression.
- `notEndsWith(dp, e)` true when the defined property does not end with given expression; requires one expression.
- `in(dp, e)` true when the defined property exists within the given expressions; requires one or more expressions.
- `notIn(dp, e)` true when the defined property does exist within given expressions; requires one or more expressions.
- `match(dp, regex)` true when the defined property matches the given regular expression (regex); requires one regular expression.
- `matchAny(dp, regex, [,..., regex])` true when the defined property matches the given regular expressions; requires one or more regular expressions.
- `matchAll(dp, regex, [,..., regex])` true when the defined property matches all of the the given regular expressions; requires one or more regular expression.
- `between(dp, e, e)` true when the defined property is between expression one and two; requires two expressions.
- `notBetween(dp, e, e)` true when the defined property is not between expression one and two; requires two expressions.
- `isNull(dp)` true when dp is null or unset.
- `isNotNull(dp)` true when dp is not null.

### Aliases
Useful when building large expressions to reduce the length of the expression.
- `eq` alias for `equals`
- `ne` alias for `notEquals`
- `lt` alias for `lessThan`
- `le` alias for `lessThanOrEqualTo`
- `gt` alias for `greaterThan`
- `ge` alias for `greaterThanOrEqualTo`
- `ct` alias for `contains`
- `nct` alias for `notContains`
- `sw` alias for `startsWith`
- `nsw` alias for `notStartsWith`
- `ew` alias for `endsWith`
- `new` alias for `notEndsWith`
- `btw` alias for `between`
- `nbtw` alias for`notBetween`

## String functions
String functions that can be applied to strings; given as arguments to relational functions.

> All string functions require a string literal as their parameter (numbers will be interpreted as a string).

- `toUpper(str)` makes a string literal upper case.
- `toLower(str)` makes a string literal lower case.
- `length(str)` transforms a string into an integer representing the its character length.
- `blank(str)` true when the given expression is empty or null.

## Numeric functions
Numeric functions can be applied to numbers; given as arguments to relational functions.

- `ceil(num)` transforms the given number into the the smallest integer greater than or equal to the given number.
- `floor(num)` transforms the given number into the the the largest integer less than or equal to the specified number.
- `round(num, num)` the value of the given number rounded to the nearest integer. Accepts an optional second parameter to determine the decimals.
- `pi()` is pi and adds pi to the expression. It represents the ratio of the circumference of a circle to its diameter, approximately 3.14159.

## Date functions
Date functions can be applied to dates; given as arguments to relational functions.

- `now(str)` returns the current date as it's value; accepts an optional parameter to transform the date or to parse a date.
  - Examples:
    - `now()`
    - `now('2020-12-28')` 
    - `now('-30 day')`
    - `now('+1 month')`

## Database functions
Functions that can be applied directly to defined properties. These functions expose a select few functions from the database to transform the value of the defined properties.

> Database functions only apply to defined properties.

- `length(dp)` transforms a the defined property into an integer representing the its character length.
- `trim(dp)` trims spaces from the edges of the defined property
- `rtrim(dp)` trims spaces from the right side of the defined property
- `ltrim(dp)` trims spaces from the left side of the defined property
- `toUpper(dp)` makes the defined property upper case
- `toLower(dp)` makes the defined property lower case
- `ceil(dp)` transforms the defined property into the smallest integer greater than or equal to the given number.
- `floor(dp)` transforms the defined property into the largest integer less than or equal to the specified number.
- `round(dp)` the value of the defined property rounded to the nearest integer.

## String literal behaviour
- Spaces will be trimmed from the edges of string literals.
- When `true` and `false` are given as a string they will automatically be cast to a boolean.
- When `null` is given as a string it will automatically be cast to null.

## Expression filtering
In this section we dive a little deeper into the expression filtering and go through each of the variants to see how they function and what their limitations are.

> The paragraphs in this section build on top of one another.

### Basic filtering
Basic filters follow a key value pair structure where the value is what's being filtered on and are limited in their functionality. In the background these are mapped to expressions that will eventually be applied to the query resulting in the collection returned. Basic filters use the `equals` and `in` relational functions. The key, property or query paremeter in this context is called the **defined property**. These are specified as query parameters at each endpoint.

Here you can see the forms in which you could apply a basic filter depending on the available query parameters:
```js
// key equals value -> name equals John
<key>=<value> -> name=John
// the property of object equals value -> the user's name equals John
<object>.<property>=<value> -> user.name=John
// key is one of the given values -> name is one of Jane or John
<key>=<value>|<value> -> name=Jane|John
// the property of object is one of the given values -> the user's name is one of Jane or John
<object>.<property>=<value>|<value> -> user.name=Jane|John
```

### Basic expression filtering
Basic expression filters follow a key value pair structure where the value is a **relational function** (rf) without the **defined property** (dp) as the key is the defined property. Relational functions that only take the defined property as an argument (arg) will not accept any arguments. Relational functions can also accept string, numeric & date functions (df).

Let's take the examples from basic filtering and write them in their basic expression form:
```js
name=John -> name=equals('John')
user.name=John -> user.name=equals('John')
name=Jane|John -> name=in('Jane', 'Joe')
user.name=Jane|John -> user.name=in('Jane', 'Joe')
```
Now let's expand on that and match only the users that were created in 2020 with the first name Jane or Joe and last name Doe:
```js
// <dp>=<rf>(<arg1>, <arg2>)&<dp>=<rf>(<arg1>)&<dp>=<rf>(<df>(<arg1>))
first_name=in('Jane', 'Joe')&last_name=equals('Doe')&created_at=greaterThanOrEqualTo(now('2020-01-01'))
```
This can be simplified to the following mixing basic filters and basic expression filters with aliases:
```js
first_name=Jane|Joe&last_name=Doe&created_at=ge(now('2020-01-01'))
```

### Advanced expression filtering
Advanced expression filtering unlocks the full potential of expressions. In the API endpoints this will be possible via the query parameter `filter`. It accepts both logical functions and relational functions. When a relational function is given it essentially functions as a basic expression filter, however the defined property will have to be specified.

Let's take a look at how it works with a simple example where a users email has to contain ratecard:
```js
filter=contains(email, 'ratecard')
// Alternatively:
email=contains('ratecard')
```
As you can see this example can just as well be written as a basic expression filter. So what can we do with an advanced expression filter? Let's say we want to apply 2 filters to one property or we want to match one of the given expression, basic filters don't allow that. 

#### Example 1
Let's take the example with the contains and we want to check if the email contains gmail or outlook:
<!--  
type: tab
title: Expression
-->
```js
or(contains(email, 'gmail'), contains(email, 'outlook'))
// With aliases
or(ct(email, 'gmail'), ct(email, 'outlook'))
```
<!--  
type: tab
title: JSON
-->
```json
{
  "name": "or",
  "arguments": [
    {
      "name": "contains",
      "arguments": [
        "email",
        "gmail"
      ]
    },
    {
      "name": "contains",
      "arguments": [
        "email",
        "outlook"
      ]
    }
  ]
}
```
<!--  
type: tab
title: SQL
-->
```sql 
WHERE email LIKE '%gmail%' OR email LIKE '%outlook%';
```
<!-- type: tab-end -->

#### Example 2
We want all feedback with an NPS above 8 or a score above 8 given in the past month. Additionaly we want to make sure that our score is rounded as it can have decimal values and that the respondent's email ends with our company's domain name (ratecard.io). We also want to ensure the respondent email will not have spaces in it so we trim it.
<!--  
type: tab
title: Expression
-->
```js
and(or(greaterThan(nps, 8), greaterThan(round(score), 8)), endsWith(trim(respondent.email), 'ratecard.io'))
// With aliases
and(or(gt(nps, 8), gt(round(score), 8)), ew(trim(respondent.email), 'ratecard.io'))
```
<!--  
type: tab
title: Json
-->
```json
{
  "name": "and",
  "arguments": [
    {
      "name": "or",
      "arguments": [
        {
          "name": "greaterThan",
          "arguments": [
            "nps",
            8
          ]
        },
        {
          "name": "greaterThan",
          "arguments": [
            "round(score)",
            8
          ]
        }
      ]
    },
    {
      "name": "endsWith",
      "arguments": [
        "trim(respondent.email)",
        "ratecard.io"
      ]
    }
  ]
}
```
<!--  
type: tab
title: SQL
-->
```sql 
WHERE (nps > 8 OR ROUND(score) > 8) 
AND 
TRIM(respondent.email) LIKE '%ratecard.io';
```
<!-- type: tab-end -->

## Test an expression
Test a fake expression and see how our app processes it!

> Defined properties and database functions will not be applied to this test

```yaml http
{
  "method": "get",
  "url": "https://api.ratecard.io/test_expression?filter="
}
```

## Glossary
- `defined property (dp)` is a filterable property that's part of the model that the (basic) filter expression is applied to (e.g. *score* for feedback or *name* for groups). All relational functions require one as their first argument, but can accept more than one (unless they take a single argument).
- `expression` is a combination of functions, string literals and/or defined properties.
  - example 1: `first_name=john`
  - example 2: `first_name=equals('John')`
  - example 3: `filter=equals(trim(first_name), toLower('John'))`
- `regular expression` [(click here)](https://en.wikipedia.org/wiki/Regular_expression)