# eON

---
extended Object Notation Language.

By GiftShower_ (Chung Ho Jung)

## Objectives

---
eON aims to be an extended version of JSON with its additional syntaxes.
It is designed to overcome the limitations of JSON while being compatible.

## Table of contents

---
- Spec
- Referencing
- Reservoir
## Spec

---
- eON is case-sensitive.
- eON file must be a valid UTF-8 encoded Unicode document.
- Basic syntax is same as [JSON](https://www.json.org/)
- Every eON document should use .eon file extension.

## Referencing

---

### Basic

---
Referencing is the key function of eON document.

The basic form of referencing looks like this.
```text
"hello" : "world"

Reference key from value: |"world"|
Reference value from key: ||"hello"||
```
### Unreferenceable

---
You can define a key, or value as unreferenceable.
```text
!>>"hello" : "world"
Reference key from value: |"world"| (Valid)
Reference value from key: ||"hello"|| 
(Invalid, because the key "hello" is defined as unreferenceable.
```

### Referencing priority

---
If referencing is used multiple times in same object, they'll act as an array.
```text
"hello" : "world"

|"world"| : "there"
|"world"| : "mike"
```
Then accessing "hello" will return this:
```text
"hello": [ world, there, mike ]
```
or accessing referenced value only will return this:
```text
"hello": [there, mike]
```

To prevent this, you can set priority for referencing.

```text
"hello" : "world"
r1|"world"| : "there"
r2|"world"| : "mike"
```
Then, you can access references individually with their reference priority.

## Reservoir

---
Reservoir is a container that can be used to define variables.
Key/Value pair in Reservoir can't use referencing.

```text
< "hello": "world" >
{
    ||"hello"||: "is awesome"
}
```

Same thing in JSON:
```json
{
  "world": "is awesome"
}
```

**WARNING**: Reservoirs should be defined before root object.

---
