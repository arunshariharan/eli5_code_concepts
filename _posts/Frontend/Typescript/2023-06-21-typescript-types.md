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
  - [Enum](#enum)
  - [Functions](#functions)
    - [A void function](#a-void-function)
    - [A function that returns a number](#a-function-that-returns-a-number)
    - [A function that takes optional parameter.](#a-function-that-takes-optional-parameter)

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

## Enum

Enums are a set of named constants. enum Variable name should be in PascalCase, and so are its keys.

```typescript
// Declaration
enum ShirtSize {
  Small,
  Medium,
  Large,
}
```

- By default, the first key in an enum gets assigned 0 as the value. But it can be changed
- In the declaration below, we assign  Small as 1, and the compiler will automatically assign 2 and 3 for Medium / Large
```typescript
enum ShirtSize1 {
  Small = 1,
  Medium,
  Large,
}
```

- If we need to assign any other value other than number, we need to explicitly declare for each key in enum

```typescript
enum ShirtSizeWithStringValues {
  Small = "s",
  Medium = "m",
  Large = "l",
}

// Usage
console.log(ShirtSize.Small); // => 0
console.log(ShirtSize1.Medium); // => 2
console.log(ShirtSizeWithStringValues.Large); // => 'l'
```

## Functions

Function is a block of code that does performs a.. function. They form the building block of any programming language

### A void function

```typescript
function calculateTaxReturn(income: number) {
  if (income < 10_000) console.log(income * 2.3);
  else console.log(income * 1.5);
}
```

### A function that returns a number

- It is highly recommended to specify the return type in function declaration

```typescript
function calculateTaxReturn1(income: number): number {
  if (income < 10_000) return income * 2.3;
  else return income * 1.5;
}
```

### A function that takes optional parameter. 

- The second param is optional in the following example 

```typescript
function calculateTaxReturnWithOptionalParam(
  income: number,
  taxOffset = 10_000
): number {
  if (taxOffset < 10_000) return income * 2.3;
  else return income * 1.5;
}

let taxReturn = calculateTaxReturnWithOptionalParam(2000); // 2000 for income & default 10_000 for taxOffset
let taxReturn1 = calculateTaxReturnWithOptionalParam(200_000, 3000); // 200_000 for income & 3000 as taxOffset
```