# Kenpali Text Specification

## Editing Strings

```
# Trimming whitespace
trim = text.trim;
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

```
# Converting to lowercase
toLowerCase = text.toLowerCase;
[
    "FOO" | toLowerCase,
    "foo" | toLowerCase,
    "fOo42" | toLowerCase,
]
>> ["foo", "foo", "foo42"]
```

```
# Converting to uppercase
toUpperCase = text.toUpperCase;
[
    "FOO" | toUpperCase,
    "foo" | toUpperCase,
    "fOo42" | toUpperCase,
]
>> ["FOO", "FOO", "FOO42"]
```

```
# Starts with
startsWith = text.startsWith;
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

```
# Remove prefix
removePrefix = text.removePrefix;
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

```
# Ends with
endsWith = text.endsWith;
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

```
# Remove suffix
removeSuffix = text.removeSuffix;
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

## Regexes

```
# Finding all matches for a regex
r = text.regex("f(ai|ooba)r");
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
r = text.regex("f(ooba)?r");
r.findAll("foobarfr")
>> [
    {match: "foobar", index: 1, numberedGroups: ["ooba"], namedGroups: {}},
    {match: "fr", index: 7, numberedGroups: [null], namedGroups: {}}
]
```

```
# Matching an entire string to a regex
r = text.regex("f(ai|ooba)r");
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
