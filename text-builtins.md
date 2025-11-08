# Kenpali Text Specification

## Editing Strings|editing

### trim|trim

Removes all whitespace from the start and end of the string.

Parameters:

- `string` (_String_): The string to trim.

Returns:

- (_String_): The trimmed string.

```
# Trimming whitespace
trim = text/trim;
[
    "" | trim,
    "  " | trim,
    "foo" | trim,
    "   foo    " | trim,
    "   foo\n" | trim,
    "  foo bar baz " | trim,
]
>> ["", "", "foo", "foo", "foo", "foo bar baz"]
```

### toLowerCase|toLowerCase

Converts all letters to lowercase.

Parameters:

- `string` (_String_): The string to convert to lowercase.

Returns:

- (_String_): The lowercase string.


```
# Converting to lowercase
toLowerCase = text/toLowerCase;
[
    "FOO" | toLowerCase,
    "foo" | toLowerCase,
    "fOo42" | toLowerCase,
]
>> ["foo", "foo", "foo42"]
```

### toUpperCase|toUpperCase

Converts all letters to uppercase.

Parameters:

- `string` (_String_): The string to convert to uppercase.

Returns:

- (_String_): The uppercase string.

```
# Converting to uppercase
toUpperCase = text/toUpperCase;
[
    "FOO" | toUpperCase,
    "foo" | toUpperCase,
    "fOo42" | toUpperCase,
]
>> ["FOO", "FOO", "FOO42"]
```

### startsWith|startsWith

Tests whether the string starts with the specified prefix.

Parameters:

- `string` (_String_): The string to check.
- `prefix` (_String_): The prefix to check for.

Returns:

- (_Boolean_): Whether `string` starts with `prefix`.

```
# Starts with
startsWith = text/startsWith;
[
    "foobar" | startsWith(""),
    "foobar" | startsWith("f"),
    "foobar" | startsWith("o"),
    "foobar" | startsWith("foo"),
    "foobar" | startsWith("fb"),
]
>> [
    true,
    true,
    false,
    true,
    false,
]
```

### removePrefix|removePrefix

Removes the specified prefix from the string if possible.

Parameters:

- `string` (_String_): The string to remove the prefix from.
- `prefix` (_String_): The prefix to remove.

Returns:

- (_String_): If `string` starts with `prefix`, `string` with `prefix` removed, otherwise `string` itself.

```
# Remove prefix
removePrefix = text/removePrefix;
[
    "foobar" | removePrefix(""),
    "foobar" | removePrefix("f"),
    "foobar" | removePrefix("o"),
    "foobar" | removePrefix("foo"),
    "foobar" | removePrefix("fb"),
]
>> [
    "foobar",
    "oobar",
    "foobar",
    "bar",
    "foobar",
]
```

### endsWith|endsWith

Tests whether the string ends with the specified suffix.

Parameters:

- `string` (_String_): The string to check.
- `suffix` (_String_): The suffix to check for.

Returns:

- (_Boolean_): Whether `string` starts with `suffix`.

```
# Ends with
endsWith = text/endsWith;
[
    "foobar" | endsWith(""),
    "foobar" | endsWith("r"),
    "foobar" | endsWith("a"),
    "foobar" | endsWith("bar"),
    "foobar" | endsWith("br"),
]
>> [
    true,
    true,
    false,
    true,
    false,
]
```

### removeSuffix|removeSuffix

Removes the specified suffix from the string if possible.

Parameters:

- `string` (_String_): The string to remove the suffix from.
- `suffix` (_String_): The suffix to remove.

Returns:

- (_String_): If `string` starts with `suffix`, `string` with `suffix` removed, otherwise `string` itself.

```
# Remove suffix
removeSuffix = text/removeSuffix;
[
    "foobar" | removeSuffix(""),
    "foobar" | removeSuffix("r"),
    "foobar" | removeSuffix("a"),
    "foobar" | removeSuffix("bar"),
    "foobar" | removeSuffix("br"),
]
>> [
    "foobar",
    "fooba",
    "foobar",
    "foo",
    "foobar",
]
```

## Regular Expressions|regexes

### Regex|Regex

Creates a regex instance to match the specified regex pattern.

Some regex methods return _match objects_. A match object has the following properties:

- `match` (_String_): The portion of the string that matched the regex.
- `index` (_Number_): The index in the string where the match starts.
- `numberedGroups` (_Array of String_): The substrings matched by the numbered groups in the regex.
- `namedGroups` (_Object of String_): The substrings matched by the named groups in the regex.

#### newRegex|newRegex

Creates a new regex instance.

Parameters:

- `pattern` (_String_): The regex pattern.

Returns:

- (_Regex_): The regex instance.

#### Regex/findAll|Regex-findAll

Finds all matches for the regex in the specified string.

Parameters:

- `string` (_String_): The string to search.

Returns:

- (_Array of Object_): An array of all the match objects.

```
# Finding all matches for a regex
r = text/newRegex("f(ai|ooba)r");
[
    r.findAll("x"),
    r.findAll("anafairafoobara"),
]
>> [
    [],
    [
        {match: "fair", index: 4, numberedGroups: ["ai"], namedGroups: {}},
        {match: "foobar", index: 9, numberedGroups: ["ooba"], namedGroups: {}},
    ]
]
```

```
# Unmatched groups returning null
r = text/newRegex("f(ooba)?r");
r.findAll("foobarfr")
>> [
    {match: "foobar", index: 1, numberedGroups: ["ooba"], namedGroups: {}},
    {match: "fr", index: 7, numberedGroups: [null], namedGroups: {}}
]
```

#### Regex/match|Regex-match

Tries to match the regex against an entire string.

Parameters:

- `string` (_String_): The string to match.

Returns:

- (_Object or Null_): A match object if the entire string matches the regex, or `null` if it doesn't.

```
# Matching an entire string to a regex
r = text/newRegex("f(ai|ooba)r");
[
    r.match("x"),
    r.match("fair"),
    r.match("foobar"),
    r.match("anafairafoobara"),
]
>> [
    null,
    {match: "fair", index: 1, numberedGroups: ["ai"], namedGroups: {}},
    {match: "foobar", index: 1, numberedGroups: ["ooba"], namedGroups: {}},
    null,
]
```
