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

