# EcmaScript modules

Evaluated statically; may only appear in top-level scope.

### Named exports

__Exporting__

```javascript
//const sin = Math.sin
export { sin }
```

```javascript
//const sin = Math.sin
//const cos = Math.cos
export { sin, cos }
```

```javascript
//const tan = Math.tan
export { tan as tg }
```

```javascript
export const tg = Math.tan
```

```javascript
export function ctg( x ){ return 1 / Math.tan(x) }
```


__Importing__

```javascript
import { sin } from "./relative/path"
```

```javascript
import { sin, cos } from "./relative/path"
```

```javascript
import { tg as tangent } from "./relative/path"
```

```javascript
import * as trig "./relative/path"               // Import all named exports into an object.
```

```javascript
import "./relative/path"                         // For side effects only.
```



### Default export

Just another named export with special syntax.

__Exporting__

```javascript
export default Math.tan
```

```javascript
export default function(){}
```

```javascript
export default class {}
```

```javascript
//const tan = Math.tan
export { tan as default }                              // Named exports syntax.
```

__Importing__

```javascript
import tangent from "./relative/path"
```

```javascript
import { default as tangent } from "./relative/path"   // Named exports syntax.
```


# Node modules

__Exporting__

By assignment to `module.exports`, which is initially an empty object (additionally referenced by `exports`).

```javascript
module.exports = Math.tan
```

__Importing__

Calling `require()` returns the assigned value.

```javascript
const tg = require("./relative/path")
```

Requiring an absolute path subjects the module to __node resolution mechanism__ - either return a core module or recursively look up `node_modules` of the parent directory until the module is found or root is reached.