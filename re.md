#### notes
(the "r" in the beginning is making sure that the string is being treated as a "raw string", no escaping, treat `\` as literal character not escape character"

#### metacharacters (characters with special meaning)

- `[]` a set of characters
- `\` escape special characters
- `.` any character except newline (\n)
- `*` zero or more occurrences
- `+` one or more occurrences
- `?` zero or one occurances, also `*?` stops greedy match (only first is matched)
- `{}` exactly the specified number or range of occurances, eg `{1}`, `{1,}`, `{1,3}`
- `|` either or
- `()` capture and group

#### quantifiers


#### special sequences
- `\A` if the specified characters are at the beginning of the string
- `\d` if string contains digits (numbers from 0-9), opposite `\D`
- `\s` if string contains a white space character, opposite `\S`
- `\w` if string contains any word characters (a to Z, 0-9, and _ ), opposite `\W`
- `\Z` if specified characters are at the end of the string

#### assertions (beginning & end of lines and word)
- `^` the beginning of input, or line (if multiline flag is true, `/^\d/m`)
- `$` the end of input, or line (if multiline flag is true)
- `\b` if specified characters are at the beginning or at the end of a word, opposite `\B`
- `x(?=y)` matches "x" only if "x" is followed by "y" (lookahead assertion)
- `x(?!y)` negative lookahead assertion
- `(?<=y)x` matches "x" only if "x" is preceded by "y" (lookbehind assertion)
- `(?<!y)x` negative lookbehind assertion

#### sets
- `[arn]` if one of the specified characters (a, r, or n) are present
- `[a-n]` if lower case character, alphabetically between a and n, opposite `[^arn]`
- `[0-5][0-9]` if two-digit numbers from 00 and 59
- `[a-zA-Z]` if one letter either, upper or lower case
- `[+]` in sets, +, *, ., |, (), $,{} has no special meaning, so [+] means: return a match for any + character in the string


#### pattern modifiers
- `g` global match
- `i` case-insensitive
- `m` multiple lines
- `s` treat string as single line
- `x` allow comments and white space in pattern


### using regular expressions with python

#### `re.findall(<expression>, <string>)` returns a list containing all matches.
```py
txt = "The rain in Spain"
x = re.findall("ai", txt)
print(x)
```
prints a list the contains the matches in the order they are found.
If no matches are found, an empty list is returned.

#### `re.split(<expression>, <string>, [max-split])` returns a list where the string has been split at each match
```py
txt = "The rain in Spain"
x = re.split("\s", txt, 1)
print(x)
```	
splits at each white-space character

#### `re.sub(<expression1>, <expression2>, <string>, [count])` replaces the matches with the text of your choice, returns a string. You can control the number of replacements by specifying the count parameter:
```py
txt = "The rain in Spain"
x = re.sub(r"\bS(\w+)", r"T\1", txt) # "The rain in Tpain"
print(x)
```
- if you don't want to replace the entire text, use separate paranthesis to extract that info
  - `re.sub(r"([0-9]+)([a-z])", r"\1\\textsuperscript{\2}", "World Crude Oil Production, 1960-2021a")`
#### `re.search(<expression>, <string>)` searches the string for a match, and returns a Match object if there is a match.
```py
txt = "The rain in Spain"
x = re.search("\s", txt)   
print("The first white-space character is located in position:", x.start())
```

#### match object is an object containing information about the search and the result. If there is no match, the value None will be returned, instead of the Match Object.

- `.span()` returns a tuple containing the start, and end positions of the match.
- `.string` returns the original `<string>` passed into the function.
- `.group()` returns the list of all matches