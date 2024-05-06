# Regex-Tutorial

Regex, or Regular Expression, is a series of special characters that define a search pattern. Here, we will discuss the special characters that can be used in such a search such as Anchors, Quantifiers, OR Operators, Character Classes, Flags, Grouping and Capturing, Bracket Expressions, Greedy and Lazy Matches, Boundaries, Back-references, Lookarounds, etc.

## Summary

In exploring our search characters and expressions, we will be using validation of an email address as our example. Please note that we will be addressing only the search components used by JavaScript in this disussion. JavaScript provides two ways to create a regex object - literal notation or the use of a RegExp constructor (these are wrapped in quotation marks rather than slashes). In this tutorial, we will be using literal notation.

## Table of Contents

- [Regex Components](#regex-components)
- [Bracket Expressions](#bracket-expressions)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back References](#back-references)
- [Lookarounds](#lookarounds)
- [Regex Javascript Methods](#regex-javascript-methods)

## Regex Components

A regex is considered a literal, so the search pattern must be wrapped between slashes (<span style="color: magenta">/</span>) in our search expression. As you can see in the example below, the slash is followed by an anchor (<span style="color: magenta">^</span>) and the search characters themselves are wrapped inside square brackets (<span style="color: magenta">[]</span>).

Example:

<span style="color: magenta;">/^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)\*$/</span>

As you can see, our example has 3 separate bracket expressions as follows:

1. One for the part of the email address that comes before the "@" sign;
2. One for the domain name; and
3. One for .com, .net, etc.

We will break these down as we define the various Regex components.

### Bracket Expressions

The characters wrapped in brackets - our <span style="font-weight: bold;">Bracket Expression</span>, are the characters that we want to match. In this example:

- <span style="color: magenta;">[a-z]</span> means that any lowercase letter between a and z, and [A-Z] includes any uppercase letter between A and Z.

- <span style="color: magenta;">[0-9]</span> indicates that the string can contain any number between 0-9.

- <span style="color: magenta;">[_-]</span> indicates that the string can contain an underscore or hyphen. Wrapping these "special characters" in our bracket expression means we are searching for these characters, which can include non-alphanumeric characters, such as symbols or punctuation marks.

### Anchors

The anchor (<span style="color: magenta;">^</span>) indicates the start of a string or the start of a line, depending on a multiline search. However, it should be noted that an anchor that is inside square brackets, means <span style="color: magenta;">"not"</span>.

Conversely, the (<span style="color: magenta;">$</span>) anchor indicates the end of a string or end of a line, depending on multiline mode. Keep in mind that Regex is <span style="font-weight: bold;">case-sensitive</span> so that an exact string match, in the case of <span style="color: magenta;">^This</span>, <span style="color: magenta;">"This"</span> or <span style="color: magenta;">"This expression"</span> match, but <span style="color: magenta;">"this"</span> and <span style="color: magenta;">"this expression"</span> do not. (We will discuss the <span style="color: magenta;">{3-16}</span> in our search pattern in the next session addressing Quantifiers.)

### Quantifiers

A quantifier tells us "how many". In our example above, <span style="color: magenta;">{3,16}</span> indicates that the string must be between 3 and 16 characters long. Quantifiers are special expressions that govern the limits of the string that our regex must match and frequently include the minimum and maximum number of characters to be included in our search. Below is a list of quantifiers:

- <span style="color: magenta;">\*</span> matches the pattern zero or more times;
- <span style="color: magenta;">+</span> matches the pattern one or more times;
- <span style="color: magenta;">?</span> matches the pattern zero or one time;
- <span style="color: magenta;">{ }</span> Curly brackets can provide ways to limit matches:
  - <span style="color: magenta;">{ n }</span> matches the pattern exactly <span style="color: magenta;">n</span> number of times;
  - <span style="color: magenta;">{ n, }</span> matches the pattern at least <span style="color: magenta;">n</span> number of times;
  - <span style="color: magenta;">{ n, x }</span> matches the pattern from a minimum of <span style="color: magenta;">n</span> number of times to a maximum of <span style="color: magenta;">x</span> number of times.

### OR Operator

Because a bracket expression does not require the string to meet all of the requirements in the pattern, we will often want to add this same logic outside of a bracket expression.

Using the OR operator(<span style="color: magenta;">|</span>), we can write the expression <span style="color: magenta;">[abc]</span> as <span style="color: magenta;">(a|b|c)</span>.

Thus, we can take the original expression" <span style="color: magenta;">(abc):(xyz)</span> and use the OR operator to convert it to <span style="color: magenta;">(a|b|c):(x|y|z)</span>.

Now <span style="color: magenta;">"abc:xyz"</span>, <span style="color: magenta;">"acb:xyz"</span>, and <span style="color: magenta;">"a:z"</span> match but <span style="color: magenta;">"xyz:abc"</span> does not.

## Character Escapes

The backslash (<span style="color: magenta;">\\</span>) in a regex expression <span style="font-weight: bold;">escapes</span> a character that would otherwise be interpreted literally. For example, the open curly brace (<span style="color: magenta;">{</span>) is used to begin a quantifier, but the open curly brace can also be used with the backslash, thelling regex to look for the open curly brace character instead of defining it as the beginning of a quantifier. The backslash is used with any character that is typically used in a quantifier, when we need it in our regex expression as a special character.

### Character Classes

A <span style="font-weight: bold;">character class</span> defines a set of characters. Our bracket expression is a charcter class. Any set of characters that can occur in an input string tto fulfill a match is a character class. This applies to positive adn negative character groups.

The following are common character classes:

- <span style="color: magenta;">.</span> matches any character except the newline character (<span style="color: magenta;">\n</span>).
- <span style="color: magenta;">\d</span> matches any Arabic numeral digit, which is equivalent to the bracket expression <span style="color: magenta;">[0-9]</span>.
- <span style="color: magenta;">\w</span> matches any alphanumeric character from the basic Latin alphabet, including the underscore <span style="color: magenta;">[A-Za-z0-9_]</span>.
- <span style="color: magenta;">\s</span> matches a single whitespace character. This includes tabs and line breaks.
- By capitalizing the letter character in the last three character classes, we can perform an inverse matches (<span style="color: magenta;">\D</span>), (<span style="color: magenta;">\W</span>), and (<span style="color: magenta;">\S</span>).

### Flags

Flags are placed at the end of a refex, after the second slash. They define additional functionality ro limits for the regex. There are six optional flags we can use (separately or together, and in any order). Hereare the three we are likely to need:

- (<span style="color: magenta;">g</span>) is a global search. The regex should be tested against all possible matches in a string.
- (<span style="color: magenta;">i</span>) Case is to be ignored while attempting a match in a string (case insensitive search).
- (<span style="color: magenta;">m</span>) a multi-line input string should be treated as multiple lines.

### Grouping and Capturing

A complicated regex search, such as our example, can require multiple sections to fulfill different requirements, such as the 3 sections of an email address as discssed in the Regex Component section above.

In the case of our example, we will need <span style="font-weight: bold;">grouping constructs</span>. The primary method of grouping sections of a regex is using parentheses(<span style="color: magenta;">()</span>). These sections are known as <span style="font-weight: bold;">subexpressions</span>.

The first character before the bracket expression in our example is a forward slash (<span style="color: magenta;">/</span>), which denotes that this is the beginning of our regex expression.

The 2nd character is our anchor (<span style="color: magenta;">^</span>), which indicates the start of a string or the start of a line.

This is followed by the bracket expression of our first section<span style="color: magenta;">[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]</span>, in which our regex is looking at lowercase, uppercase, and numeric characters, as well as special characters (<span style="color: magenta;">.!#$%&’\*+/=?^\_`{|}~</span>). The final character in this section is a range indicator (<span style="color: magenta;">-</span>) (<span style="color: magenta;">-</span>).

In our second section (<span style="color: magenta;">+@[a-zA-Z0-9-]</span>), our regex is looking for one or more <span style="color: magenta;">+@</span> signs and lowercase, uppercase, and numeric characters. The final character in this section is a range indicator (<span style="color: magenta;">-</span>).

In our third section denoted by parens, (<span style="color: magenta;">+(?:\.[a-zA-Z0-9-]+)\*$/</span>), our regex is looking for one or more matches. The logic operator (<span style="color: magenta;">?:</span>) indicates a non-capturing group, which means our characters or expressions are grouped so that they do not capture the matched text. Using this syntax tells the regex engine not to store the matched text in a separate memory slot.

The backslash-dot (<span style="color: magenta;">\.</span>) tells our regex that we are using the dot as a special character rather than a regex component.

The bracket expression is looking for one or more matches of lowercase and uppercase letters from A to Z and numbers between 0 and 9.

The backslash-star (<span style="color: magenta;">\*</span>) indicates that we are using the star as a special character and not as a quantifier.

The dollar sign (<span style="color: magenta;">$</span>) denotes the end of our string and the forward slash (<span style="color: magenta;">/</span>) indicates that we are at the end of our regex expression.

### Greedy and Lazy Match

Quantifiers are inherently <span style="font-weight: bold;">"greedy"</span> and will match as many instances of these particular patterns as possible.

Each of these quantifiers can be made <span style="font-weight: bold;">"lazy"</span> by adding the <span style="color: magenta;">?</span> symbol after it, meaning it will match as few occurrences as possible.

### Boundaries

Boundaries indicate the beginnings and endings of lines and words, and other patterns indicating in some way that a match is possible, including look arounds (look-ahead, look-behind, and conditional expressions.)

### Back References

Backreferences refer to a previously captured group in the same regular expression.

### Lookarounds

Lookarounds can be used in both positive and negative expressions as follows:

- Positive lookahead <span style="color: magenta;">(?<=...>)</span>
- Positive lookbehind <span style="color: magenta;">(?<=...>)</span>
- Negative lookahead <span style="color: magenta;">(?!...)</span>
- Negative lookbehind <span style="color: magenta;">(?<!...)</span>

### Regex Javascript Methods

Regular expressions are used in JavaScript with theREgExp methods: test(). and exec(). and with the String methods match()., matchAll()., replace()., replaceAll()., search()., and split().

## Author

Phyllis Ann Lataille, a former Massachusetts resident and transplant to Colorado, who had previously enjoyed taking programming and web development courses in her spare time, decided to pursue a career as a web developer. She enrolled in a full-time coding bootcamp through the University of Denver and received her certification in its full-stack web development course. For additional information and to review the author's repositories, please visit the author's GitHub profile at https://github.com/lavendarqueen?tab=repositories
