---

copyright:
years: 2015, 2023
lastupdated: "2023-08-04"

subcollection: watson-assistant

---

{{site.data.keyword.attribute-definition-list}}

# Expression language methods for actions
{: #expression-methods-actions}

The {{site.data.keyword.conversationshort}} expression language can be used to specify values that are independent of, or derived from, values that are collected in steps or stored in session variables. You can use an expression to define a step condition or to define the value of a session variable.
{: shortdesc}

The Watson Assistant expression language is based on the Spring Expression Language (SpEL), but with some important differences in syntax. For detailed background information about SpEL, see [Spring Expression Language (SpEL)](https://docs.spring.io/spring-framework/docs/5.2.13.RELEASE/spring-framework-reference/core.html#expressions){: external}.
{: note}

You can use SpEL expressions in two ways:

- Defining a step condition. For more information, see [Writing expressions](/docs/watson-assistant?topic=watson-assistant-expressions).
- Assigning a value to a session variable. For more information, see [Using variables to manage conversation information](/docs/watson-assistant?topic=watson-assistant-manage-info).

## Referencing action variables
{: #referencing-action-variables}

An action variable is created implicitly for any step that expects customer input, and the variable is bound to the step. To reference an action variable inside an expression, you must specify the step ID by using the format `${step_id}` (for example, `${step_771}`. To find the step ID for a step, select the step and then look at the end of the URL in your browser.

## Referencing session variables
{: #referencing-session-variables}

Session variables are created explicitly in the **Variables** section of the step. To reference a session variable inside an expression, you must specify the variable ID by using the format `${variable_id}` (for example, `${current_time}`. You can find the variable ID in the list of variables. (For more information, see [Using variables to manage conversation information](/docs/watson-assistant?topic=watson-assistant-manage-info).)

When you are editing an expression, you can type `$` to see a list of variables you can reference. Select a variable from the list to automatically insert the step ID or variable ID.

## Supported data types
{: #supported-data-types}

Expressions can use atomic JSON types (such as `integer`, `string`, `number`, and `boolean`), and compound data types (such as JSON arrays (`[]`) and objects (`{}`). When you specify literal string values, you can use either single (`'`) or double (`"`) quotation marks.

Values that action steps collect from customers use customer response types such as date, time, currency, or percent. These values are stored as JSON objects in the following format:

```json
{
  "system_type": "{system_type}",
  "value": "{value}"
}
```
{: codeblock}

where `{system_type}` is one of the following types:
- `time`
- `percentage`
- `currency`

## Date and Time methods
{: #expression-methods-actions-date-time}

Several methods are available to work with date and time values.

### `now(String timezone)`
{: #expression-methods-actions-now}

The `now()` method returns the current date and time for a specified time zone, in the format `yyyy-MM-dd HH:mm:ss 'GMT'XXX`:


```text
now('Australia/Sydney').
```

In this example, if the current date and time is `2021-11-26 11:41:00`, the returned string is `2021-11-26 21:41:00 GMT+10.00` or `2021-11-26 21:41:00 GMT+11.00` depending on Daylight Saving Time.

The output string format change is applicable to date and time calculation methods as well. For example, if the `<date>` string used is in the format `yyyy-MM-dd HH:mm:ss`, such as when you use the method `today()`, then the output is in the same format (`yyyy-MM-dd HH:mm:ss`). However, if the `<date>` string is in the format `yyyy-MM-dd HH:mm:ss 'GMT'XXX`, such as when you use the method `now()`, then the output is in the format `yyyy-MM-dd HH:mm:ss 'GMT'XXX`.

### `.reformatDateTime(String format)`
{: #expression-methods-actions-dates-reformatDateTime}

Formats date and time strings for output. The parameter is a format string that specifies how the date or time value is formatted. The format string must be specified by using the Java [SimpleDateFormat](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html){: external} syntax.

This method returns a string that is formatted according to the specified format:

- `MM/dd/yyyy` for 12/31/2016
- `h a` for 10pm

To return the day of the week:

- `EEEE` for Tuesday
- `E` for Tue
- `u` for day index (1 = Monday, ..., 7 = Sunday)

For example, this expression returns the value 17:30:00 as `5:30 PM`:

```text
${system_current_date}.reformatDateTime('h:mm a')
```
{: codeblock}

If the input string includes only a time, the default date `1970-01-01` is used in the output. If the input string includes only a date, the default time `12 AM (00:00)` is used.
{: note}

### `.before(String date/time)`
{: #expression-methods-actions-dates-before}

- Determines whether a date and time value is before the specified date and time argument, as in this example:

```text
${system_current_date}.before('2021-11-19')
```

You can compare a date with another date, or a time with another time. You can also compare a time with a date and time value, in which case the date is ignored and only the times are compared. Any other comparisons of mismatched values (for example, comparing a date with a time) return `false`, an exception is logged in `output.debug.log_messages` (which you can see in the assistant preview or in API responses).

### `.after(String date/time)`
{: #expression-methods-actions-dates-after}

- Determines whether the date and time value is after the date and time argument.

### `.sameMoment(String date/time)`
{: #expression-methods-actions-dates-sameMoment}

- Determines whether the date and time value is the same as the date and time argument.

### `.sameOrAfter(String date/time)`
{: #expression-methods-actions-dates-sameOrAfter}

- Determines whether the date and time value is after or the same as the date and time argument.
- Analogous to `.after()`.

### `.sameOrBefore(String date/time)`
{: #expression-methods-actions-dates-sameOrBefore}

- Determines whether the date and time value is before or the same as the date and time argument.

### Date and time calculations
{: #expression-methods-actions-date-time-calculations}

Use the following methods to calculate a date.

| Method                  | Description |
|-------------------------|-------------|
| `<date>.minusDays(_n_)`   | Returns the date of the day _n_ days before the specified date. |
| `<date>.minusMonths(_n_)` | Returns the date of the day _n_ months before the specified date. |
| `<date>.minusYears(_n_)`  | Returns the date of the day _n_ years before the specified date. |
| `<date>.plusDays(_n_)`   | Returns the date of the day _n_ days after the specified date. |
| `<date>.plusMonths(_n_)` | Returns the date of the day _n_ months after the specified date. |
| `<date>.plusYears(n)`  | Returns the date of the day _n_ years after the specified date. |
{: caption="Date calculations" caption-side="bottom"}

where `<date>` is specified in the format `yyyy-MM-dd` or `yyyy-MM-dd HH:mm:ss`.

For example, to get tomorrow's date, specify the following expression:

```text
${system_current_date}.plusDays(1)
```
{: codeblock}

Use the following methods to calculate a time.

| Method                  | Description |
|-------------------------|-------------|
| `<time>.minusHours(_n_)`   | Returns the time _n_ hours before the specified time. |
| `<time>.minusMinutes(_n_)` | Returns the time _n_ minutes before the specified time. |
| `<time>.minusSeconds(_n_)`  | Returns the time _n_ seconds before the specified time. |
| `<time>.plusHours(_n_)`   | Returns the time _n_ hours after the specified time. |
| `<time>.plusMinutes(_n_)` | Returns the time _n_ minutes after the specified time. |
| `<time>.plusSeconds(_n_)`  | Returns the time _n_ seconds after the specified time. |
{: caption="Time calculations" caption-side="bottom"}

where `<time>` is specified in the format `HH:mm:ss`.

For example, to get the time one hour from now, specify the following expression:

```text
 now().plusHours(1)  
```
{: codeblock}

### Working with time spans
{: #expression-methods-actions-time-spans}

To show a response based on whether today's date falls within a certain time span, you can use a combination of time-related methods. For example, if you run a special offer during the holiday season every year, you might want to check whether today's date falls between November 25 and December 24 of this year.

First, define the dates of interest as session variables. In the following start and end date session variable expressions, the date is being constructed by concatenating the dynamic current year value with hardcoded month and day values:

```text
start_date = now().reformatDateTime('Y') + '-12-24'
end_date = now().reformatDateTime('Y') + '-11-25'
```
{: codeblock}

Then, in a step condition, you can indicate that you want to show the response only if the current date falls between the start and end dates that you defined as session variables:

```text
now().after(${start_date}) && now().before(${end_date})
```
{: codeblock}

### `java.util.Date` support
{: #expression-methods-actions-dates-java-util-date}

In addition to the built-in methods, you can use standard methods of the `java.util.Date` class.

For example, to get the date of the day that falls a week from today, you can use the following syntax:

```java
new Date(new Date().getTime() + (7 * (24*60*60*1000L)))
```
{: codeblock}

This expression first gets the current date in milliseconds (since January 1, 1970, 00:00:00 GMT). It also calculates the number of milliseconds in 7 days (`(24*60*60*1000L)` represents one day in milliseconds). It then adds 7 days to the current date. The result is the full date of the day that falls a week from today (for example, `Fri Jan 26 16:30:37 UTC 2018`).

## Number methods
{: #expression-methods-actions-numbers}

These methods help you get and reformat number values.

For information about recognizing numbers in customer responses, see [Choosing a response type](/docs/watson-assistant?topic=watson-assistant-collect-info#choosing-a-response-type).

If you want to change the decimal placement for a number (for example, to reformat a number as a currency value), see the [String format() method](#expression-methods-actions-strings-java-lang-String-format).

### `toDouble()`
{: #expression-methods-actions-numbers-toDouble}

Converts the object or field to the Double number type. You can call this method on any object or field. If the conversion fails, `null` is returned.

### `toInt()`
{: #expression-methods-actions-numbers-toInt}

Converts the object or field to the Integer number type. You can call this method on any object or field. If the conversion fails, `null` is returned.

### `toLong()`
{: #expression-methods-actions-numbers-toLong}

Converts the object or field to the Long number type. You can call this method on any object or field. If the conversion fails, `null` is returned.

To specify a Long number type in a SpEL expression, you must append an `L` to the number to identify it as such (for example, `5000000000L`). This syntax is required for any numbers that do not fit into the 32-bit Integer type. Numbers that are greater than 2^31 (2,147,483,648) or less than -2^31 (-2,147,483,648) are considered Long number types. Long number types have a minimum value of -2^63 and a maximum value of 2^63-1 (or 9,223,372,036,854,775,807).

### Standard math
{: #expression-methods-actions-numbers-standard-math}

Use SpEL expressions to define standard math equations, where the operators are represented by using these symbols:

| Arithmetic operation | Symbol     |
|----------------------|:-----------|
| addition             | `+`        |
| division             | `/`        |
| multiplication       | `*`        |
| subtraction          | `-`        |
{: caption="Standard math" caption-side="bottom"}

### `java.lang.Math()`
{: #expression-methods-actions-numbers-java-lang-math}

You can use the functions of the java.lang.Math class to perform basic numeric operations.

You can use the Class methods, including:

- `max()`:

    ```java
    T(Math).max(${step_297},${step_569})
    ```
    {: codeblock}

- `min()`:

    ```java
    T(Math).min(${step_297},${step_569})
    ```
    {: codeblock}

- `pow()`:

    ```java
    T(Math).pow(${step_297}.toDouble(),2.toDouble())
    ```
    {: codeblock}

See the [java.lang.Math reference documentation](https://docs.oracle.com/javase/7/docs/api/java/lang/Math.html){: external} for information about other methods.

### `java.util.Random()`
{: #expression-methods-actions-numbers-java-util-random}

Returns a random number. You can use any of the following syntax options:

- To return a random Boolean value (`true` or `false`), use `new Random().nextBoolean()`.
- To return a random double number between 0 (included) and 1 (excluded), use `new Random().nextDouble()`
- To return a random integer between 0 (included) and a number you specify, use `new Random().nextInt(_n_)`, where _n_ is 1 greater than the top of the number range you want. For example, if you want to return a random number between 0 and 10, specify `new Random().nextInt(11)`.
- To return a random integer from the full integer value range (-2147483648 to 2147483648), use `new Random().nextInt()`.

For example, you might create step that is executed only for a randomly selected subset of customers. The following step condition would mean that the step has a 50% chance of executing:

```bash
new Random().nextInt(2) == 1
```
{: codeblock}

See the [java.util.Random reference documentation](https://docs.oracle.com/javase/7/docs/api/java/util/Random.html){: external} for information about other methods.

You can also use standard methods of the following classes:

- `java.lang.Byte`
- `java.lang.Integer`
- `java.lang.Long`
- `java.lang.Double`
- `java.lang.Short`
- `java.lang.Float`

## String methods
{: #expression-methods-actions-strings}

These methods help you work with text.

For details about the syntax to use in methods that involve regular expressions, see [RE2 Syntax reference](https://github.com/google/re2/wiki/Syntax){: external}.
{: note}

### `String.append(Object)`
{: #expression-methods-actions-strings-append}

This method appends an input object (as a string) to a string, and returns a modified string.

```text
${step_297}.append('next text')
```
{: codeblock}

### `String.contains(String)`
{: #expression-methods-actions-strings-contains}

This method returns `true` if the action variable or session variable contains a substring, which is useful in conditions.

```text
${step_297}.contains('Yes')
```
{: codeblock}

### `String.endsWith(String)`
{: #expression-methods-actions-strings-endsWith}

This method returns `true` if the string ends with the input substring.

```text
${step_297}.endsWith('?')
```
{: codeblock}

### `String.equals(String)`
{: #expression-methods-actions-strings-equals}

This method returns `true` if the specified string equals the action variable or session variable.

```text
${step_297}.equals('Yes')
```
{: codeblock}

### `String.equalsIgnoreCase(String)`
{: #expression-methods-actions-strings-equals-ignore-case}

This method returns `true` if the specified string equals the action variable or session variable irrespective of case.

```text
${step_297}.equalsIgnoreCase('Yes')
```
{: codeblock}

### `String.extract(String regexp, Integer groupIndex)`
{: #expression-methods-actions-strings-extract}

This method returns a string from the input that matches the specified regular expression group pattern. It returns an empty string if no match is found.

This method is designed to extract matches for different regex pattern groups, not different matches for a single regex pattern. To find different matches, see the [getMatch()](#expression-methods-actions-strings-getMatch) method.
{: note}

In this example, the action variable is saving a string that matches the regex pattern group that you specify. In the expression, two regex patterns groups are defined, each one enclosed in parentheses. Inherent is a third group that is composed of the two groups. This is the first (groupIndex 0) regex group; it matches with a string that contains the full number group and text group. The second regex group (groupIndex 1) matches with the first occurrence of a number group. The third group (groupIndex 2) matches with the first occurrence of a text group after a number group.

```text
${step_297}.extract('([\d]+)(\b [A-Za-z]+)', <n>)
```
{: codeblock}

If action variable contains:

```text
Hello 123 this is 456.
```
{: codeblock}

the results are as follows:

- When `<n>`=`0`, the value is `123 this`.
- When `<n>`=`1`, the value is `123`.
- When `<n>`=`2`, the value is `this`.

### `String.find(String regexp)`
{: #expression-methods-actions-strings-find}

This method returns `true` if any segment of the string matches the input regular expression. You can call this method against a JSONArray or JSONObject element, and it converts the array or object to a string before it makes the comparison.

For example, if the action variable `${step_297}` collects the string `Hello 123456`, then the following expression returns `true`:

```text
${step_297}.find('^[^\d]*[\d]{6}[^\d]*$')
```
{: codeblock}

The condition is `true` because the numeric portion of the input text matches the regular expression `^[^\d]*[\d]{6}[^\d]*$`.

### `String.getMatch(String regexp, Integer matchIndex)`
{: #expression-methods-actions-strings-getMatch}

This method returns a string that matches the occurrence of the specified regular expression pattern. This method returns an empty string if no match is found.

As matches are found, they are added to what you can think of as an array of matches. Because the array element count starts at 0, if you want to return the third match, you would specify 2 as the `matchIndex` value. For example, if you enter a text string with three words that match the specified pattern, you can return the first, second, or third match only by specifying its index value.

For example, the following example is looking for a group of numbers in an action variable.

```text
${step_297}.getMatch('([\d]+)', 1)
```
{: codeblock}

If the action variable `${step_297}` contains the string `hello 123 i said 456 and 8910`, this expression returns `456`.

### `String.isEmpty()`
{: #expression-methods-actions-strings-isEmpty}

This method returns `true` if the string is an empty string, but not `null`, as in this example:

```text
${step_297}.isEmpty()
```
{: codeblock}

### `String.length()`
{: #expression-methods-actions-strings-length}

This method returns the character length of the string, as in this example:

```text
${step_297}.length()
```
{: codeblock}

If the action variable `${step_297}` contains the string `Hello`, this expression returns 5.

### `String.matches(String regexp)`
{: #expression-methods-actions-strings-matches}

This method returns `true` if the string matches the input regular expression, as in the example:

```text
${step_297}.matches('^Hello$')
```
{: codeblock}

If the action variable `${step_297}` contains the string `Hello`, this expression evaluates to `true`.

### `String.startsWith(String)`
{: #expression-methods-actions-strings-startsWith}

This method returns `true` if the string starts with the specified substring, as in this example:

```text
${step_297}.startsWith('What')
```
{: codeblock}

If the action variable `${step_297}` contains the string `What is your name?`, this expression returns `true`.

### `String.substring(Integer beginIndex, Integer endIndex)`
{: #expression-methods-actions-strings-substring}

This method returns a substring beginning with the character at `beginIndex` and ending with the character before `endIndex`. (The `endIndex` character itself is not included in the substring.) The index values are zero-based, so the first character in the string is at index 0.

This example returns a substring that begins at index 5 (which is the sixth character), and continuing to the end of the string:

```text
${step_297}.substring(5, ${step_297}.length())
```
{: codeblock}

If the action variable `${step_297}` contains the string `This is a string.`, this expression returns `is a string.`

### `String.toJson()`
{: #expression-methods-actions-strings-toJson}

This method parses a string that contains JSON data and returns a JSON object or array, as in this example:

```text
${json_var}.toJson()
```
{: codeblock}

If the session variable `${json_var}` contains the following string:

```string
"{ \"firstname\": \"John\", \"lastname\": \"Doe\" }"
```
{: codeblock}

the `toJson()` method returns the following object:

```json
{
  "firstname": "John",
  "lastname": "Doe"
}
```
{: codeblock}

### `String.toLowerCase()`
{: #expression-methods-actions-strings-toLowerCase}

This method returns the specified string that is converted to lowercase letters, as in this example:

```text
${step_297}.toLowerCase()
```
{: codeblock}

If the action variable `${step_297}` contains the string `This is A DOG!`, this expression returns the string `this is a dog!`.

### `String.toUpperCase()`
{: #expression-methods-actions-strings-toUpperCase}

This method returns the original string that is converted to uppercase letters, as in this example:

```text
${step_297}.toUpperCase()
```
{: codeblock}

If the action variable `${step_297}` contains the string `hi there`, this method returns the string `HI THERE`.

### `String.trim()`
{: #expression-methods-actions-strings-trim}

This method trims any spaces at the beginning and end of a string and returns the modified string, as in this example:

```text
${step_297}.trim()
```
{: codeblock}

If the action variable `${step_297}` contains the string `   something is here    `, this method returns the string `something is here`.

### `java.lang.String` support
{: #expression-methods-actions-strings-java-lang-String}

In addition to the built-in methods, you can use standard methods of the `java.lang.String` class.

#### `java.lang.String.format()`
{: #expression-methods-actions-strings-java-lang-String-format}

You can apply the standard Java String `format()` method to text. For information about the syntax to use, see [Format String Syntax](https://docs.oracle.com/javase/7/docs/api/java/util/Formatter.html#syntax){: external}.

This example takes three decimal integers (1, 1, and 2) and adds them to a sentence:

```java
T(java.lang.String).format('%d + %d equals %d', 1, 1, 2)
```
{: codeblock}

The resulting string is `1 + 1 equals 2`.

This example changes the decimal placement for a number that is collected by a step:

```java
T(String).format('%.2f',${step_297})
```
{: codeblock}

If the `${step_297}` variable that needs to be formatted in US dollars is 4.5, the resulting string is `4.50`.

## Array methods
{: #expression-methods-actions-arrays}

These methods help you work with arrays.

### `Array.add(value...)`
{: #expression-methods-actions-arrays-add}

This method adds one or more new values to the array and returns `true` if the operation is successful.

```text
${Items}.add('four', 'five')
```
{: codeblock}

If `Items` is `['one', 'two', 'three']`, this example updates it in place to become `['one', 'two', 'three', 'four', 'five']`.

### `Array.addAll(Array array)`
{: #expression-methods-actions-arrays-add-all}

This method adds one array to another and returns `null`.

```text
${Items}.addAll(${New_items})
```
{: codeblock}

If `Items` is `['one', 'two', 'three']` and `New_items` is `['four', 'five', 'six']`, this example updates `Items` in place to become `['one', 'two', 'three', 'four', 'five', 'six']`.

### `Array.append(value...)`
{: #expression-methods-actions-arrays-append}

This method appends one or more new values to the array and returns the result as a new array. The original array is not modified.

```text
${Items}.append('four', 'five')
```
{: codeblock}

If `Items` is `['one', 'two', 'three']`, this example returns the new array `['one', 'two', 'three', 'four', 'five']`.

### `Array.clear()`
{: #expression-methods-actions-arrays-clear}

This method removes all values from the array and returns null.

```text
${Items}.clear()
```

After this expression is evaluated, `Items` is an empty array (`[]`).

### `Array.contains(value)`
{: #expression-methods-actions-arrays-contains}

This method returns `true` if the array contains an item that is exactly equal to the input value. The specified value can be a string or a number.

```text
${Items}.contains(123)
```

If `Items` is `[123, 456, 789]`, this example returns `true`.

### `Array.containsIgnoreCase(value)`
{: #expression-methods-actions-arrays-contains-ignore-case}

This method returns `true` if the array contains an item that is equal to the input value. Strings are matched regardless of whether the value is specified in uppercase or lowercase letters. The specified value can be a string or a number.

```text
${Items}.contains('two')
```

This example returns `true` if the `Items` array contains any capitalization of the string `two` (for example, `TWO` or `Two` would also match).

### `Array.filter(temp_var, "temp_var.property operator comparison_value")`
{: #expression-methods-actions-arrays-filter}

Filters an array by comparing each array element to a value you specify, returning a new array that contains only the matching elements.

The filter expression consists of the following values:

- `temp_var`: An arbitrary name for a temporary variable that is used to hold each array element as it is evaluated. For example, if the original array contains objects that describe cities, you might use `city` as the temporary variable name.

- `property`: The element property that you want to filter on. This must be a property of the elements in the source array. Specify the property as a property of `temp_var`, by using the syntax `temp_var.property`. For example, if `latitude` is a valid property name for the source elements, you might specify the property as `city.latitude`.

- `operator`: The operator to use to compare the property value to the comparison value. You can use any of the following operators:

    | Operator | Description |
    |----------|-------------|
    | `==`     | Is equal to |
    | `>`      | Is greater than |
    | `<`      | Is less than |
    | `>=`     | Is greater than or equal to |
    | `<=`     | Is less than or equal to |
    | `!=`     | Is not equal to |
    {: caption="Supported filter operators" caption-side="top"}

- `comparison_value`: The value that you want to compare each array element property value to. You can specify a literal value or reference a variable.

#### Filter examples
{: #filter-examples}

For example, you might have an array of objects that contain city names and their population numbers:

```json
[
   {
      "name":"Tokyo",
      "population":13988129

   },
   {
      "name":"Rome",
      "population":2860009

   },
   {
      "name":"Beijing",
      "population":21893095

   },
   {
      "name":"Paris",
      "population":2165423

   }
]
```
{: codeblock}

If the source array is stored in a variable that is called `${cities}`, the following exexpression returns a smaller array that contains only cities with populations greater than 5 million:

```text
${cities}.filter("city", "city.population > 5000000")
```
{: codeblock}

The expression returns the following filtered array:

```json
[
   {
      "name":"Tokyo",
      "population":13988129

   },
   {
      "name":"Beijing",
      "population":21893095

   }
]
```
{: codeblock}

Instead of a hardcoded comparison value, you might also filter based on a dynamic value that is stored in a variable. This example filters by using a population value that is specified by a customer response in a previous step:

```text
${cities}.filter("city", "city.population > ${step_123}")
```
{: codeblock}

When you compare number values, be sure to set the context variable that is involved in the comparison to a valid value before the filter method is triggered. Note that `null` can be a valid value if the array element you are comparing it against might contain it.
{: tip}

### `Array.get(Integer index)`
{: #expression-methods-actions-arrays-get}

This method returns the item from the array that is at the specified index position. Arrays are zero-indexed, meaning that the first item in the array is at index position `0`.

```text
${Items}.get(1)
```

If `Items` is `['one', 'two', 'three']`, this example returns `two`.

The `get()` method is an alternative to using brackets (`[]`) to retrieve an item from an array. The following example is also valid and returns the same result:

```text
${Items}[1]
```

If you are using a value that is specified by a customer to choose an item from an array, you might need to subtract 1 to convert to a zero-indexed value. For example, you might use an expression like `${Items}.get(${step_123} - 1)` to retrieve the intended value.
{: note}

### `Array.getRandomItem()`
{: #expression-methods-actions-arrays-get-random-item}

This method returns a randomly chosen item from the array.

```text
${Items}.getRandomItem()
```

If `Items` is `['one', 'two', 'three']`, this example returns `one`, `two`, or `three`, on a random basis.

### `Array.indexOf(value)`
{: #expression-methods-actions-arrays-index-of}

This method returns the index position of the first occurrence of the input value in the array, or `-1` if the array does not contain the input value. The specified value can be a string or a number.

```text
${Items}.indexOf(`two`)
```

If `Items` is `['one', 'two', 'three']`, this example returns the integer `1` (indicating the second position in the zero-indexed array).

### `Array.join(String delimiter)`
{: #expression-methods-actions-join}

This method joins all values in this array to a string. Values are converted to string and delimited by the input delimiter.

For example, you might use a variable that is named `pizza_toppings` that contains the array `["pepperoni", "ham", "mushrooms"]`. The following expression converts this array into the string `pepperoni, ham, mushrooms`:

```text
${toppings_array}.join(', ')
```

If you use that expression to define the value of a variable, you can then reference that variable in your assistant output to create a human-readable message (for example, `You have selected the following toppings: pepperoni, ham, mushrooms`).

### `JSONArray.joinToArray(template, retainDataType)`
{: #expression-methods-actions-arrays-join-to-array}

This method extracts information from each item in the array and builds a new array that is formatted according to the template you specify. The template can be a string, a JSON object, or an array. The method returns an array of strings, an array of objects, or an array of arrays, depending on the type of template.

This method is useful for formatting information as a string that you can return as part of the output of a step, or for transforming data into a different structure so you can use it with an external API.

In the template, you can reference values from the source array by using the following syntax:

```text
%e.{property}%
```

where `{property}` represents the name of the property in the source array.

For example, suppose that your assistant stores an array that contains flight details in a session variable. The stored data might look like this:

```json
"flights": [
      {
        "flight": "AZ1040",
        "origin": "JFK",
        "carrier": "Alitalia",
        "duration": 485,
        "destination": "FCO",
        "arrival_date": "2019-02-03",
        "arrival_time": "07:00",
        "departure_date": "2019-02-02",
        "departure_time": "16:45"
      },
      {
        "flight": "DL1710",
        "origin": "JFK",
        "carrier": "Delta",
        "duration": 379,
        "destination": "LAX",
        "arrival_date": "2019-02-02",
        "arrival_time": "10:19",
        "departure_date": "2019-02-02",
        "departure_time": "07:00"
      },
      {
        "flight": "VS4379",
        "origin": "BOS",
        "carrier": "Virgin Atlantic",
        "duration": 385,
        "destination": "LHR",
        "arrival_date": "2019-02-03",
        "arrival_time": "09:05",
        "departure_date": "2019-02-02",
        "departure_time": "21:40"
      }
    ]
```
{: codeblock}

To build an array of strings that describe these flights in a user-readable form, you might use the following expression:

```text
${Flight_data}.joinToArray("Flight %e.flight% to %e.destination%", true)
```

This expression would return the following array of strings: `["Flight AZ1040 to FCO","Flight DL1710 to LAX","Flight VS4379 to LHR"]`.

The optional `retainDataType` parameter specifies whether the method preserves the data type of all input values in the returned array. If `retainDataType` is set to `false` or omitted, in some situations, strings in the input array might be converted to numbers in the returned array. For example, if the selected values from the input array are `"1"`, `"2"`, and `"3"`, the returned array might be `[ 1, 2, 3 ]`. To avoid unexpected type conversions, specify `true` for this parameter.

#### Complex templates
{: #join-to-array-complex-template}

A more complex template might contain formatting that displays the information in a legible layout. For a complex template, you might want to store the template in a session variable, which you can then pass to the `joinToArray` method instead of a string.

For example, this complex template contains a subset of the array elements, adding labels and formatting:

```text
<br/>Flight number: %e.flight% <br/> Airline: %e.carrier% <br/> Departure date: %e.departure_date% <br/> Departure time: %e.departure_time% <br/> Arrival time: %e.arrival_time% <br/>
```
{: codeblock}

Make sure any formatting that you use in your template is supported by the channel integration that displays the assistant output.
{: note}

If you create a session variable that is named `Template`, and assign this template as its value, you can then use that variable in your expressions:

```text
${Flight_data}.joinToArray(${Template})
```

At run time, the response would look like this:

```text
Flight number: AZ1040
Airline: Alitalia
Departure date: 2019-02-02
Departure time: 16:45
Arrival time: 07:00

Flight number: DL1710
Airline: Delta
Departure date: 2019-02-02
Departure time: 07:00
Arrival time: 10:19

Flight number: VS4379
Airline: Virgin Atlantic
Departure date: 2019-02-02
Departure time: 21:40
Arrival time: 09:05
```
{: screen}

#### JSON templates
{: #join-to-array-object-template}

Instead of a string, you can define a template as a JSON object, which provides a way to standardize the formatting of information from different systems, or to transform data into the format required for an external service.

In this example, a template is defined as a JSON object that extracts flight details from the elements that are specified in the array that is stored in the `Flight data` session variable:

```json
{
  "departure": "Flight %e.flight% departs on %e.departure_date% at %e.departure_time%.",
  "arrival": "Flight %e.flight% arrives on %e.arrival_date% at %e.arrival_time%."
}
```
{: codeblock}

Using this template, the `joinToArray()` method returns a new array of objects with the specified structure.

### `Array.remove(Integer index)`
{: #expression-methods-actions-arrays-remove}

This method removes the item in the specified index position from the array, and returns the updated array.

```text
${Items}.remove(1)
```

If `Items` is `['one', 'two', 'three']`, this example returns `['one', 'three']`. The original `Items` array is also modified in place.

### `Array.removeValue(value)`
{: #expression-methods-actions-arrays-remove-value}

This method removes the first occurrence of the specified value from the array, and returns the updated array. The specified value can be a string or a number.

```text
${Items}.removeValue('two')
```

If `Items` is `['one', 'two', 'three']`, this example returns `['one', 'three']`. The original `Items` array is also modified in place.

### `Array.set(Integer index, value)`
{: #expression-methods-actions-arrays-set}

This method replaces the item in the specified index position with the specified value, and returns the updated array.

```text
${Items}.set(2,'five')
```

If `Items` is `['one', 'two', 'three']`, this example returns `['one', 'two', 'five']`. The original `Items` array is also modified in place.

### `Array.size()`
{: #expression-methods-actions-arrays-size}

This method returns the number of items in the array as an integer.

```text
${Items}.size()
```

If `Items` is `['one', 'two', 'three']`, this example returns `3`.

### `Array.sort()`
{: #expression-methods-actions-arrays-sort}

This method does an in-place sorting and returns the sorted array. The default parameter is `ascending`. You can specify `descending` to change the sort order. Any other parameter entry is ignored and a log error appears.

```text
${Items}.sort("ascending")
```

The method compares numbers and strings. A number is always smaller than a string. Any other type is converted to string by default to compare. 

For example:

| Original array | Sorted array |
| --- | --- |
| [2,1,3,5,4,3,2] | [1,2,2,3,3,4,5] |
| ["Banana", "Orange", "Apple", "Mango"] | ["Apple", "Banana", "Mango", "Orange"] |
| [3, 2, 4, "1", "10", "12", "Banana", "Orange", 0, "Apple", "Mango"] | [0, 2, 3, 4, "1", "10", "12", "Apple", "Banana", "Mango", "Orange"] |
{: caption="Sorting examples" caption-side="bottom"}

### `Array.transform()`
{: #expression-methods-actions-arrays-transform}

This method is used with the [`session_history` variable](/docs/watson-assistant?topic=watson-assistant-manage-info#built-in-variables) only. You can transform the output of the variable to match a specific generative AI system. 

The signature is `transform(String rolePrefix, String userPrefix, String assistantPrefix, optional Boolean currentAction=false)`. Customer messages are in the form `{$rolePrefix: $userPrefix, "content": $content}`. Assistant messages are in the form `{$rolePrefix: $assistantPrefix, "content": $content}`.

If `currentAction` is true:

| Assistant uses | Description |
| --- | --- |
| Actions only | The transform excludes all messages where `n`is true, which indicates that a customer question triggered a new base action. 
| Dialog only  | `currentAction` is ignored and the transform includes the entire contents of the `session history` variable.
| Dialog and action | The transform includes everything in the `session_history` variable since the most recent start of an action, regardless of whether any dialog nodes are triggered. |
{: caption="If `currentAction` is true" caption-side="bottom"}

The `n : true` flags are not included in the output of transform.

This example produces OpenAI chat format:

```text
${system_session_history}.transform("role", "user", "assistant")
```

This example produces Google PaLM2 chat format:

```text
${system_session_history}.transform("author", "USER", "AI")
```
