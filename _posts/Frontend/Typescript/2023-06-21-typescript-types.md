---
layout: post
title:  "Built-in types in Typescript"
date:   2023-06-21 15:41:00 +1000
categories: [frontend]
tags: [typescript, built-in types, types]
---

- [Built-in Types in Typescript](#built-in-types-in-typescript)
  - [The "any" type](#the-any-type)
  - [Arrays](#arrays)
  - [Tuples](#tuples)

# Built-in Types in Typescript 

## The "any" type
If you declare but don't initialise to anything, it becomes "any" type

`let someValue;`

This "any" type can be assigned to anything, but it is not recommended to use "any" type because it defeats purpose of Typescript

```typescript
someValue = 1;
console.log(someValue); // => 1
someValue = "Typescript";
console.log(someValue); // => 'Typescript'
```

## Arrays

```typescript 
let numbersArray: number[] = [1, 2, 3]; // Explicit declaration
let numbersArray1 = [1, 2, 3]; // Implicit declaration
```

When declaring empty array, you must explicitly declare the type. Otherwise it becomes "any" type array

```typescript
let emptyArray:number[] = []
```

```typescript
// Example function
let numbersArray3: number[] = [1, 2, 3, 4, 5];
let logValue = () => {
  numbersArray3.forEach((n) => {
    if (n < 4) console.log(n);
    else console.log(n.toExponential(2));
  });
};

logValue();
```

## Tuples

A Fixed type array, used for assigning key/value pairs mostly.
It is a single variable name, but has multiple types in the array, unlike tuples in other languages (c#) where each value in a tuple has its own variable name

```typescript
// Declaration
let user: [number, string] = [33, "Arun"];
```

Typescript is smart enough to understand each value's type, so we can perform appropriate actions on them. For example, the following is valid. 

```typescript
user[0].toFixed(1);
user[1].toLower();
```

The following code will throw error since the first value is defined as `number`, and hence any `string` specific operations are not possible.

```typescript
user[0].toLower(); // throws 'Property 'toLower' does not exist on type 'number'.ts(2339)'
```