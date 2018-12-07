# Type refinements

Those are basic JavaScript expressions which will execute as you expect by the runtime, but they also work on the type level: they act as hints to the type checker to refine the variable type.

```typescript
type Foo = string | number;

declare var foo: Foo;

if (typeof foo === "string") {
  console.log(foo.toUpperCase());
} else {
  console.log(Math.abs(foo));
}
```

Extracting the type refinement into a function will break the refinement for both TypeScript and Flow:

```typescript
type Foo = string | number;

declare var foo: Foo;

function isString(foo: Foo) {
  return typeof foo === "string";
}

if (isString(foo)) {
  console.log(foo.toUpperCase()); // TS 3.1: Property 'toUpperCase' does not exist on type 'number'.
} else {
  console.log(Math.abs(foo)); // TS 3.1: Type 'string' is not assignable to type 'number'.
}
```

Both type checkers need a special return type indicating a refinement:

```typescript
// TypeScript
function isString(foo: Foo): foo is string {
    return typeof foo === "string";
}
```

```javascript
// Flow
function isString(foo: Foo): %checks {
    return typeof foo === "string";
}
```

- [%checks](https://github.com/facebook/flow/issues/4723)
- [TypeScript's `is`](https://www.typescriptlang.org/docs/handbook/advanced-types.html#typeof-type-guards)
