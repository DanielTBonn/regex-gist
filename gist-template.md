# Title (replace with your title)

Regex is an important search tool that programmers can use to help identify patterns that arise in strings or text. To those of us who are newer to programming it can look like indigestable gibberish only the computers can hope to comprehend. However, after taking some time to learn the patterns it actually is quite simple and can become a powerful tool in our programming toolkit. To help understand regex and possibly pass on this knowledge to other new programmers trying to make sense of these cryptic patterns, I have set out to explain what it's components do. To do this, I will use a specific example and relay the purpose of every individual part of the expression and what the results will be for different expressions. 

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.

Regular expressions, or regex, actually comes from the mathematical concept of regular sets. 

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

A regex is considered a literal, so in javascript the pattern must be wrapped in slash characters `/`.

### Anchors

^ and $ are 'anchored' to the front and back of the regex respectively

### Quantifiers

Sets the limit of the string our regex matches, includes min and max number of characters that our regex is looking for.
Are inherently greedy, meaning they match as many of occurences of particular patterns as possible.

### OR Operator

Like with the bracket operators, the OR operator can match expressions such as `[abc]` in the same manner using `(a|b|c)`

### Character Classes

A character class defines a set of characters, any of which can occur in an input string to fulfill a match. An example of this is the brackets we have already seen, but more are:

* . -- matches any character except the newline \n
* \d -- matches any arabic numeral digit. Equal to [0-9]
* \w -- matches any alphanumeric character from the basic latin alphabet, including the underscore. Equal to [A-Za-z0-9_]
* \s -- matches a single whitespace character, including tabs and line breaks

Inverse matches can be performed by using the capital letter, see \D matching non-digit characters.

### Flags

Outside of the literal between slashes, we can place a flag like so -- `/literal/g`. The flag defines additional functionality or limits to our regex. You can use the 6 flags together or seperately for your purposes, the 3 most common ones are as follows: 

* g -- Global search: the regex should be tested against all possible matches in a string.
* i -- Case-sensitive search: case should be ignored while attempting a match in a string.
* m -- Multi-line search: a multi-line input string should be treated as multiple lines

### Grouping and Capturing

Grouping constructs are performed by using parenthesis `()` to create sections known as subexpressions. The following is two subexpressions: 

`(abc):(xyz)`. 

Sub expressions look for an exact match, meaning the expression `abc:xyz` will match, but `acb:xyz` will not unless told to do otherwise.

Grouping constructs have two categories, `capturing` and `non-capturing`. The important thing to know for now is that capturing groups capture the matched character sequences for possible re-use (including a numbered backreferences) while non-capturing groups do not. A grouping construct can be made non-capturing by adding the characters ?: at the beginning of an expression inside the parentheses. 

### Bracket Expressions

A bracket expression, or positive character group (outlines characters we want included), is anything inside a set of brackets `[]` representing a range of characters that we want to match. [abc] matches any string that includes an a, b, or c, and hyphens `-` are used between alphanumeric characters (letters/numbers) to represent a possible range. Therefore [abc] = [a-c]. Bracket expressions typically follow forms such as:

* [a-z] -- Contains any lowercase letter between a-z. For uppercase characters we must use [A-Z]
* [0-9] -- Contains numbers between 0-9
* [_-] -- Contains any special character that matches the _ and -, note that the hyphen `-` is different than the range hyphen above since it doesn't follow an alphanumeric character. 

Note we can create a negative character group, or a bracket expression that excludes any character of a certain pattern, but including a carrot `^` inside the bracket expression at the beginning. Therefor the expression [^aeiouAEIOU] looks for any string that does NOT contain a vowel.

### Greedy and Lazy Match

Greedy matching will find as many occurrences of a particular pattern as possible. Quantifiers are inherently greedy, and include:

* `*` -- matches the pattern zero or more times
* + -- Matches the pattern one ore more times
* ? -- Matches the pattern zero or one time
* {} -- Curly brackets can provide three different ways to set limits for a match:
    - { n } -- Matches EXACTLY n number of times
    - { n, } -- Matches AT LEAST n number of times
    - { n, x } -- Matches a minimum of n and maximum of x nubmer of times

These quantifiers can be made lazy by adding the ? symbol after it, meaning it will match as few occurrences as possible.

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
