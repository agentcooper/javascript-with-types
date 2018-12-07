# Exhaustiveness

Exhaustiveness is an ability of the compiler to see if you have checked all the possible cases.

```typescript
type State = "loading" | "ready" | "error";
function renderHTML(state: State): string {
  switch (state) {
    case "loading":
      return "<img src='loading.gif' />";
    case "ready":
      return "<p>Read!</p>";
    case "error":
      return "<p>Error!</p>";
  }
}
/*
TS 3.1 = OK: no errors

Flow 0.86 = Not OK:
3: function renderHTML(state: State): string {
                                      ^ Cannot expect string as the return type of function
*/
```

When we add another option TypeScript error is not very helpful:

```typescript
type State = "loading" | "ready" | "error" | "warning";
```

```
Function lacks ending return statement and return type does not include 'undefined'.
```

This can be improved by introducing a helper function:

```typescript
type State = "loading" | "ready" | "error" | "warning";

function assertUnreachable(x: never): never {
  throw new Error("Didn't expect to get here");
}

function renderHTML(state: State): string {
  switch (state) {
    case "loading":
      return "<img src='loading.gif' />";
    case "ready":
      return "<p>Read!</p>";
    case "error":
      return "<p>Error!</p>";
  }
  /* Expected error: Argument of type '"warning"' is not assignable to parameter of type 'never'. */
  return assertUnreachable(state);
}
```

Flow's equivalent of `never` is called `empty`:

```javascript
type State = "loading" | "ready" | "error" | "warning";

function assertUnreachable(x: empty): empty {
    throw new Error("Didn't expect to get here");
}

function renderHTML(state: State): string {
    switch (state) {
        case "loading":
            return "<img src='loading.gif' />";
        case "ready":
            return "<p>Read!</p>";
        case "error":
            return "<p>Error!</p>";
    }
    return assertUnreachable(state);
}
```

```
16:     return assertUnreachable(state);
                                 ^ Cannot call `assertUnreachable` with `state` bound to `x` because string literal `warning` [1] is incompatible with empty [2].
References:
7: function renderHTML(state: State): string {
                              ^ [1]
3: function assertUnreachable(x: empty): empty {
                                 ^ [2]
```
