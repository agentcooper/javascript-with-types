# Predicates

```
const arr = [1.1, 2.2, null, 3.3, 4.4];
​
arr.map(n => n.toFixed(2));
arr.filter(Boolean).map(n => n.toFixed(2));
​
/*
TS 3.1:
  ❌errors on both line 3 and 4

Flow 0.86:
  ✅error only on line 4 as expected
*/
```

How does this work in Flow? In Flow's [`lib/core.js`](https://github.com/facebook/flow/blob/master/lib/core.js):

```
filter(callbackfn: typeof Boolean): Array<$NonMaybeType<T>>;
```

What if we try a custom predicate function?

```
const arr = [1.1, 2.2, null, 3.3, 4.4];
​
arr.filter(n => Boolean(n)).map(n => n.toFixed(2));
// 😢 Flow: Cannot call `n.toFixed` because property `toFixed` is missing in null [1].
```
