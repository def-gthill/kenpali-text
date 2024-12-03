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

## Regexes

```
# Finding all matches for a regex
r = text.regex("f(ai|ooba)r");
[
    r @ findAll:("x"),
    r @ findAll:("anafairafoobara"),
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
r @ findAll:("foobarfr")
>> [
    {match: "foobar", index: 1, numberedGroups: ["ooba"], namedGroups: {}},
    {match: "fr", index: 7, numberedGroups: [null], namedGroups: {}}
]
```
