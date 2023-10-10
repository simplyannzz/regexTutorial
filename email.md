# REGEX Tutorial: Matching an Email

Welcome to this amazing, simple tutorial on matching an email regular expression (regex)!

There are many methods to find a string that contains a certain letter or phrase. One of the ways is by using regular expressions!

A regular expression (Regex) is a series of special characters that define a search pattern.

## Summary

We will learn the basics of regex and the search pattern for email validation.

This is the breakdown for email:

- contain any lowercase letter between a-z
- contain any number between 0-9
- contain a metacharacter (\.-\_)
  contain three parts: local, domain, and top-level domain.
- 2–6 characters long for the top-level domain

Regex are universal and can be used in all programming languages.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Character Escape](#character-escape)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)

## Regex Components

Regex is considered a literal, so the pattern must be wrapped in slash characters (/).

"Matching an email" regex:
\/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

Comment: Javascript provides two ways to create a regex object. The first, shown in the example above, uses literal notation. The second is the constructor. The constructors are not enclosed within slashes; instead, they use quotation marks.

### Anchors

The characters ^ and $ are both considered anchors.

The ^ anchor signifies a string that begins with the characters that follow it. It has one of two formats:

- An extact string match, such as ^The, where the strings "the" or "the person" match but "the" or "the person" don't. This is because regex is case-sensitive.
  A range of possible matches is displayed using bracket expressions.

The $ anchor signifies a string that ends with the characters that precede it. It can be preceded by an exact string or a range of possible matches.

So in "matching an email" regex, the string starts and ends with something that matches the pattern \([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.].

Anchors play a vital role in defining the position of the pattern within the input string and ensuring accurate and reliable validation.

In the context of email validation, anchors are important because they ensure the intended email address adheres to the specified pattern.

### Quantifiers

Quantifiers set the limits of the string that regex matches (or an individual section of the string). They frequently include the minimum and maximum number of characters that your regex is looking for.

Quantifiers are greedy, meaning they match as many instances of particular patterns as possible. They include the following:

- - : matches the pattern zero or more times
- - : matches the pattern one or more times
- ? : matches the pattern zero or one time
- {} : curly brackets can provide three different ways to set limits for a match:
    - {n} : matches the pattern exactly n number of times
    - {n,} : matches the pattern at least n number of times
    - {n, x} : matches the pattern from a minimum of n times to a maximum of x times.

Each of these quantifiers can be made lazy by adding the ? symbol after it, meaning it will match as few instances as possible.

The + quantifier means "one or more" is used after the pattern \[a-z0-9_\.-] captures the group \([a-z0-9_\.-]+). This means it should occur at least once, but it can also occur multiple times consecutively. This also applies to \[da-z\.-].

Now, let's look at how quantifiers are used in the "matching an email" regex. We have the quantifier {2,6}, meaning this sequence of 2–6 lowercase letters or dots. The email address must end with a two- to six-letter domain, such as.com,.edu, or.co.uk.

Looking at this expression, \/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ matches the valid email address that starts with one or more lowercase letters, digits, underscores, dots, or hyphens, followed by @, followed by more digits, lowercase letters, dots, or hyphens, followed by a period, and a two- to six-letter domain.

The regex above matches a valid email address:

- one or more lowercase letters, digits, underscores, dots, or hyphens
- followed by @
- followed by one or more digits, lowercase, dots, or hyphens
- followed by a period
- ending with a two- to six-letter domain (.com,.edu,.co.uk).

### Grouping and Capturing

The "matching an email" regex is fairly straightforward and open-ended about what it accepts. As it grows more complicated, we often need multiple parts of a string to determine that different sections fulfill different requirements. To break these sections up, you'll need to use grouping constructs.

The primary way you group a section of regex is by using parentheses (). Each section within parentheses is known as a subexpression. The purposes of ():

- applying quantifiers to a group of characters
- capturing the designated part of the match for later use
- creating backreference for a previously matched group
- applying alternation to a group of characters.

Matching an email has three parts:

1. Local
2. Domain
3. Top-level domain

4. Local:
     \([a-z0-9_\.0]+), this group is the local part of the email address before the @.

For example: annie_doe1!@gmail.com
The local part is annie_doe1! This local follows a valid format by allowing a combination of lowercase, numbers, underscores, dots, and hyphens.

2. Domain:
      \([\da-z\.-]+) corresponds to and matches the domain name.

The valid format is:

- numbers : \d
- lowercase letters: a-z
- dots: .
- hyphens: -

For example: mocha@mocha-domain1234.com
This example matches the regex format.

3. Top-level domain:
       \([a-z\.]{2,6}) is the top-level domain.

For example: mocha1!@example.com
The top level is.com.

All of those parts follow a combination of letters, numbers, dots, hyphens, and underscores, with a length constraint of 2 to 6 characters.

### Bracket Expressions

Anything inside a set of square brackets [] represents a range of characters that we want to match. These patterns are known as bracket expressions, but they are also known as positive character groups because they outline the characters we want to include.

For example, \[aeiou] will look for a string that includes a, e, i, o, or u, regardless of the length of the string. All of these examples would match: "ant,", "eat", "ice", "oooh", and "under".

You will more commonly see a hyphen (-) used between alphanumeric characters (letters and numbers only) to represent a range of those possible characters. This means that \[a-c] and \[abc] will look for the exact same thing.

We can break down the bracket for "Matching an email" regex as follows:
\/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

Part 1: local \/^([a-z0-9_\.-]+)
example: mocha1!@example.com
mocha1! is the local

- a-z : matches a lowercase letter
- 0-9 : matches the digits or numbers
- \_ : matches underscore
- \. : matches a literal period. The blackslash is used to escape the dot since it has a special meaning in regex.
- - : matches the hyphen character

Part 2: Domain \[\da-z\.-]
example: mocha1!@example.com
example.com is the domain.

- \d : matches the digits or numbers
- a-z : the lowercase letters
- \. : matches the period
- - : matches the hyphen

Part 3: Top-Level Domain \[a-z\.]{2,6}
example: mocha1!@example.example.edu
example.edu is the local

- a-z : matches lowercase letters
- \. : dots
- {2,6} : matches the quantifier.

It is important to note that a bracket expression can be turned into a negative character group by adding the ^ to the beginning of the expression inside the brackets. A common example is matching a string that doesn't include any vowels. The pattern \[^aeiouAEIOU] would find any strings that don't include lowercase or uppercase vowels.

### OR Operator

The bracket expression doesn't have to meet all of the requirements in the pattern.

We want to write the same logic outside of a bracket expression, especially within a grouping construct or between different grouping constructs.

Using the OR operator |, the expression \[abc] could be written as [a|b
|c]. Using our example in the grouping constructs section, we can take the original expression: (abc):(xyz), and then use the OR operator to convert it to the following: (a|b|c): (x|y|z).

### Character Classes

A character class in a regex defines a set of characters, any one of which can occur in an input string to fulfill a match.

Some of the common character classes are:

- . : matches any character except the newline character \n
- \d : matches any arabic numberical digit. This class is equivalent to the bracket expression [0-9].
- \w : matches any alphanumeric character from the basic Latin alphabet, including the underscore \_. This class is equivalent to the bracket expression \[a-zA-Z0-9].
- \s : matches a single whitespace character, including tabs and line breaks.

Each of the last character classes can be changed to perform an inverse match by capitalizing the letter character. For example, \D matches a non-digit character.

In our tutorial: \/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ uses various regex elements, including character classes, character sets, metacharacters, and repeating character classes.

Character class: \d and .. characrter sets are defined within the square brackets \[a-z], \[0-9], and [.-]. Those sets represent multiple characters, allowing a single character to match from the specified range. In our example, the \d is the class, and \[a-z] and \[A-Z] are the sets.

Metacharacter is the (.). Inside some character classes, some metacharacters lose their special meaning and are treated as literals. In our email example, the (-) and (.) are metacharacters inside the \[a-z0-9_.-] and \[\da-z.-].

Repeating character: The regex uses the + and {2,6} quantifiers to indicate repeating character classes.

### Character Escape

The backslash \ in regex escapes a character that otherwise would be interpreted literally. For example, the open curly brace { is used to begin a quantifier, but adding a blackslash before the open curly brace \{ means the regex should look for the open curly brace character instead of beginning to define a quantifier. This is common when looking for strings with special characters that are the same as a particular component of a regex.

All the special characters, including the blackslash \, lose their special meaning inside bracket expressions.

In our tutorial, the \. ensures the dot is treated as a literal period instead of a metacharacter with a wildcard meaning.

Example:

1. annie@example.com (valid)
2. annie@example@example.com (invalid)

By using \. , we ensure the regex only matches valid email addresses with literal periods in the appropriate positions, preventing the dot from acting as a wildcard and allowing for more accurate pattern matching.

### Flags

Regex is literal, so it must be wrapped in slash characters. The one exception to this rule is with the component known as flags. Flags are placed at the end of a regex, after the second slash, and define additional functionality or limits for the regex. There are six optional flags that can be used, either separately or together and in any order.

This is the most common:

- g : global search - the regex should be tested against all possible matches in a string.
- i : case-insensitive search - case should be ignored while attempting a match in a string
- m : multi-line search: a multi-line input string should be treated as multiple lines.

## Author

Github: https://github.com/simplyannzz

Deployed Gist: https://gist.github.com/simplyannzz/46a10c90fbe846351412a683a38bc85d

Github repo: https://github.com/simplyannzz/regexTutorial
