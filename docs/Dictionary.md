In Quarkdown, a dictionary is a collection of key-value pairs, without duplicate keys. A key is always a string value, while a value can be of any type.

The syntax for dictionaries recalls the YAML one, as it uses Markdown lists:

```yaml
- key1: value1
- key2: value2
- key3: value3
```

Since its syntax clashes with [Iterable](iterable)'s, wrapping the dictionary declaration in a **`.dictionary`** function ensures no ambiguity is present, in cases where both dictionaries and iterables are accepted.  
In the following example, [`.foreach`](loops) is suitable for both, so we enforce to run it on a dictionary to iterate over key-value pairs:

```yaml
.var {mydictionary}
  .dictionary
    - key1: value1
    - key2: value2
    - key3: value3

.foreach {.mydictionary}
  ...
```

&nbsp;

Dictionaries can be nested if accepted by the called function ([`.localization`](localization#localization-table) for instance).

```yaml
- English:
  - greeting: Hello
  - food: Fish and chips
- Italian:
  - greeting: Ciao
  - food: Pasta
```

Trailing colons that precede nested dictionaries are not mandatory and can be omitted:

```yaml
- English
  - greeting: Hello
  - food: Fish and chips
- Italian
  - greeting: Ciao
  - food: Pasta
```

# Operations

A dictionary can be passed to any function that accepts an [iterable](iterable#operations) (it is treated as an iterable of pairs).

For a complete list of dictionary operations, please refer to the stdlib's [`Dictionary` documentation](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Dictionary).
