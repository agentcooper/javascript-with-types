# Exact & non-exact objects

[Flow has open object by default and \$Exact helper for exact objects.​](https://flow.org/en/docs/types/objects/#exact-object-types-)

[TypeScript does not have exact type, but checks for excessive properties by default.​](https://github.com/Microsoft/TypeScript/issues/12936#issuecomment-284590083)

```typescript
interface User {
  name: string;
}
const user: User = { name: "A", extraProperty: "foo" };

/*
TS 3.1:
Type '{ name: string; extraProperty: string; }' is not assignable to type 'User'.
  Object literal may only specify known properties, and 'extraProperty' does not exist in type 'User'.

Flow 0.86: No errors!
*/
```
