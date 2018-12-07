# mixed & unknown

**TL;DR**: don't use `any` type in your code.

```typescript
declare var externalData: any;
const first = externalData[0]; // potential runtime crash
```

With `any` both type checkers will bail out.

```typescript
declare var externalData: unknown;
const first = externalData[0]; // Expected error

if (Array.isArray(externalData)) {
  const first = externalData[0];

  if (typeof first === "string") {
    console.log(first.to_upper_case()); // Expected error
    console.log(first.toUpperCase());
  }
}
```

Flow's equiavalent of `unknown` is called `mixed`.
