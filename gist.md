# Regex Tutorial: Matching a Hex Value

This tutorial is in reference to a regular expression that would be utilized to match a hex value - both to guide others that may come across this post, as well as to apply and further my own knowledge in different facets of regular expression utilization.

## Summary

`Regex` is short for `regular expression`, which is a series of characters that define a specific search pattern. Regular expressions can be used to find patterns of characters within a string, find and replace characters or sequences of characters within a string, or more commonly - validating inputs.

In this case, the regex that I will be describing will be used to match a hex value. I will be explaining the components of the regex for matching a hex value, the anchors, quantifiers, grouping constructs, bracket expressions, character classes, the OR operator, flags, and character escapes.

Here is an example code snippet of a regex to match a hex value: `/^#?([a-f0-9]{6}|[a-f0-9]{3})$/`

As a simple breakdown of this regex code snippet:

-   The string can contain any lowercase letters between a-f
-   The string can contain any numbers between 0-9
-   The string will be either 6 units in length OR 3 units in length
-   We are looking for a match count of zero or one time(s)

## Table of Contents

-   [Anchors](#anchors)
-   [Quantifiers](#quantifiers)
-   [Grouping Constructs](#grouping-constructs)
-   [Bracket Expressions](#bracket-expressions)
-   [Character Classes](#character-classes)
-   [The OR Operator](#the-or-operator)
-   [Flags](#flags)
-   [Character Escapes](#character-escapes)

## Regex Components

Regex is considered a literal, therefore it must be wrapped in forward slash characters (`/`)

We will list out the components of a regex and will go deeper into the components in their respective sections. With that prefaced, the first component of a regex are the anchors, followed by the quantifiers, grouping constructs, bracket expressions, character classes, the OR operator, flags, and the character escapes.

### Anchors

The two anchors of a regex are the `^` and `$` characters. As seen in the example code snippet above, you can see the `/^` starting the regex matching snippet and the `$/` that closes out the expression.

The `^` anchor signifies a string that begins with the characters that follow right after it. This can be followed by an exact string or a range of possible string matches. It is important to note that regex is case sensitive - as an example: `^Hello`, will match with the strings `Hello` or `Hello world`, but will not match with the strings `hello` or `hello cat`.

The `$` anchor signifies a string that ends with the characters that come right before it. Similar to the `^` achor, this `$` anchor can be preceded by either an exact match or a range of matches.

In our example snippet we can see that the string will need to start with a combination that matches the pattern `[a-f0-9]`. If you take a look back at the code snippet, you will also notice the pattern `{6}`, this is known as a `quantifier`, which we will transition over to in the next section!

### Quantifiers

`Quantifiers` set the limits of the string length that the regex will be matching. They will frequently be set up with the parameters of minimum and maximum length of characters that the regex will be searching for. This can be seen with a format of `{4,8}` which can be described as a minumum of 4 characters short and a maximum of 4 characters long.

In our code snippet example above, we can see our regex will be searching for strings either exactly 6 characters long (designated with the `{6}`) OR strings that are exactly 3 characters long (designated with the `{3}`). We will discuss in a different section as to how we know the regex is searching for strings of either 6 OR 3 characters long. As a hint, the `|` character plays a large role in what is known as the OR Operator.

Quantifiers will match with as many occurrences of particar patterns as possible. A few of the common ones you may see will be listed below:

-   `*` -- matches the pattern zero or more times
-   `+` -- matches the pattern one or more times
-   `?` -- matches the pattern zero or one times
-   `{}` -- this can provide different ways to set limits for a match:
    -   `{n}` -- matches the pattern exactly `n` number of times
    -   `{n, }` -- matches the pattern at least `n` number of times
    -   `{n, x}` -- matches the pattern from a minumum of `n` number of times to a maximum of `x` number of times

In our code snippet example above, we can see our regex will be searching for strings that match the specified pattern zero or one times - designated via the `?` close to the start of the snippet.

### Grouping Constructs

Regular expressions may grow in complexity, where you may want to match for mulitple parts of a string. This is where you will using `grouping constructs` to break up different sections of the matching parameters. The main method of grouping sections of a regex is to use parentheses - where each section within parentheses are called `subexpressions`.

For example `(qwe):(asd)`. The first subexpression is looking for a part of the string that matches the string `qwe` exactly. Similarly, the second subexpression is looking for `asd`. There is a colon that lies in between the two subexpressions - Subexpressions look for an exact match unless specified otherwise. For this example, the string `qwe:asd` would match, but the string `qew:ads` would not.

In our example, we can see that the grouping constructs are used to encompass our two parameters separated by an OR Operator - which tells us that we only have one subexpression that we are looking to match for - `([a-f0-9]{6}|[a-f0-9]{3})`

### Bracket Expressions

Anything within a set of square brackets represents a range of characters that we are looking to match with in our search. These patterns within the brackets are known as `bracket expressions` and have also been known as `positive character group`. The parameters set in the brackets set our search exclusively for those characters or numbers, but they are parameters that would be included in the search requirements for a match. For example, `[qwe]` will look for a string that includes `q`, `w`, or `e` - regardless of the length of the string.

You will also see a hyphen (`-`) used to represent a range between alphanumeric characters. In our example, you can see that we are looking for a range of lowercase characters beween `a-f` and numbers between `0-9`.

If we wanted to include uppercase letters, we would adjust the search expression to `[a-fA-F]`. It is also common to see expressions that would like to include special characters like underscores or hyphens - this can be done by adding them at the end of the square brackets, following the alphanumeric parameters set - `[a-f0-9_-]`.

### Character Classes

Character classes in regex defines a set of characteres, of which can occur in an input string to fulfill a match. The bracket expressions discussed previously is considered a character class. A few other common character classes are listed below:

-   `.` -- matches any character except the newline character
-   `\d` -- matches any Arabix numeral digit. This is equivalent to the bracket expression `[0-9]`
-   `\w` -- matches any alphanumeric character from the basic Latin alphabet, including the underscore. This is equivalent to the bracket expression `[A-Za-z0-9_]`
-   `\s` -- matches a single whitespace character, including tabs and line breaks

### The OR Operator

The OR Operator (`|`) in an expression can allow us to change our matching parameters. Referring to the example in grouping constructs of `(qwe):(asd)`, we can convert it using the OR Operator to `(q|w|e):(a|s|d)`, where both of the strings `qwe:asd` and `ewq:das` would match, as well as `q:a`, but `asd:qwe` would not.

### Flags

As discussed earlier in this post, a regex must be wrapped in forward slash characters (`/`), however, there is one exception to this rule - that is with the component known as `flags`. Flags are placed at the very end of the regex, after the second forward slash, and they provide additional functionality or limits for the regex. There are 6 optional flags, separately or together and in any order, but there are three that are most common:

-   `g` -- global search: the regex should be tested against all possible mathces in a string
-   `i` -- case-insensitive search: case should be ignored while attempting a match in a string
-   `m` -- multi-line search: a multi-line input string should be treated as multiple lines

### Character Escapes

Regex uses character escapes, which is denoted via the the backslash character (`\`) - this escapes a character that would otherwise would be interpreted literally. For example, the open curly brace (`{`) is used to begin a quantifier, however, adding a backslash before the open curly brace (`\{`) would make it so that the regex would look for the open curly brace character instead of beginning the definition to a quantifier. This is commonly used when looking for strings with special characters that are also used as a particular component of a regex.

It's important to note that all special characters, including the backslash, lose their special significance inside bracket expressions.

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
