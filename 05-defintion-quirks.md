# Built-in definition quirks

## Object.values

Flow's [`lib/core.js`](https://github.com/facebook/flow/blob/master/lib/core.js):

```flow
declare class Object {
  // ...
  static values(object: any): Array<mixed>;
```

TypeScript's [`lib/lib.es2017.object.d.ts`](https://github.com/Microsoft/TypeScript/blob/master/lib/lib.es2017.object.d.ts):

```
interface ObjectConstructor {
  /**
    * Returns an array of values of the enumerable properties of an object
    * @param o Object that contains the properties and methods. This can be an object that you created or an existing Document Object Model (DOM) object.
    */
  values<T>(o: { [s: string]: T } |  ArrayLike<T>): T[];
```

Example:

```typescript
type Point = {
  x: number,
  y: number
};
type PointMap = { [key: string]: Point };

const foo: PointMap = {
  "1": { x: 5, y: 6 },
  "2": { x: 7, y: 8 }
};

Object.values(foo).map(p => {
  return p.x;
  // Flow 0.86: ^ Cannot get `p.x` because property `x` is missing in mixed [1].
  // TS 3.1: OK.
});
```

- [Flow issue](https://github.com/facebook/flow/issues/2221) (August 2016)
