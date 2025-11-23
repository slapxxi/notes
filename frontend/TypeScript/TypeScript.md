- Convert tuple to union with `[number]`
- Get length of a tuple with `['length']`

#### Building Blocks for Types Programming

- Generics
  - Conditional Types
- Mapped Types
- Indexing (including special `number` indexing)
- Recursion
- Destructuring
- Merging `[...value]`
- `typeof`, `keyof`

#### Conditional Types

```ts
type A<T> = T extends string ? true : false;
```

#### Mapped Types

```ts
type OptionsFlags<Type> = {
  [Property in keyof Type]: boolean;
};

type CreateMutable<Type> = {
  -readonly [Property in keyof Type]: Type[Property];
};

type Getters<Type> = {
  [Property in keyof Type as `get${Capitalize<string & Property>}`]: () => Type[Property];
};

type ExtractPII<Type> = {
  [Property in keyof Type]: Type[Property] extends { pii: true } ? true : false;
};
```

You can filter out keys by producing `never` via a conditional type:

```ts
type RemoveKindField<Type> = {
  [Property in keyof Type as Exclude<Property, 'kind'>]: Type[Property];
};
```

#### Indexing

```ts
const MyArray = [
  { name: 'Alice', age: 15 },
  { name: 'Bob', age: 23 },
  { name: 'Eve', age: 38 },
];
type Person = (typeof MyArray)[number];
```

#### Tuples

```ts
type Length<T extends readonly any[]> = T['length'];
```

```ts
[number, string]
[number, ...Tuple]
[number, ...boolean[], string]
```

#### Distributive

When you are writing the construct `T extends U` where `T` is the union, actually what is happening is TypeScript iterates over the union `T` and applies the condition to each element.

```ts
type MyExclude<T, U> = T extends U ? never : T;
type T1 = MyExclude<'a' | 'b' | 'c', 'a' | 'b'>;
```

#### Variadic Tuple Types

```ts
type Concat<T, U> = [...T, ...U];
```

```ts
type Concat<T extends unknown[], U extends unknown[]> = [...T, ...U];
```

#### Infer

Recursive inference:

```ts
type Awaited<T> = T extends Promise<infer R> ? Awaited<R> : T;
```

