# Adding constraints and rules

In addition to the basic [cardinality](slots) constraints for slots, additional constraints can be specified

## Unique Key

A class can declare [unique_keys](https://w3id.org/linkml/unique_keys), a set of slots that are unique for members of that class.

[identifier](https://w3id.org/linkml/identifier)s are special cases of unique keys.

## String serialization

A rule for generating the string value of a slot can be specified as a [string_serialization](https://w3id.org/linkml/string_serialization)

```yaml
classes:
  Person:
    attributes:
      first:
      last:
      full:
        string_serialization: "{first} {last}"
```

- Tools for performing missing value inference can then populate the `full` slot based on the other two slots
- Tools for performing validation can use this to check slot values
    - if all 3 slots are populated, missing value inference can be used to check for consistency
    - if only `full` is provided, then the string can be checked (e.g. by a regex) to ensure the syntax is consistent

## Patterns

The value of a slot can be constrained to conform to a particular string pattern using the [pattern](https://w3id.org/linkml/pattern) metaslot

Example:

```yaml
  slots:
     phone:
       pattern: "^[\\d\\(\\)\\-]+$"   ## regular expression

```

## Structured patterns

The [structured_pattern](https://w3id.org/linkml/structured_pattern) construct
allows you to provide patterns in a more structured way, and to *reuse* sub-patterns.

First you declare the patterns to be reused in the top level of your schema:

```yaml
settings:
  float: "\\d+[\\.\\d+]"
  unit: "\\S+"
  email: "\\S+@\\S+{\\.\\w}+"
```

You can then use this inside a structured pattern:

```yaml
  height:
    range: string
    structured_pattern:
      syntax: "{float} {unit.length}"
      interpolated: true
      partial_match: false
```

## Minimum and Maximum values

Any numeric value can have minimum and maximum values specified

 * [minimum_value](https://w3id.org/linkml/minimum_value)
 * [maximum_value](https://w3id.org/linkml/maximum_value)




