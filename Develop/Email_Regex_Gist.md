# Email Regex

Tutorial explaining how an email Regex works to verify that the characters entered for an email are allowed. 
This tutorial will cover the different components that make up a Regex and how they are used to validate an email address.

## Summary

A Regex is a sequence of characters that defines a search pattern for a text. The email Regex validates an email
address enetered by a user to see if it is acceptable or not. It checks to see 
if certain characters are before and after the @ symbol as well as the period usually before a .com. The Email Regex is below:

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [Character Escapes](#character-escapes)

## Regex Components

A regex is considered a literal, so the pattern must be wrapped in slash characters (/). Below is
 the email regex which starts and ends with a slash (/).

` / ^ ([a-z0-9_\.-]+) @ ([\da-z\.-]+) \. ([a-z\.]{2,6}) $ /`

### Anchors

The characters ^ and $ are anchors. The ^ anchor represents the begining of the string, the characters after it 
are only allowed to be the characters in the [].:

* An exact string match, such as ^The, where the strings "The" or "The person" match, but "the" and "the person"
 do not. This is because a regex is case-sensitive.

* A range of possible matches, displayed using bracket expressions. [ abc ]


This can be seen in the email Regex

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

The first part, `/^([a-z0-9_\.-]+)`, which immediately follows the ^,  means that the begining of the email can
only have the characters that are included after the ^ up to the @ symbol. In this case it allows for a 
lowercase letter or number or underscore or period or dash. The + after the ] bracket represents a quantifier, 
which will be explained in the next section.

The $ anchor represents the end of the string, the characters before it are only allowed to be the characters in 
the [].

The last part of the Email Regex, `([a-z\.]{2,6})$/`, only allows for the end of the email address(.com, .net, .edu) 
to be between 2 and 6 characters and can include a lowercase letter or a period

Below are some examples of email address' that would and wouldn't meet these requirements:

Allowed:

charlescallender@gmail.com \
charles.callender@gmail.edu \
charlescallender27@gmail.nets.

Not Allowed:

charles!#@gmail.com isn't allowed because it has a ! and # \
Charlescallender@gmail.com isn't allowed because it has a capital C \
charlescallender@gmail.88 isn't allowed because it ends with 88 \
charlescallender@gmail.com!! isn't allowed becuase it has ! points at the end


### Quantifiers

Quantifiers set the limits of the string that your regex matches (or an individual section of the string). They 
frequently include the minimum and maximum number of characters that your regex is looking for.

Quantifiers are inherently greedy, meaning they match as many occurrences of particular patterns as possible. 
They include the following:

* *—Matches the pattern zero or more times

* +—Matches the pattern one or more times

* ?—Matches the pattern zero or one time

* {}—Curly brackets can provide three different ways to set limits for a match:

    * { n }—Matches the pattern exactly n number of times

    * { n, }—Matches the pattern at least n number of times

    * { n, x }—Matches the pattern from a minimum of n number of times to a maximum of x number of times

Each of these quantifiers can be made lazy by adding the ? symbol after it, meaning it will match as few 
occurrences as possible.

Looking at the Email Regex, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, we can see that quantifiers are 
being used at the end, `\.([a-z\.] {2,6} )$/`, this part of the Regex is for the .com, .net, or .edu part of the 
email address. It sets the number of characters allowed at the end of the email address after the (.). In this, it 
allows for between 2 and 6 characters.

A quantifier is also used at the end of `/^([a-z0-9_\.-] + )` and `([\da-z\.-] + )` in the form of a + symbol. The 
plus symbol means that the pattern has to match 1 or more times.

Below are some examples of email address' that would and wouldn't meet this requirement:

Allowed:

charlescallender@gmail.com \
charlescallender@uw.edu \
charlescallender_88@gmail-88.com

Not Allowed:

charlescallender@gmail.emailaddress isn't allowed because it has too many characters after the . \
charlescallender@gmail.c isn't allowed because it doesn't have enough characters after the . \
@gmail.com isn't allowed because the + symbol requires the pattern match 1 or more times

### Grouping Constructs

Grouping constructs are used to break the string a Regex is being applied to up into several groups or subexpressions.

For example, charlescallender@gmail.com, using the email Regex, would be  broken up into 3 parts,
charlescallender, gmail, com.

The primary way you group a section of a regex is by using parentheses ().

Looking at the Email Regex, `/^ ([a-z0-9_\.-]+) @ ([\da-z\.-]+) \. ([a-z\.]{2,6}) $/`, we can see that there are 3 
groups/subexpressions:

1. `([a-z0-9_\.-]+)`
2. `([\da-z\.-]+)`
3. `([a-z\.]{2,6})`


The entire Regex expression is considered group 0.

### Bracket Expressions

Anything inside a set of square brackets ([]) represents a range of characters that we want to match. These 
patterns are known as bracket expressions. We can write these expressions to include all of the characters we 
want to match. For example, [abc] will look for a string that includes a or b or c, regardless of the length of 
the string. So all of the following examples would match: "aaa", "bin" "court", "abracadabra", and "bca".

The dash inbetween the letters represents all the characters inbetween. [a-c] = [abc]

Examples of some common bracket expressions are:

* [a-z]—The string can contain any lowercase letter between a–z. Keep in mind that this looks for lowercase 
characters only. If we wanted to include uppercase characters, we would need to change the expression to [a-zA-Z].

* [0-9]—The string can contain any number between 0–9

We can see bracket notation being used in the Email Regex, `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, 
in each group.

`/^( [a-z0-9_\.-] +)` uses bracket notation to allow for a lowercase letter or number or underscore or period or 
dash

`( [\da-z\.-] +)` uses bracket notation to allow for a number or a lowercase letter or period or dash, \d is the 
equivalent of [ 0-9 ]

`( [a-z\.] {2,6})$/` uses bracket notation to allow for a lowercase letter or period

Allowed

charles@aol.com \
charles@88.com \
charles12.-_me@gmail.edu

Not Allowed

charles!@gmail.com isn't allowed becuase of the ! \
charles##@gmail.com isn't allowed because of the # \
charles@.com isnt allowed because there are no characters after the @ \
charles@gmail.eduuuuuuuuuuuuuuu isn't allwed because there are more than 6 characters after the last period \
charles@gmail_.com isn't allowed because of the _

### Character Classes

A character class in a regex defines a set of characters, any one of which can occur in an input string to 
fulfill a match. Character classes usually are between [] brackets.

Here are some common character classes:

* .—Matches any character except the newline character (\n)

* \d—Matches any digit. This class is equivalent to the bracket expression [0-9].

* \D-Oppostie of \d, matches everything that's not [0-9].

* \w—Matches any alphanumeric character from the basic Latin alphabet, including the underscore (_). This class 
is equivalent to the bracket expression [A-Za-z0-9_].

* \W-Opposite of \w, matches everything that's not [A-Za-z0-9_].

* \s—Matches whitespace, tabs and spaces

* \S-Opposite of \s, matches everything that's not whitespace

Each of the last three character classes can be changed to perform an inverse match by capitalizing the letter 
character. For example, \D matches a non-digit character.

The \d character class is being used in the second group of the Email Regex, `([ \d a-z\.-]+)`, which allows a 
number 0-9 to be incuded in that part of the email address.

An example that follows this pattern would be gmail or .com or .edu or gma.il. or gmail22


### Character Escapes

The backslash (`\`) in a regex escapes a character that otherwise would be interpreted literally. Character 
classes are used with character classes to allow them to represent a class of characters rather than 1 character. 
For example, the Email Regex `/^([a-z0-9_ \. -]+)@([\da-z \. -]+) \. ([a-z \. ]{2,6})$/` uses character escapes
in 4 places before the period, (`\.`). This means a literal period.

It's important to note that all special characters, including the backslash (`\`), lose their special 
significance inside bracket expressions. For example, in the subexpression ([\da-z\.-]+), the \d doesn't 
represent a literal d and instead represents a digit.


## Author

My github username is cj8355 and my github can be found at: https://github.com/cj8355
