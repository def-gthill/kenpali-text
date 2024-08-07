```
# Trimming whitespace
trim = import("text").trim;
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
toLowerCase = import("text").toLowerCase;
[
    "FOO" | toLowerCase,
    "foo" | toLowerCase,
    "fOo42" | toLowerCase,
]
>> ["foo", "foo", "foo42"]
```

```
# Converting to uppercase
toUpperCase = import("text").toUpperCase;
[
    "FOO" | toUpperCase,
    "foo" | toUpperCase,
    "fOo42" | toUpperCase,
]
>> ["FOO", "FOO", "FOO42"]
```
