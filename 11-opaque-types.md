# Opaque types

Unique feature for Flow.

- [Opaque types in Flow](https://flow.org/en/docs/types/opaque-types/)
- [How to emulate opaque types in TypeScript​](https://codemix.com/opaque-types-in-javascript/)

```javascript
// uuid.js

export opaque type UUID = string;
​
export function validate(s: string): UUID {
  // validate s
  return s;
}
```

```javascript
// index.js

import type { UUID } from "./uuid";
import { validate } from "./uuid";
​
interface User {
  name: string;
}
​
declare function fetchUser(uuid: UUID): Promise<User>;
​
fetchUser(""); // Cannot call `fetchUser` with `"123"` bound to `uuid` because string [1] is incompatible with `UUID` [2]
fetchUser(validate("")); // OK
```
