# Literal type inference

```typescript
const foo = "FOO";
const bar: typeof foo = "BAR";
/*
TS 3.1 OK: Type '"BAR"' is not assignable to type '"FOO"'.

Flow 0.86:
No errors!
*/
```

TypeScript infers the type of `foo` to be literal string type `"FOO"`, but Flow infers `foo` as string. This causes missing errors in common JavaScript patterns like [Redux](https://redux.js.org/basics/actions).

- [Flow issue](https://github.com/facebook/flow/issues/2639) (since October 2016)
