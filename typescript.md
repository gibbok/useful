# TypeScript

## Generate an union of number 

Generate an union of number from START to END not included. Up to < 1000 members of the union as for TypeScript recursion limitation.

```typescript
type Enumerate<N extends number, Acc extends Array<number> = []> = Acc['length'] extends N
    ? Acc[number]
    : Enumerate<N, [...Acc, Acc['length']]>;

type NumericRange<START extends number, END extends number> = Exclude<
    Enumerate<END>,
    Enumerate<START>
>;

type CustomRange = NumericRange<1, 4> // 1 | 2 | 3
```

[Example](https://www.typescriptlang.org/play?ssl=10&ssc=51&pln=1&pc=1#code/C4TwDgpgBAogdgVwLYQE4ENgQDwDkoQAeWcAJgM5SJIBGaANFAIIDGLBxEZlTqGI2anVQA+KAF4oAbQC6YyaxZSA5ABsuAc2AALZTI4kKUXACgo5qAH5mbKULQyzFgFyxqaTDlyMpAOn+KjIoq6nBaujJyANwmJqCQxshoAJYsAEroYTgAygAqTGm5BlxG9qiMMLgAIsXcVMjC8rCELKoIpDhO5vBJGFjYlVUi9F1uvZ7YeQW5IiYiMXHg0ADCCOTAAPZIGVkSiSioqTsaOACMjAAsYgD011CnUAA+UABMT1AAzCZAA)


## DeepPartial

Generate a type which has all properties optional at any level of nesting.

```typescript
type DeepPartial<T> = T extends object
    ? {
          [P in keyof T]?: DeepPartial<T[P]>;
      }
    : T;

type Type = { a: number, b: { a:number, b: {a:number}}}

type TypeDeepPartial = DeepPartial<Type>
```

[Example](https://www.typescriptlang.org/play?ssl=9&ssc=41&pln=1&pc=1#code/C4TwDgpgBAIhFgAoEMBOwCWyA2AeAKgHxQC8U+UEAHsBAHYAmAzlAPYBGAVhAMbABQUIVAD8UAN6Dh0oQG1EUDHSgBrCCFYAzcgF0RALljwkaTDgLydhANxTpAXztRD+W-1CRy4aGXFRkhnQArgC27BCoADRQ7IZ+AcFhEdGxEgmh4aj22fzu3l6QcAgo6FjYpEbFpmUE3oT8QA)


## Unpack type from array type

Given an array type, returns an union with all type in the array.

```typescript
export type Unpacked<T> = T extends Array<infer U> ? U : T;

type Arr = [{a:number}, number, string]

type Item = Unpacked<Arr>
```

[Example](https://www.typescriptlang.org/play?ssl=5&ssc=26&pln=1&pc=1#code/KYDwDg9gTgLgBDAnmYcCqA7MBDAxga2ABMAeAFQD44BeOMuUGYDIgZzgEEoptESBLDADNgUdFQD86OAC46AbgBQipCk7cacANoBvbDIwBXALYAjUQF8ANHCNnRN1jCiCA5gF1lq1AEkmxzUwcAmISLigKIA)

## JSON object

Matches a JSON object.

```typescript
type JsonObject = { [Key in string]: JsonValue } & { [Key in string]?: JsonValue | undefined };
type JsonArray = JsonValue[];
type JsonPrimitive = string | number | boolean | null;
type JsonValue = JsonPrimitive | JsonObject | JsonArray;
```

## Dealing with keyof objects:

```typescript
type Person = {
    name: string,
    age: number,
    admin: 0 | 1,
}

const getValuByKey = (data: Person, key: keyof Person) => data[key]

// not optimal way
const r1 = getValuByKey({
    name: 'simone',
    age: 123,
    admin: 0
}, 'admin') // string | number, typescript was not able to narrow the type it takes the common denominator: string | number | (0 | 1)

const getValueByKeyWithGeneric = <T, K extends keyof T>(data: T, key: K) => data[key]

// better way, use generic to infer properly the type, as with a generic we define the type passed in is a subtype (so we know all props)
const r2 = getValueByKeyWithGeneric({
    name: 'simone',
    age: 123,
    admin: 0
}, 'admin') //number correct result

// Explanation for this behaviour in TS: https://github.com/microsoft/TypeScript/pull/12253#issuecomment-263132208
```

## Conditional types with infer and template literals

```typescript
type GetUserId<T> = T extends `site.com/userId:${infer U}` ? U extends 'simone' ? { userId: U } : { userId: 'notSimone' } : never

type SimoneRoute = 'site.com/userId:simone'
type SimoneUserId = GetUserId<SimoneRoute>

type JoyRoute = 'site.com/userId:joy'
type JoyUserId = GetUserId<JoyRoute>
```
