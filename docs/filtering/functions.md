# Filtering: Functions
In this article you'll find all the functions that can be used in basic and advanced expression filtering.

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
- `notBetween` true when the defined property is not between expression one and two; requires two expressions.
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

- `toUpper(str)` makes a string lieral upper case.
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
  - `now()`, `now('2020-12-28')` `now('-30 day')`, `now('+1 month')`

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
- `round(dp)` the value of thedefined property rounded to the nearest integer.

## String literal behaviour
- Spaces will be trimmed from the edges of string literals.
- When `true` and `false` are given as a string they will automatically be cast to a boolean.
- When `null` is given as a string it will automatically be cast to null.

## Test an expression
Test a fake expression and see how our app processes it!

> Defined properties and database functions will not be applied to this test

```yaml http
{
  "method": "get",
  "url": "https://api.ratecard.io/test_expression?filter="
}
\```

## Glossary
- `defined property (dp)` is a filterable property that's part of the model that the (basic) filter expression is applied to (e.g. *score* for feedback or *name* for groups). All relational functions require one as their first argument, but can accept more than one (unless they take a single argument).
- `expression` is a combination of functions, string literals and/or defined properties.
  - example 1: `first_name=john`
  - example 2: `first_name=equals('John')`
  - example 3: `filter=equals(trim(first_name), toLower('John'))`
- `regular expression` [(click here)](https://en.wikipedia.org/wiki/Regular_expression)