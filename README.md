# Regular Expression Cheat Sheet

## SYNTAX:

const pattern = new RegExp(pattern, attributes);

### attributes:

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

## METACHARACTERS:

`.`: Matches any character other than newline (or including line terminators with the /s flag)

```javascript
const regexp = new RegExp(/./); // >> res Array [ "a" ]
const regexp = new RegExp(/./g); // >> res Array(7) [ "a", " ", "b", " ", "c", ".", " " ]
const regexp = new RegExp(/.+/g); // >> res Array [ "a b c. " ]
//   const regexp = new RegExp(/.+/); // res >> Array [ "a b c. " ]
const str = "a b c. ";
```

`\s`: a whitespace character (space, tab, newline) or `[\t\n\v\f\r ]`.

```
[^\s] === \S
```

```javascript
const regexp = new RegExp(/\s/g); // >> res Array [ " ", " " ]
const str = "any whitespace character";
```

`\S`: non-whitespace character.

```javascript
const regexp = new RegExp(/\S+/); // >> res Array [ "any" ]
const str = "any non-whitespace";
```

`\d`: a digit [0-9].

```javascript
const regexp = new RegExp(/\d/g); // >> res Array [ "1", "2" ]
const str = "one: 1, two: 2";
```

`\D`: a non-digit.

```
[^0-9] === \D
```

```javascript
const regexp = new RegExp(/\D+/); // >> res  Array [ "one: " ]
const str = "one: 1, two: 2";
```

`\w`: a word character [a-z, A-Z, 0-9, \_].

```javascript
const regexp = new RegExp(/\w+/g); // >> res  Array(3) [ "any", "word", "character" ]
const str = "any word character";
```

`\W`: a non-word character.

```javascript
const regexp = new RegExp(/\W+/g); // >> res  Array(3) [ ".", "@", "%" ]
const str = "not.a@word%character";
```

`[\b]`: a literal backspace (special case).

```javascript
const regexp = new RegExp(/\b/g); // >> res  Array(6) [ "", "", "", "", "", "" ]
const str = "not.a@w";
```

`[aeiou]`: matches a single character in the given set.

```javascript
const regexp = new RegExp(/[aeiou]+/g); // >> res  Array(12) [ "a", "e", "i", "e", "i", "aeiou", "a", "e", "e", "i", … ]
const str = "matches in the list aeiou (case sensitive)";
```

`[^aeiou]`: matches a single character outside the given set.

```javascript
const regexp = new RegExp(/[^aeiou]+/g); // >> res  Array(13) [ "m", "tch", "s ", "n th", " l", "st ", " (c", "s", " s", "ns", … ]
const str = "matches in the list aeiou (case sensitive)";
```

(foo|bar|baz): matches any of the alternatives specified.

```javascript
const regexp = new RegExp(/(foo|bar|baz)/g); // >> res  Array(3) [ "foo", "baz", "bar" ]
const str = "matches foo character baz in the list(case bar sensitive)";
```

## BRACKETS:

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

## QUANTIFIERS:

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

`a{N}`: It matches any string containing a sequence of N as.🥱

```javascript
const regexp = new RegExp(/a{3}/g); // >> res Array [ "aaa", "aaa" ]
const str = "a aa aaa aaaa";
```

`a{3,6}`: It matches any string containing a sequence of three or six as.

```javascript
const regexp = new RegExp(/a{3,6}/g); // >> res Array(4) [ "aaa", "aaaa", "aaaaaa", "aaaa" ]
const str = "a aa aaa aaaa aaaaaaaaaa";
```

`a{3, }`: It matches any string containing a sequence of at least three as.

```javascript
const regexp = new RegExp(/a{3,}/g); // >> res Array(4) [ "aaa", "aaaa", "aaaaaa", "aaaa" ]
const str = "a aa aaa aaaa aaaaaaaaaa";
```

`p$`: It matches any string with p at the end of it.

```javascript
const regexp = new RegExp(/\w+$/); // >> res Array [ "string" ]
const str = "end of string";
```

`^s`: It matches any string with s at the beginning of it.

```javascript
const regexp = new RegExp(/^\w+/); // >> res Array [ "start" ]
const str = "start of string";
```

`a*?`: It matches any string with a at the beginning of it.

```javascript
const regexp = new RegExp(/r\w*?/g); // >> res Array [ "start" ]
const str = "start of string";
```

## LITERAL CHARACTERS:

### Alphanumeric: Itself.

`\0`: The NUL character (\u0000).

`\t`: Tab (\u0009).

`\n`: Newline (\u000A).

`\v`: Vertical tab (\u000B).

`\f`: Form feed (\u000C).

`\r`: Carriage return (\u000D).

## REGULAR EXPRESSIONS PROPERTIES:

`constructor`: Specifies the function that creates an object prototype.

`global`: Specifies if the "g" modifier is set.

`ignoreCase`: Specifies if the "i" modifier is set.

`lastIndex`: The index at which to start the next match.

`multiline`: Specifies if the "m" modifier is set.

`source`: The text of the pattern.

## REGULAR EXPRESSIONS METHODS:

`exec()`: Executes a search for a match in its string parameter.

`test()`: Tests for a match in its string parameter.

`toSource()`: Returns an object literal representing the specified object; you can use this value to create a new object.

`toString()`: Returns a string representing the specified object.

## STRING METHODS:

`String.match(pattern)`: Matches given string with the RegExp. Returns an array containing the matches, a string or null.

```javascript
const paragraph = "The quick brown fox jumps over the lazy dog. It barked.";
const regex = /[A-Z]/g;
const found = paragraph.match(regex);
console.log(found); // Array ["T", "I"]
```

`String.search(pattern)`: Matches RegExp with string and returns the index of the beginning of the match if found, -1 if not.

```javascript
const paragraph =
  "The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?";
// any character that is not a word character or whitespace
const regex = /[^\w\s]/g;
console.log(paragraph.search(regex)); // 43
console.log(paragraph[paragraph.search(regex)]); // "."
```

`String.replace(pattern,string)`: Replaces matches with the given string, and returns the edited string.

```javascript
const p =
  "The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?";

console.log(p.replace("dog", "monkey"));
// expected output: "The quick brown fox jumps over the lazy monkey. If the dog reacted, was it really lazy?"

const regex = /Dog/i;
console.log(p.replace(regex, "ferret"));
// expected output: "The quick brown fox jumps over the lazy ferret. If the dog reacted, was it really lazy?"
```

`String.split(pattern)`: Cuts a string into an array, making cuts at matches.

```javascript
const str = "The quick brown fox jumps over the lazy dog.";

const words = str.split(" ");
console.log(words[3]);
// expected output: "fox"

const chars = str.split("");
console.log(chars[8]);
// expected output: "k"

const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]
```

# 8 REGULAR EXPRESSIONS YOU SHOULD KNOW:

## Matching a Username

```javascript
Matching a Username: /^[a-z0-9_-]{3,16}$/
```

We begin by telling the parser to find the beginning of the string (^), followed by any lowercase letter (a-z), number (0-9), an underscore, or a hyphen. Next, {3,16} makes sure that are at least 3 of those characters, but no more than 16. Finally, we want the end of the string ($).

#### String that matches:

`my-us3r_n4m3`

#### String that doesn't match:

`th1s1s-wayt00_l0ngt0beausername` (too long)

## Matching a Password

```javascript
Matching a Password: /^[a-z0-9_-]{6,18}$/
```

Matching a password is very similar to matching a username. The only difference is that instead of 3 to 16 letters, numbers, underscores, or hyphens, we want 6 to 18 of them ({6,18}).

#### String that matches:

`myp4ssw0rd`

#### String that doesn't match:

`mypa$$w0rd` (contains a dollar sign)

## Matching a Hex Value

```javascript
Matching a Hex Value: /^#?([a-f0-9]{6}|[a-f0-9]{3})$/
```

We begin by telling the parser to find the beginning of the string (^).

Next, a number sign is optional because it is followed a question mark. The question mark tells the parser that the preceding character — in this case a number sign — is optional, but to be "greedy" and capture it if it's there.

Next, inside the first group (first group of parentheses), we can have two different situations.

The first is any lowercase letter between a and f or a number six times. The vertical bar tells us that we can also have three lowercase letters between a and f or numbers instead.

Finally, we want the end of the string ($).

The reason that I put the six character before is that parser will capture a hex value like #ffffff.

If I had reversed it so that the three characters came first, the parser would only pick up #fff and not the other three f's.

#### String that matches:

`#a3c113`

#### String that doesn't match:

`#4d82h4` (contains the letter h)

## Matching a Slug

```javascript
Matching a Slug: /^[a-z0-9-]+$/
```

You will be using this regex if you ever have to work with mod_rewrite and pretty URL's.

We begin by telling the parser to find the beginning of the string (^), followed by one or more (the plus sign) letters, numbers, or hyphens.

Finally, we want the end of the string ($).

#### String that matches:

`my-title-here`

#### String that doesn't match:

`my_title_here` (contains underscores)

## Matching an Email

```javascript
Matching an Email: /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

We begin by telling the parser to find the beginning of the string (^).

Inside the first group, we match one or more lowercase letters, numbers, underscores, dots, or hyphens.

I have escaped the dot because a non-escaped dot means any character.

Directly after that, there must be an at sign.

Next is the domain name which must be: one or more lowercase letters, numbers, underscores, dots, or hyphens.

Then another (escaped) dot, with the extension being two to six letters or dots. I have 2 to 6 because of the country specific TLD's (.ny.us or .co.uk).

Finally, we want the end of the string ($).

#### String that matches:

`john@doe.com`

#### String that doesn't match:

`john@doe.something` (TLD is too long)

## Matching a URL

```javascript
Matching a URL: /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

This regex is almost like taking the ending part of the above regex, slapping it between `"http://"` and some file structure at the end.

It sounds a lot simpler than it really is. To start off, we search for the beginning of the line with the caret.

The first capturing group is all option. It allows the URL to begin with `"http://"`, `"https://"`, or neither of them.

I have a question mark after the s to allow URL's that have `http` or `https`. In order to make this entire group optional, I just added a question mark to the end of it.

Next is the domain name: one or more numbers, letters, dots, or hypens followed by another dot then two to six letters or dots.

The following section is the optional files and directories.

Inside the group, we want to match any number of forward slashes, letters, numbers, underscores, spaces, dots, or hyphens. Then we say that this group can be matched as many times as we want.

Pretty much this allows multiple directories to be matched along with a file at the end. I have used the star instead of the question mark because the star says zero or more, not zero or one.

If a question mark was to be used there, only one file/directory would be able to be matched.

Then a trailing slash is matched, but it can be optional.

Finally we end with the end of the line.

#### String that matches:

`https://net.tutsplus.com/about`

#### String that doesn't match:

`http://google.com/some/file!.html` (contains an exclamation point)

## Matching an IP Address

```javascript
Matching an IP Address: /^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/
```

Now, I'm not going to lie, I didn't write this regex; I got it from [here](https://www.regular-expressions.info/regexbuddy/ipaccurate.html).

Now, that doesn't mean that I can't rip it apart character for character.

The first capture group really isn't a captured group because was placed inside which tells the parser to not capture this group (more on this in the last regex).

We also want this non-captured group to be repeated three times — the `{3}` at the end of the group.

This group contains another group, a subgroup, and a literal dot. The parser looks for a match in the subgroup then a dot to move on.

The subgroup is also another non-capture group. It's just a bunch of character sets (things inside brackets): the string `"25"` followed by a number between `0` and `5`; or the string `"2"` and a number between `0` and `4` and any number; or an optional zero or one followed by two numbers, with the second being optional.

After we match three of those, it's onto the next non-capturing group. This one wants: the string `"25"` followed by a number between `0` and `5`; or the string `"2"` with a number between `0` and `4` and another number at the end; or an optional zero or one followed by two numbers, with the second being optional.

We end this confusing regex with the end of the string.

#### String that matches:

`73.60.124.136` (no, that is not my IP address :P)

#### String that doesn't match:

`256.60.124.136` (the first group must be "25" and a number between zero and five)

## Matching an HTML Tag

```javascript
Matching an HTML Tag: /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
```

One of the more useful regexes on the list.

It matches any HTML tag with the content inside. As usually, we begin with the start of the line.

First comes the tag's name. It must be one or more letters long. This is the first capture group, it comes in handy when we have to grab the closing tag.

The next thing are the tag's attributes. This is any character but a greater than sign (>).

Since this is optional, but I want to match more than one character, the star is used. The plus sign makes up the attribute and value, and the star says as many attributes as you want.

Next comes the third non-capture group.

Inside, it will contain either a greater than sign, some content, and a closing tag; or some spaces, a forward slash, and a greater than sign.

The first option looks for a greater than sign followed by any number of characters, and the closing tag.

`\1` is used which represents the content that was captured in the first capturing group. In this case it was the tag's name.

Now, if that couldn't be matched we want to look for a self closing tag (like an img, br, or hr tag). This needs to have one or more spaces followed by `"/>"`.

The regex is ended with the end of the line.

#### String that matches:

`Nettuts">http://net.tutsplus.com/">Nettuts+`

#### String that doesn't match:

`<img src="img.jpg" alt="My image>" />` (attributes can't contain greater than signs)

[Credit to →](https://code.tutsplus.com/tutorials/8-regular-expressions-you-should-know--net-6149)

## regexp(ru)

`\` - Следующий символ является специальным. Экранирование.

`^` - Начало искомой строки. Если установлен флаг многострочности,
также производит сопоставление непосредственно после переноса строки.

`$` - Конец искомой строки. Если установлен битовый флаг многострочности,
также сопоставляется содержимому до переноса строки.

`.` - Любой символ кроме переноса строки.

### Квантификаторы:

`-` - 0 или более раз. Эквивалентно {0,}.

`*` - 1 или более раз. Эквивалентно {1,}.
`?` - 0 или 1 раз. Эквивалентно {0,1}. Если использован сразу
после квалификаторов \*, +, ?, или {}, делает квалификатор
"нежадным" (соответствующим минимальному количеству символов).

`{n}` - кол-во n вхождений предыдущего символа.

`{n,m}` - минимум n и максимум m вхождений предыдущего символа.

### Группировка:

`(x)` - Соответствует 'x' и запоминает это соответствие (захватывающие скобки).

`(?:x)` - Соответствует 'x' но не запоминает соответствие (не-захватывающие скобки).

`x(?=y)` - 'x' только если за 'x' следует 'y' (упреждение).

`x(?!y)` - 'x' только если за 'x' НЕ следует 'y' (отрицательное упреждение).

`/\d+(?!\.)/.exec("3.141")` сопоставит '141' но не '3.141'.

`x|y` - либо 'x' либо 'y'.

`[xyz]` - Любой сивол из перечисленных.

`[^xyz]` - всё, что неперечисленно.

`[\b]` - Бэкспейс (U+0008). (Не путать с `\b`.)

`\b` - Граница слова.

`\B` - Несловообразующая граница.

`\cX` - Управляющий символ в строке. `/\cM/` соответствует control-M (U+000D) в строке.

`\d` - Цифровой символ. Эквивалентно выражению [0-9].

`\D` - Нецифровой символ. Эквивалентно выражению [^0-9].

`\f` - Символ прогона страницы (U+000C).

`\n` - Символ перевода строки (U+000A).

`\r` - Символ возврата каретки (U+000D).

`\s` - Символ пустого пространства, включая пробел, табуляция,
прогон страницы, перевод строки.

`\S` - Одиночный символ непустого пространства.

`\t` - Символ горизонтальной табуляции.

`\v` - Символ вертикальной табуляции (U+000B).

`\w` - Любой цифробуквенный символ включая нижнее подчёркивание.
Эквивалентен `[A-Za-z0-9_]`.

`\W` - Любой не цифробуквенный символ. Равносилен `[^a-za-z0-9_]`.

`\0` - Символ NULL (U+0000). Не следует ставить за ним другой цифровой символ,
поскольку \0<digits> является восьмеричной экранирующей последовательностью.

`\xhh` - Символы кода hh (две шестнадцатеричные цифры).

`\uhhhh` - Сиволы кода hhhh (четыре шестнадцатеричные цифры).

### Флаги:

`i` - поиск не зависит от регистра

`g` - ищет все совпадения, без него – только первое

`m` - многострочный режим

`s` - включает режим «dotall» (точка может соответствовать символу перевода строки \n)

`u` - полная поддержка юникода (разрешает корректную обработку суррогатных пар)

`y` - режим поиска на конкретной позиции в тексте

## REGEXP Y

```javascript
const regexp = new RegExp(
  /"([А-Я][а-я]+)"|("[а-я]*[А-Я]([а-я])?)"|^(')([А-Яа-я]{1,}.,\s.+)?/gm
); // >> res  Array(4) [ "\"Мама\"", "\"авТо\"", "\"гриБ\"", "'Яблоко', 'яБлоко', 'ябЛоко', 'яблОко', 'яблоКо', 'яблокО'" ]
const str = `"Мама"
"авТо"
"гриБ"
'Яблоко', 'яБлоко', 'ябЛоко', 'яблОко', 'яблоКо', 'яблокО'
"агент007"
"стриж"
"ГТО"
"Три богатыря"`;

const res = str.match(regexp);
console.log("res :>> ", res);

// url https://regex101.com/r/Caa1in/1
// del https://regex101.com/delete/aobzN4rcK3qhiBHh2iZwNTg4
```
