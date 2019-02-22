# Why don't my imports work like a normal React project?

Often when starting a Typescript project, you will find you have to change your imports to something like this:


```
import * as React from 'react'
```

This is because not all libraries you will use are written with ES2015/ES6/ESNext style imports. To get around this, you must set **allowSyntheticDefaultImports** to true:


```
// tsconfig.json
{
  "compilerOptions": {
    "allowSyntheticDefaultImports": true, // see below
  }
}
```

Then you will be able to use imports like this:

```
import React from 'react'
```