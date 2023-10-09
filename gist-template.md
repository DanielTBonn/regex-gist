# Title (replace with your title)

Regex is an important search tool that programmers can use to help identify patterns that arise in strings or text. To those of us who are newer to programming it can look like indigestable gibberish only the computers can hope to comprehend. However, after taking some time to learn the patterns it actually is quite simple and can become a powerful tool in our programming toolkit. To help understand regex and possibly pass on this knowledge to other new programmers trying to make sense of these cryptic patterns, I have set out to explain what it's components do. To do this, I will use a specific example and relay the purpose of every individual part of the expression and what the results will be for different expressions. 

## Summary

Today we will be studying a regex that matches a URL. The different components that make up this regular expression is as follows:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Extra Topics](#extra-topics)

## Regex Components

A regex is considered a literal, so in javascript the pattern must be wrapped in slash characters `/`. For characters that may be interpreted literally as a regex component, we use the backslash `\` before it. For instance, as we will see with the next example, problems may arise if we wanted to use the forward slash `/`, to combat this and allow for it in our regex, we simply need to include the backslash before it `\/`. Other examples we will see later on are looking for a period `.` by using `\.`, or perhaps a 

### Anchors

First, lets turn our attention to the two symbols at the front and end of our regex respectively, the `^` and `$`. These two symbols are known as anchors, and their purpose is anchoring the regex component that immediately follows to the front or back of the expression we are looking for respectively. 

In our case, if we take a look at the `^` which is an anchor for the front of our expression, we can see it anchors the regex component inside the parentheses `(https?:\/\/)`. We will look at the `?` in more detail later, but all you need to know is that it matches something 0 or at most 1 times, so we see the phrase `https://`. When web browsing, we can see that this (or similarly `http://`) is always going to be at the front of our website url, making it essential to searching for in our regex. 

For the `$` anchor tag, which anchors the end of our expression with whatever should be placed at the end, we find the expression `\/?$`. Recalling what we learned about the `\` and `?` components, we can see that the `$` anchor is simply looking for 0 or at most 1 forward slash at the end of the expression `/`. 

### Quantifiers

Sets the limit of the string our regex matches, includes min and max number of characters that our regex is looking for. Quantifiers are inherently greedy, meaning they match as many of occurences of particular patterns as possible.

A quantifier is used to set the exact number, lower limit, or the min and max number of times we want to see a certain regular expression. It uses 2 squigly brackets followed by the pattern you desire, it will look something like this:

- { n } -- Matches EXACTLY n number of times
- { n, } -- Matches AT LEAST n number of times
- { n, x } -- Matches a minimum of n and maximum of x nubmer of times

In our regex we find one component that matches a quantifier, `{2,6}`. The entire expression that our quantifier executes on is `([a-z\.]{2,6})`, a bracket expression contained inside the same parentheses as our quantifier. Bracket expressions are used for ranges of characters, therefore any lowercase english letter aswell as a period `\.` will be match our expression.  Due to it's placement it seems to want to match any expression that could be a to be a top level domain, or in other words something along the lines of .com, .org, .io, etc.

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

### Grouping and Capturing

Before we jump in, you should know that grouping constructs have two categories, capturing and non-capturing. The important thing to know for now is that capturing groups capture the matched character sequences for possible re-use (including a numbered backreferences) while non-capturing groups do not. A grouping construct can be made non-capturing by adding the characters ?: at the beginning of an expression inside the parentheses.

Grouping constructs are performed by using parenthesis `()` to create sections known as subexpressions. They allow us to break up our regex into subexpressions that determine if a string matches what we are looking for. It is important to note that these are different than bracket expressions, because subexpressions look for an exact match unless they're told to do otherwise. As you can see in our example, we have 4 different grouping constructs looking for 4 different expressions in every string:

`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`

Which is comprised of:

- `(https?:\/\/)`
- `([\da-z\.-]+)`
- `([a-z\.]{2,6})`
- `([\/\w \.-]*)`

We have already discussed some of the regex components within the grouping constructs above, so now we can go over how we can use group capturing to restrict our search. 

For our first expression `(https?:\/\/)`, we have already guessed that `(https?:\/\/)` will match a value of `https://` or `http://`. No other values will match for our initial subexpression. 

Our second expression `([\da-z\.-]+)` matches digits, lowercase characters, a period and a dash. As you can see, this expression can match many different things, and with the addtion of the greedy quantifier `+` symbol, it is required to match at least once ore more times. That means the strings it can match are quite long. The important thing to notice is that it includes a backslash period `\.`, meaning if there are any periods anywhere within the expression it will still count as valid like we would want for something following the URL format `example.website`. This makes the expression very flexible in searching for the subdomain and second-level domain (note the top-level domain is actually left off such as `.com`).

Our third expression is `([a-z\.]{2,6})` which is one we have already seen. It searches for a wide variety of expressions containing lowercase letters and/or a period, but set by a quantifier range of `{2,6}` that. Many things could be searched for using this, including a top-level domain such as `.com`, `.org`, `.io`.  

Our final expression is `([\/\w \.-]*)` which casts a wide net for many different expressions. It includes a bracket expression that can match a forwardslash `\/`, alphanumeric characters `\w`, a period `\.`, and a dash `-`. Using another greedy quantifier it can match things 0 or more times due to the `*`. This matches many different routes following the main url following the form `/route/example/for-gist`.

As we can see we broke up essential parts of a url into subexpressions that we can use to verify a url. Each expression covers their own section making it easier to create a regex that can verify something that may be complicated.

### Bracket Expressions

The bracket expressions within our regex are whatever character classes or literals we choose to match placed inside of a two brackets `[]`. Bracket expressions match all characters that they include, meaning `[abc]` matches any a, b, or c character regardless of the length of the string (see `abracadabra` and `abaccaba`). You can also use a hyphen between a range of characters in ascending order, so `[a-c]` = `[abc]`. This also works with numbers where `[0123]` = `[0-3]`.

For this example, we'll take a closer look at the bracket expression `[\da-z\.-]` in our regex. As you can see it matches digits, lowercase characters, a period and a dash. This is a very flexible expression that will be used to match any character in a valid subdomain and second level domain due to the inclusion of the period with the `\.`. For example `blogpost.website-123.` will match this expression which is exactly the form we are looking for when matching the first two portions of our url following the scheme `https://`. 

Note we can create a negative character group, or a bracket expression that excludes any character of a certain pattern, but including a carrot `^` inside the bracket expression at the beginning. Therefor the expression `[^aeiouAEIOU]` looks for any string that does NOT contain a vowel.

### Greedy and Lazy Match

Greedy matching will find as many occurrences of a particular pattern as possible. Quantifiers are inherently greedy, and include:

* `*` -- matches the pattern zero or more times
* `+` -- Matches the pattern one or more times
* `?` -- Matches the pattern zero or one time
* `{}` -- Curly brackets can provide three different ways to set limits for a match:

These quantifiers can be made lazy by adding the `?` symbol after it, meaning it will match as few occurrences as possible.

In our regex we see all four of these methods being used. Since we have already talked about the squigly brackets `{}` regarding quantifiers, we will turn our attention to the `*`, `+`, and `?` symbols.

In our first grouping construct, we see a subexpression looking to match the scheme of a url, `(https?:\/\/)?`. Since the question mark `?` seeks to match 0 or 1 times, we can safely match both secure and insecure http protocols `https` or `http` respectively. Because the grouping construct ends with a quesiton mark as well, the http protocol does not need to be included for us to match a valid URL. In addition to those two instances of `?`, we see one more at the end of our entire regex trying to match a forward slash `\/?` one or more times.







`/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`


### Extra Topics

Our regex hasn't covered some important or more advanced topics when it comes to using regular expressions. You may want to do some extra research to learn about these powerful tools that can help you match expressions more cleanly.

- OR operator
- Flags
- Boundaries
- Back-references
- Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
