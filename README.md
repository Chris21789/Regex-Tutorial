# Understanding the URL Validation Regex

The URL validation regex can be a somewhat complicated topic to understand without having a detailed guide to learn from. This document aims to provide such a guide by providing an in-depth look at the pattern and how it is designed to match a broad range of URL formats. These formats can even extend to optional protocal specifications, domain names, top-level domains and optional paths. 

## Summary

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

While this line of symbols and characters may look like chicken scratch there is a very specific explaination to all of it. Most people may only consider searching for something using literal characters but a regex, or regular expression, can use special characters to find something using a specific pattern. The pattern used in this regex matches the typical pattern found in a URL and I will break down and explain this expression piece by piece.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors
Anchors are the identifiers that signal the beginning and the end of a string inside of a regex. The carrot or `^` signals the beginning of the string while the dollar sign or `$` signals the end of the string. In our example regex: `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`, we see the `^` is followed immediatly by `(https?:\/\/)` which is a major indicator that we are looking for a URL.
### Quantifiers
Quantifiers indicate numbers of characters or expressions to match. Here is a list of quantifiers and what they do:

`x*`: Matches the preceding item "x" 0 or more times.

`x+`: Matches the preceding item "x" 1 or more times.

`x?`: Matches the preceding item "x" 0 or 1 times.

`x{n}`: When "n" is a non-negative integer, matches exactly "n" occurrences of the preceding item "x".

`x{n,}`: When "n" is a non-negative integer, matches at least "n" occurrences of the preceding item "x".

`x{n,m}`: When "n" and "m" are non-negative integers and `m >= n`, matches at least "n" and at most "m" occurrences of the preceding item "x".

We can break down our example regex `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/` using these quantifiers as examples. 

`(https?:\/\/)?`: Indicates we are looking for this pattern 0 or 1 times. This is typical for a URL as the https:// tag is generally used once and sometimes not at all.

`[\da-z\.-]+`: This section indicates we are looking for a string that includes lower case letters, numbers, a dot and a hyphen more than once like in this section of a URL.

`[a-z\.]{2,6}`: Similar to the last section, we are looking for a string of lower case letters and a dot however this time there has to be at least 2 occurences but no more than 6 occurences.

`([\/\w \.-]*)*`: For this final segment we are looking for any  alphanumerical value, a dot and a hyphen 0 or more times. 

### Grouping Constructs
Grouping constructs with `( )`such as `(https?:\/\/)?` matches what is within the parenthesis and remembers the match so that it can be refered to later.  Doing so also allows the application of a quantifier to the entire group as shown in the example.
### Bracket Expressions
Bracket expressions match any of the characers enclosed within them. For example, in our regex `[a-z\.]` indicates a string that includes lower case letters and a dot.
### Character Classes
Character classes distinguish kinds of characters such as distinguishing better letters and digits. Some of the major classes inclue:

`\d`: Matches any digit (0-9).

`\w`: Matches any word characters (alphanumeric and underscore).

`[a-z]`: Matches any lowercase letter. 

`\.`: Escapes the period character, matching a literal period.
### The OR Operator
The OR operator is denoted with a `|` and is also refered to as a disjunction. Although there are none in the example regex, in the example `x|y` the section would match either x or y. 
### Flags
Flags can modify the behavior of a regex but our example URL regex does not use any. Some example flags include:

`g`: Makes the expression search for all occurrences

`i`: Makes the expression search case-insensitively

`m`: Makes the boundary characters ^ and $ match the beginning and ending of every single line instead of the beginning and ending of the whole string

`u`: Makes the expression assume individual characters as code points, not code units, and thus match 32-bit characters as well

`s`: Makes the wild character `.` match newlines as well
### Character Escapes
When trying to use any of the special characters literally, a character escape must be used by putting a `\` in front of it. A great example from our regex: `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/` can be seen here: `([\da-z\.-]+)\.`. This portion in parenthesis is looking for domain name text while the `\.` is the literal period following like in `www.`.
## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
