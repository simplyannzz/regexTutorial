# REGEX Tutorial: Matching an Username


There are many methods to find a string that contains a certain letter or phrase. One of the ways is using regular expression!

Regular Expression (Regex) are series of special characters that define a search pattern.

## Summary

We will learn the basic of regex and the search pattern for username validation.

This is the breakdown for username:
- contain any lowercase letter between a-z
- contain any number between 0-9
- contain underscore or hyphen
- 3-16 characters long

Regex are universal and can be used within all programming languages.



## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Character Escape](#character-escapes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)


## Regex Components

Regex is considered a literal, so the pattern must be wrapped in slash characters (/).

"Matching a username" Regex:
/^[a-z0-9_-]{3,16}$/

Comment: Javascript provides two ways to create a regex object. The first is shown in the example aboe, uses literal notation. The second is constructor. The constructor are not enclosed within slashes; instead they use quotation marks.

### Anchors

The characters ^ and $ are both considered be anchors.

The ^ anchor signifies a string that begins with the characters that follow it. It has one of two format:

- An extact string match, such as ^The, where the strings "The" or "The person" match, but "the" or "the person" don't/ This is because regex is case-sensitive.
- A range of possible matches, displayed using bracket expressions.

The $ anchor signifies a string that ends with the characters taht precede it. It can be preceded by an extact string or a range of possible matches.

So in "matching a username" regex, the string much start and end with something that matches the pattern [a-z0-9_-].

### Bracket Expressions

Anything inside a set of square brackets [] represents a range of characters that we want to match. These patterns are kown as bracket expressions, but they are also known as positive character group, because they outline the characters we want to include.

For example, [aeiou] will look for a string that includes a, e ,i, o, or u regardless of the length of the string. All of this example would match: "Ant", "eat", "ice", "oooh", and "under".

You will see more commonly see a hyphen (-) used between alphanumeric characters (letters and numbers only) to represent a range of those possible characters. This means that [a-c] and [abc] will look for the extact same thing.

We can break down the bracket for "Matching a Username" regex:

- [a-z] : The string can contain any lowercase letter between a-z. This looks for lowercase only. If we want to include uppercase characters, we could need to change the expression to [a-zA-Z]. -[0-9] : The string can contain any number between 0-9.
- [_-]: The string contain an underscore or hyphen are called special characters. Special characters include any non-alphanumeric characters such as punctuation or symbols.

If we both all the expression together then we form a pattern [a-z0-9_-], this pattern can be in any order. It doesn't require a string to meet all of those requirements.

It is important to note that a bracket expression can be turned into a negative character group by adding the ^ to the beginning of the expression inside the brackets. A common example is matching a string that doesn't include any vowels. The pattern [^aeiouAEIOU] would find any strings that don't include lowercase or uppercase vowels.

### Quantifiers

Quantifiers set the limits of the string that regex matches (or an individual section of the string). They frequently include the minimum and maximum number of characters taht your regex is looking ofr.

Quantifiers are greedy, meaning they match as many occurences of particular patterns as possible. They include the following:

- - : matches the pattern zero or more times
- - : matches the pattern one or more times
- ? : matches the pattern zero or one time
- {} : curly brackets can provide 3 different ways to set limits for a match:
  - {n} : matches the pattern exactly n number of times
  - {n,} : matches the pattern at least n number of times
  - {n, x} : matches the pattern from a minimum of n number of times to a maximum of x number of tiems

Each of these quantifiers can be made lazy by adding the ? symbol after it, meaning it will match as few occurences as possible.

Now let's look at how quantifiers are used in the "matching a username" regex. We have the quantifier {3,16}. This mean that we want to find the preceding string pattern a miniumum of 3 times and max of 16 times. The quantifier mean hat this string has to be between 3 and 16 characters.

This matches the requirement:

- 123
- l3rn-antin0_1
  \*note: String doesn't need to meet all of the requirements-just any of them

The following examples doesn't match:

- 25
- L3RN-antino0_1
  -l3rn-antin0_am1k0
  -l3rn\*antin0?1

### Grouping and Capturing

The "matching a username" regex is fairly straightforward and open-ended about what it accepts. As it grow more complicated, we many need multiple parts of a string to determine that different sections fulfill different requirement. To break these sections up, you'll need to use grouping constructs.

The primary way you group a section of regex is by using parentheses (). Each section within parentheses is known as a subexpression.

The following example contain groupoing constructs/subexpression:
(abc):(xyz)

The first subexpresion is looking for "abc" and second is looking for "xyz". In between the subexpression, we have a colon :. Unlike bracket expressions, subexprssions look for an exact match unlewss they're told to do otherwise.

Grouping constructors have two primary categories: capturing and non-capturing. Capturing groups capture the matched characters sequences for possible re-use (including numbered backreference) while non-capturing groups do not. A grouping construct can be made non-capturing by adding the characters ?: at the beginning of an expression inside the parenthese.

### OR Operator

Bracket expression doesn't have to meet all of the requirement in the pattern.

We want to write the same logic outside of a bracket expression, espically within a grouping construct or between different grouping constructs.

Using the OR operator |, the expression [abc] could be written as [a|b
|c]. Using our example in grouping constructs section, we can take the original exprssion: (abc):(xyz) and then use the OR operator to convert it to the following: (a|b|c) : (x|y|z).

### Character Escapes

The backslah \ in regex escapes a character taht otherwise would be interpreed literally. For example, the open curly brace { is used to begin a quantifier but adding blackslash before the open curly brace \{ mean the regex should look for the open curly brace charcter isntead of beginning to define a quantifier. This is common when looking for strings with speical characters taht are the same as a particular component of a regex.

All the speical characters including the blackslash \, lose their speical significane inside bracket expressions.

### Character Classes
Character class in a regex defines a set of characters, any one of whic can occur in an input string to fulfill a match.

Some of the common character classes:
- . : matches any character except the newline character \n
- \d : matches any arabic numberical digit. This class is equivalent to the bracket expression [0-9].
- \w : matches any alphanumeric character from basic latin alphabet, including the underscore _. This class is equivalent to the bracket expression [a-zA-Z0-9].
- \s : matches a single whitespace character, including tabs and line breaks

Each of the last character classes cab be changed to perform an inverse match by capitalizing the letter character. For example, \D matches to a non-digit character.

### Flags
Regex is a literal, so it must be wrapped in slash characters. The one exception to this rule is with the componenet known as flags. Flags are placed at the end of a regex, after the second slash, and define additonal functionality or limits for the regex. There are six optional flags that can be used, either seperately or together and in any order.

This is the most common:
- g : global search - the regex should be tested against all possible matches in a string
- i : case-insensitive search - case should be ignored while attempting a match in a string
- m : multi-line search - a multi-line input string shuld be treated as multiple lines.

## Author

Annie Bui, a Full-stack development student @ University of Minnesota Bootcamp. This is my github: https://github.com/simplyannzz
