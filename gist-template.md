# Title (replace with your title)

Regex is an important search tool that programmers can use to help identify patterns that arise in strings or text. To those of us who are newer to programming it can look like indigestable gibberish only the computers can hope to comprehend. However, after taking some time to learn the patterns it actually is quite simple and can become a powerful tool in our programming toolkit. To help understand regex and possibly pass on this knowledge to other new programmers trying to make sense of these cryptic patterns, I have set out to explain what it's components do. To do this, I will use a specific example and relay the purpose of every individual part of the expression and what the results will be for different expressions. 

## Summary

Today we will be studying a regex that matches a URL. The different components that make up this regular expression is as follows:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`



https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial

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

A regex is considered a literal, so in javascript the pattern must be wrapped in slash characters `/`. For characters that may be interpreted literally as a regex component, we use the backslash `\` before it. For instance, as we will see with the next example, problems may arise if we wanted to use the forward slash `/`, to combat this and allow for it in our regex, we simply need to include the backslash before it `\/`. Other examples we will see later on are looking for a period `.` by using `\.`, or perhaps a 

### Anchors

First, lets turn our attention to the two symbols at the front and end of our regex respectively, the `^` and `$`. These two symbols are known as anchors, and their purpose is anchoring the regex component that immediately follows to the front or back of the expression we are looking for respectively. 

In our case, if we take a look at the `^` which is an anchor for the front of our expression, we can see it anchors the regex component inside the parentheses `(https?:\/\/)`. We will look at the `?` in more detail later, but all you need to know is that it matches something 0 or at most 1 times, so we see the phrase `https://`. When web browsing, we can see that this (or similarly `http://`) is always going to be at the front of our website url, making it essential to searching for in our regex. 

For the `$` anchor tag, which anchors the end of our expression with whatever should be placed at the end, we find the expression `\/?$`. Recalling what we learned about the `\` and `?` components, we can see that the `$` anchor is simply looking for 0 or at most 1 forward slash at the end of the expression `/`. 

### Quantifiers

Sets the limit of the string our regex matches, includes min and max number of characters that our regex is looking for.\(\[\\da-z\\\.-\]\+\)
Are inherently greedy, meaning they match as many of occurences of particular patterns as possible.

A quantifier is used to set the exact number, lower limit, or the min and max number of times we want to see a certain regular expression. It uses 2 squigly brackets followed by the pattern you desire, it will look something like this:

- { n } -- Matches EXACTLY n number of times
- { n, } -- Matches AT LEAST n number of times
- { n, x } -- Matches a minimum of n and maximum of x nubmer of times

In our regex we find one component that matches a quantifier, `{2,6}`. The entire expression that our quantifier executes on is `([a-z\.]{2,6})`, a bracket expression contained inside the same parentheses as our quantifier. Bracket expressions are used for ranges of characters, therefore any lowercase english letter aswell as a period `\.` will be match our expression.  Due to it's placement it seems to want to match any expression that could be a to be a top level domain, or in other words something along the lines of .com, .org, .io, etc.

### OR Operator

Like with the bracket operators, the OR operator can match expressions such as `[abc]` in the same manner using `(a|b|c)`

### Character Classes

There are quite a few character classes that can comprise regex expressions. They usually follow the same pattern however, starting with a `\` and followed by a letter. In our case we find two different character classes nested within two different grouping constructs (or in this case a group of characters within a set of parentheses `()`) of our expression. 

- `\d` part of the grouping construct `([\da-z\.-]+)`
- `\w` part of the grouping construct `([\/\w \.-]*)`

These two character classes define a set of characters, any of which can occur in an input string to fulfill a match. The first one `\d` matches any arabic numeral digit between `[0-9]`. So for any integer expression, such as `86` or `75309`, the regex will match.  

The second character class `\w` matches any alphanumeric character from the basic latin alphabet, including the underscore, and is equal to `[A-Za-z0-9_]`. So for any expression that doesn't include special characters, spaces, or non-latin alphabet characters, we will find a match. For example `abc_321` matches, but `-#@%\. ` will not.

In addition to these two character classes, I have provided information on two more below.

* `.` -- matches any character except the newline `\n`
* `\s` -- matches a single whitespace character, including tabs and line breaks
* `\d` -- matches any arabic numeral digit. Equal to `[0-9]`
* `\w` -- matches any alphanumeric character from the basic latin alphabet, including the underscore. Equal to `[A-Za-z0-9_]`

For the last three classes above, inverse matches can be performed by using their capital letter. The character class `\D` will then match non-digit characters.

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

A grouping construct is used to break up sections of a string to determine if they match what type of expression you are looking for. The primary way to make them are by using parentheses `()`.

### Bracket Expressions

A bracket expression, or positive character group (outlines characters we want included), is anything inside a set of brackets `[]` representing a range of characters that we want to match. [abc] matches any string that includes an a, b, or c, and hyphens `-` are used between alphanumeric characters (letters/numbers) to represent a possible range. Therefore [abc] = [a-c]. Bracket expressions typically follow forms such as:

* [a-z] -- Contains any lowercase letter between a-z. For uppercase characters we must use [A-Z]
* [0-9] -- Contains numbers between 0-9
* [_-] -- Contains any special character that matches the _ and -, note that the hyphen `-` is different than the range hyphen above since it doesn't follow an alphanumeric character. 

Note we can create a negative character group, or a bracket expression that excludes any character of a certain pattern, but including a carrot `^` inside the bracket expression at the beginning. Therefor the expression [^aeiouAEIOU] looks for any string that does NOT contain a vowel.

### Greedy and Lazy Match

Greedy matching will find as many occurrences of a particular pattern as possible. Quantifiers are inherently greedy, and include:

* `*` -- matches the pattern zero or more times
* `+` -- Matches the pattern one ore more times
* `?` -- Matches the pattern zero or one time
* `{}` -- Curly brackets can provide three different ways to set limits for a match:
    - `{ n }` -- Matches EXACTLY n number of times
    - `{ n, }` -- Matches AT LEAST n number of times
    - `{ n, x }` -- Matches a minimum of n and maximum of x nubmer of times

These quantifiers can be made lazy by adding the ? symbol after it, meaning it will match as few occurrences as possible.

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
