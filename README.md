# Regular Expression Cheat Sheet

# SYNTAX:

const pattern = new RegExp(pattern, attributes);

## attributes:

`g` (global);

`i` (case-sensitive);

`m` (multiline matches)

### Example:

```javascript
const str = "Bla-bla-bla foam";
const regexp = new RegExp(/foam/gim);

const res = str.match(regexp);
console.log("res :>> ", res); // res >> Array [ "foam" ]
```

# ANY SINGLE CHARACTERS

`.`: Matches any character other than newline (or including line terminators with the /s flag)

```javascript
const regexp = new RegExp(/./); // >> res Array [ "a" ]
const regexp = new RegExp(/./g); // >> res Array(7) [ "a", " ", "b", " ", "c", ".", " " ]
const regexp = new RegExp(/.+/g); // >> res Array [ "a b c. " ]
//   const regexp = new RegExp(/.+/); // res >> Array [ "a b c. " ]
const str = "a b c. ";
```

# BRACKETS:

`[b]`: Any one character between the brackets.

```javascript
const regexp = new RegExp(/[b]/); // >> Array [ "b" ]
const regexp = new RegExp(/[b]/gim); // >> Array(3) [ "B", "b", "b" ]
const str = "Bla-bla-bla without foam. ";
```

`[^abc]`: Any one character not between the brackets.

```javascript
const regexp = new RegExp(/[^abc]/); // res >> Array [ "A" ]
const regexp = new RegExp(/[^abc]+/); // res >> Array [ "Anything " ]
const regexp = new RegExp(/[^abc]+/g); // res >> Array(3) [ "Anything ", "ut ", ". " ]
const str = "Anything but abc. ";
```

`[0-9]`: It matches any decimal digit from 0 through 9.

```javascript
const regexp = new RegExp(/[0-9]/gim); // res >> Array(7) [ "5", "6", "7", "5", "4", "3", "5" ]
const regexp = new RegExp(/[0-9]+/gim); // res >> Array [ "5675", "435" ]
const regexp = new RegExp(/[0-9]+/); // res >> Array [ "5675" ]
const str = "Bla-bla-bla yuch5675 without foam 435. ";
```

`[a-z]`: It matches any character from lowercase a through lowercase z.

```javascript
const regexp = new RegExp(/[a-z]/); // res >> Array [ "n" ]
const regexp = new RegExp(/[a-z]/g); // res >> Array(5) [ "n", "l", "y", "a", "z" ]
const regexp = new RegExp(/[a-z]+/); // res >> Array [ "nly" ]
const regexp = new RegExp(/[a-z]+/g); // res >> Array(3) [ "nly", "a", "z" ]
const regexp = new RegExp(/[a-z]+/gim); // res >> Array(3) [ "Only", "a", "z" ]
const regexp = new RegExp(/[^a-z]+/g); // res >> Array(3) [ "O", " ", "-" ]
const str = "Only a-z";
```

`[A-Z]`: It matches any character from uppercase A through uppercase Z.

```javascript
const regexp = new RegExp(/[A-Z]/); // res >> Array [ "B" ]
const regexp = new RegExp(/[A-Z]/g); // res >> Array [ "B", "W" ]
const regexp = new RegExp(/[a-zA-Z]+/g); // res >> Array(6) [ "Bla", "bla", "bla", "yuch", "Without", "foam" ]
const str = "Bla-bla-bla yuch5675 Without foam 435. ";
```

# QUANTIFIERS:

`a+`: Matches one or more consecutive `a` characters.

```javascript
const regexp = new RegExp(/a+/g); // res >> Array(6) [ "a", "aa", "aaa", "aaaa", "a", "aa" ]
const str = "a aa aaa aaaa bab baab";
```

`a*`: It matches zero or more consecutive `a` characters.

```javascript
const regexp = new RegExp(/ba*/g); // res >> Array(4) [ "ba", "baa", "ba", "b" ]
const str = "a ba baa aaa ba b";
```

`a?`: Matches an `a` character or nothing.

```javascript
const regexp = new RegExp(/ba?/g); // >> res Array [ "ba", "b" ]
const str = "ba b a";
```

`a{N}`: It matches any string containing a sequence of N as.

```javascript
const regexp = new RegExp(/a{3}/g); // >> res Array [ "aaa", "aaa" ]
const str = "a aa aaa aaaa";
```

p{3,6}: It matches any string containing a sequence of two or three ps.

```javascript
const regexp = new RegExp(/a{3,6}/g); // >> res Array(4) [ "aaa", "aaaa", "aaaaaa", "aaaa" ]
const str = "a aa aaa aaaa aaaaaaaaaa";
```

p{3, }: It matches any string containing a sequence of at least two ps.

```javascript
const regexp = new RegExp(/a{3,}/g); // >> res Array(4) [ "aaa", "aaaa", "aaaaaa", "aaaa" ]
const str = "a aa aaa aaaa aaaaaaaaaa";
```

p$: It matches any string with p at the end of it.
^p: It matches any string with p at the beginning of it.

# LITERAL CHARACTERS:

Alphanumeric: Itself.
\0: The NUL character (\u0000).
\t: Tab (\u0009).
\n: Newline (\u000A).
\v: Vertical tab (\u000B).
\f: Form feed (\u000C).
\r: Carriage return (\u000D).

# METACHARACTERS:

.: a single character.
\s: a whitespace character (space, tab, newline).
\S: non-whitespace character.
\d: a digit (0-9).
\D: a non-digit.
\w: a word character (a-z, A-Z, 0-9, \_).
\W: a non-word character.
[\b]: a literal backspace (special case).
[aeiou]: matches a single character in the given set.
[^aeiou]: matches a single character outside the given set.
(foo|bar|baz): matches any of the alternatives specified.

# REGULAR EXPRESSIONS PROPERTIES:

constructor: Specifies the function that creates an object prototype.
global: Specifies if the "g" modifier is set.
ignoreCase: Specifies if the "i" modifier is set.
lastIndex: The index at which to start the next match.
multiline: Specifies if the "m" modifier is set.
source: The text of the pattern.

# REGULAR EXPRESSIONS METHODS:

exec(): Executes a search for a match in its string parameter.
test(): Tests for a match in its string parameter.
toSource(): Returns an object literal representing the specified object; you can use this value to create a new object.
toString(): Returns a string representing the specified object.

# STRING METHODS:

String.match(pattern): Matches given string with the RegExp. Returns an array containing the matches, a string or null.
String.search(pattern): Matches RegExp with string and returns the index of the beginning of the match if found, -1 if not.
String.replace(pattern,string): Replaces matches with the given string, and returns the edited string.
String.split(pattern): Cuts a string into an array, making cuts at matches.

# 8 REGULAR EXPRESSIONS YOU SHOULD KNOW:

Matching a Username: /^[a-z0-9_-]{3,16}$/
Matching a Password: /^[a-z0-9_-]{6,18}$/
Matching a Hex Value: /^#?([a-f0-9]{6}|[a-f0-9]{3})$/
Matching a Slug: /^[a-z0-9-]+$/
Matching an Email: /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
Matching a URL: /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
Matching an IP Address: /^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/
Matching an HTML Tag: /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
