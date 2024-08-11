#MOC/DevOps #note/boat🚤 #note/develop🍃 

- It's called a __RegEx__
- It's a sequence of characters that define a search pattern.
- It is mainly for use in pattern matching with strings, or string matching (i.e. it operates like a “find and replace” command)
- We can use it with a lot of programming languages like [[Python MOC|python]]
- One thing you have to be careful with is that different languages use different regex engines.
- Syntax: `/pattern/modifier(s)`
```js
let pattern = /corn/i;
```
## Modifiers
| Modifier                                                 | Description                       |
| -------------------------------------------------------- | --------------------------------- |
| [/g](https://www.w3schools.com/jsref/jsref_regexp_g.asp) | Perform a global match (find all) |
| [/i](https://www.w3schools.com/jsref/jsref_regexp_i.asp) | Perform case-insensitive matching |
| [/m](https://www.w3schools.com/jsref/jsref_regexp_m.asp) | Perform multiline matching        |
## Brackets(Ranges)

| Bracket                                                                  | Description                                                 |
| ------------------------------------------------------------------------ | ----------------------------------------------------------- |
| [\[abc\]](https://www.w3schools.com/jsref/jsref_regexp_charset.asp)      | Find any character between the brackets                     |
| [\[^abc\]](https://www.w3schools.com/jsref/jsref_regexp_charset_not.asp) | Find any character __NOT__ between the brackets             |
| [\[0-9\]](https://www.w3schools.com/jsref/jsref_regexp_0-9.asp)          | Find any character between the brackets (any digit)         |
| [\[^0-9\]](https://www.w3schools.com/jsref/jsref_regexp_not_0-9.asp)     | Find any character NOT between the brackets (any non-digit) |
| [(x\|y)](https://www.w3schools.com/jsref/jsref_regexp_xy.asp)            | Find any of the alternatives specified __OR__               |
### Examples
```js
/[a-z]/ // small characters
/[^a-z]/ //NOT small

/[abc]/ // ANY character in this

/[A-Z]/ // Chapital characters
/[^A-Z]/ // NOT Cap characters

/[a-zA-Z] // Capital and Small characters
/[^a-zA-Z] // NOT Capital and Small characters

/[a-zA-Z0-9]/ // Capital and Small and Numbers
/[^a-zA-Z0-9]/ // NOT Capital and Small and Numbers

/[^a-z^A-Z0-9]/ // NOT Capital and Small and Numbers and ^
```
## Character Classes
| Character                                                              | Description                                                                                 |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| [.](https://www.w3schools.com/jsref/jsref_regexp_dot.asp)              | Find a single character, except newline or line terminator                                  |
| [\w](https://www.w3schools.com/jsref/jsref_regexp_wordchar.asp)        | Find a word character                                                                       |
| [\W](https://www.w3schools.com/jsref/jsref_regexp_wordchar_non.asp)    | Find a non-word character                                                                   |
| [\d](https://www.w3schools.com/jsref/jsref_regexp_digit.asp)           | Find a digit                                                                                |
| [\D](https://www.w3schools.com/jsref/jsref_regexp_digit_non.asp)       | Find a non-digit character                                                                  |
| [\s](https://www.w3schools.com/jsref/jsref_regexp_whitespace.asp)      | Find a whitespace character                                                                 |
| [\S](https://www.w3schools.com/jsref/jsref_regexp_whitespace_non.asp)  | Find a non-whitespace character                                                             |
| [\b](https://www.w3schools.com/jsref/jsref_regexp_begin.asp)           | Find a match at the beginning/end of a word, beginning like this: \bHI, end like this: HI\b |
| [\B](https://www.w3schools.com/jsref/jsref_regexp_begin_not.asp)       | Find a match, but not at the beginning/end of a word                                        |
| [\0](https://www.w3schools.com/jsref/jsref_regexp_nul.asp)             | Find a NULL character                                                                       |
| [\n](https://www.w3schools.com/jsref/jsref_regexp_newline.asp)         | Find a new line character                                                                   |
| [\f](https://www.w3schools.com/jsref/jsref_regexp_formfeed.asp)        | Find a form feed character                                                                  |
| [\r](https://www.w3schools.com/jsref/jsref_regexp_carriagereturn.asp)  | Find a carriage return character                                                            |
| [\t](https://www.w3schools.com/jsref/jsref_regexp_tab.asp)             | Find a tab character                                                                        |
| [\v](https://www.w3schools.com/jsref/jsref_regexp_vtab.asp)            | Find a vertical tab character                                                               |
| [\xxx](https://www.w3schools.com/jsref/jsref_regexp_octal.asp)         | Find the character specified by an octal number xxx                                         |
| [\xdd](https://www.w3schools.com/jsref/jsref_regexp_hex.asp)           | Find the character specified by a hexadecimal number dd                                     |
| [\udddd](https://www.w3schools.com/jsref/jsref_regexp_unicode_hex.asp) | Find the Unicode character specified by a hexadecimal number dddd                           |
## Quantifiers
| Quantifier                                                          | Description                                                      |
| ------------------------------------------------------------------- | ---------------------------------------------------------------- |
| [n+](https://www.w3schools.com/jsref/jsref_regexp_onemore.asp)      | Matches any string that contains at least one _n_                |
| [n*](https://www.w3schools.com/jsref/jsref_regexp_zeromore.asp)     | Matches any string that contains zero or more occurrences of _n_ |
| [n?](https://www.w3schools.com/jsref/jsref_regexp_zeroone.asp)      | Matches any string that contains zero or one occurrences of _n_  |
| [n{X}](https://www.w3schools.com/jsref/jsref_regexp_nx.asp)         | Matches any string that contains a sequence of _X_ _n_'s         |
| [n{X,Y}](https://www.w3schools.com/jsref/jsref_regexp_nxy.asp)      | Matches any string that contains a sequence of X to Y _n_'s      |
| [n{X,}](https://www.w3schools.com/jsref/jsref_regexp_nxcomma.asp)   | Matches any string that contains a sequence of at least X _n_'s  |
| [n$](https://www.w3schools.com/jsref/jsref_regexp_ndollar.asp)      | Matches any string with _n_ at the end of it                     |
| [^n](https://www.w3schools.com/jsref/jsref_regexp_ncaret.asp)       | Matches any string with _n_ at the beginning of it               |
| [?=n](https://www.w3schools.com/jsref/jsref_regexp_nfollow.asp)     | Matches any string that is followed by a specific string _n_     |
| [?!n](https://www.w3schools.com/jsref/jsref_regexp_nfollow_not.asp) | Matches any string that is not followed by a specific string _n_ |
## Websites to help you
[Rubular: a Ruby regular expression editor](https://rubular.com/)
[Introducing Regular Expressions | PPT](https://www.slideshare.net/neha_jain/introducing-regular-expressions)
[Advanced regular expressions | PPT](https://www.slideshare.net/neha_jain/advanced-regular-expressions-80296518
[RegexOne - Learn Regular Expressions - Lesson 1: An Introduction, and the ABCs](https://regexone.com/)