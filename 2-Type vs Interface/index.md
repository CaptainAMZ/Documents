scaler

Certainly! Here's the article formatted in Markdown:

# TypeScript Type vs Interface

## Experience

Academy
Data Science
Neovarsity
Topics
Explore
Courses
Events
Search for Articles
Topics

## Experience Scaler

TypeScript Tutorial
TypeScript Type vs Interface
TypeScript Type vs Interface
TypeScript Type vs Interface
Learn via video courses

## Overview

We know that while using TypeScript, some developers use types while others use interfaces. Let's learn about what types and interfaces are. Interfaces are a way to define data shapes. They are the syntax that classes have to follow. On the other hand, types are defined as the data types of variables, which can be built-in types, user-defined types, or any other pre-defined data types used as inputs in a program.

## Introduction

In TypeScript, types are used for declaring variable data types, while interfaces are used to define entities. Now let's read about where we can use types and interfaces in TypeScript.

## Flexibility

Types or type aliases in TypeScript are used to create a variable name with a declared data type before the name. They can create names for built-in types like numbers, strings, booleans, null, undefined, etc. Types can also declare user-defined types like union, intersection, and tuple types.

Interfaces have more capabilities than types, so it is said that types are more flexible than interfaces. Now let's learn the syntax of both TypeScript types and interfaces.

### Syntax for types in TypeScript:

```typescript
type TypeName = Type;
```

### Syntax for interfaces in TypeScript:

```typescript
interface InterfaceName {
  property: Type;
}
```

The syntax for both types and interfaces is mostly similar.

## Merging the Declarations

Merging the declarations is only possible with interfaces and not with types. It happens when the TypeScript compiler merges two or more interfaces that share the same name into a single declaration.

Let's see an example below:

```typescript
interface Person {
  name: string;
}

interface Person {
  age: number;
}

const person: Person = {
  name: "John",
  age: 25,
};
```

Here, we have created two interfaces with the same name but with different properties. TypeScript will automatically merge both of them. Merging the declarations is very useful and it only works with interfaces, not with types. If we create two types with the same names but with different properties, TypeScript will throw an error.

## Classes

In TypeScript, classes do not support the feature of implementing or extending union types. Hence, types are not used in classes. However, interfaces in TypeScript can extend classes. This concept helps in a more object-oriented way of programming.

Let's see an example of how to implement it in our program:

```typescript
class Colors {
  color: string;
}

interface NewColors extends Colors {
  shade: string;
}

const newColor: NewColors = {
  color: "blue",
  shade: "light",
};
```

## Primitives
Primitives can only be used by types and not interfaces.

Let's see an example below:

```typescript
type MyType = number | string;
```

## Unions

Union types are used to create new types that can have a value of one or more types. To create a union type, we use the `|` keyword.

Let's see an example below:

```typescript
type MyUnion = string | number;

const value: MyUnion = "hello";
```

Here, the `MyUnion` type can have a value of either a string or a number.

## Tuple Types

Tuples are very useful because they can have two sets of values of different data types. We can only declare tuples using types and not interfaces.

Let's see an example below:

```typescript
type MyTuple = [string, number];

const tuple: MyTuple = ["hello", 42];
```

Though we cannot declare a tuple in TypeScript using an interface, we can still use a tuple inside an interface, like in the example shown below:

```typescript
interface MyInterface {
  tuple: [string, number];
}

const obj: MyInterface = {
  tuple: ["hello", 42],
};
```

## Intersection

An intersection type is a type that allows us to merge several types into one. This allows us to combine many types to create a single type with all the properties that we require. The `&` operator is used to combine multiple types using the intersection type, but it does not combine multiple types into one interface.

Let's see an example below:

```typescript
type FirstType = {
  prop1: string;
};

type SecondType = {
  prop2: number;
};

type CombinedType = FirstType & SecondType;

const obj: CombinedType = {
  prop1: "hello",
  prop2: 42,
};
```

## Inheritance

Inheritance is the ability to inherit attributes and methods from a parent. Inheritance is only possible with interfaces; itis not possible with types.

Let's see an example below:

```typescript
interface Animal {
  name: string;
  sound: string;
}

interface Dog extends Animal {
  breed: string;
}

const dog: Dog = {
  name: "Buddy",
  sound: "Woof",
  breed: "Labrador",
};
```

## Few Aspects

Types in TypeScript are used to describe functions, constructors, and tuples. Types cannot be implemented or extended in classes. Interfaces can also be used to describe functions, constructors, and tuples. They can be implemented and extended in classes. Interfaces can also be recursive when compared to types in TypeScript.

## TypeScript Types vs Interfaces

Let's read the difference between TypeScript types and interfaces:

| Type                                         | Interface                                              |
| -------------------------------------------- | ------------------------------------------------------ |
| Defined for a variable's data type           | Syntax for defining entities                           |
| Uses the `type` keyword                      | Uses the `interface` keyword                           |
| Can be used for built-in types, tuples, etc. | Cannot be used with other types of declaration         |
| Cannot be extended                           | Can be extended and supports classes                   |
| Union types can contain one or more types    | Cannot create a union interface by combining two types |
