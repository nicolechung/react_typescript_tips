# How to read Typescript error messages

Typescript error messages are hard to read.

Oftentimes you will see something like this:

```typescript
Argument of type '{ specialType: string; id: string; }' is not assignable to parameter of type 'MySpecialProps'.
  Property 'result' is missing in type '{ specialType: string; id: string; }' but required in type 'MySpecialProps'. [2741]
```

The error message is hard to read because there is no colour coding - Typescript was built with Javascript, and uses the TypeError type to describe the error, which has no formatting built in.

### Some tips to read Typescript errors:
1. Usually you can safely ignore the first sentence, it's just telling you that you have an error.
2. Scan for the `property` which has an error, in the case above it's the property named `result`.
3. Look up the error code in square brackets, in this case it's `[2721]`.
4. If a line error is given, look at that line.

### Example 1
Here is the bit of code where that error is happening:

```typescript
interface MySpecialProps {
  result: JSON,
  id: string,
  specialType: string
}
export function generateResult(id:string): MySpecialProps {
  const { id, specialType } = this.state.results[id]

  return {
    id,
    specialType,
  }
}
```

We see that the function `generateResult` should return an object that uses the `MySpecialProps` interface, which has a `required` result property.

Adding that property makes the error go away:

interface MySpecialProps {
  result: JSON,
  id: string,
  specialType: string
}
export function generateResult(id:string): MySpecialProps {
  const { result, id, specialType } = this.state.results[id]

  return {
    id,
    specialType,
    result: JSON.stringify(result)
  }
}

### Example 2

```typescript
interface Images {
  [key:string]: string;
}

function getMainImageUrl(images: Images): string {
  return images.main;
}
```

Error message:
```
error TS2339: Property 'main' does not exist on type 'Images'.
```

Solution:
Define `main` on the interface `Images`:

```typescript
interface Images {
    main: string;
    [key:string]: string;
}

function getMainImageUrl(images: Images): string {
    return images.main;
}
```
