# Typescript: Interfaces and React

A lot of typescript examples explain how to type a `const` in this format:

```typescript
const count:number = 3
```

But in React you usually need to declare the types in an interface:

```typescript
interface MyReactProps {
  count: number
}

// sample stateless component
const Header: React.SFC<MyReactProps> = ({count}) => <h2>{count}</h2>
```

Below are some common of examples of things you will have to type, and ways to go about declaring the type.

# Easy

## Numbers:

```typescript
// assignment:
count = 1

// interface:
count:number
```

## Strings:

```typescript
// assignment:
name = 'Nicole'

// interface:
name:string
```

## Number or a string:

```typescript
count: number | string
```

It can also be a number or a specific string (useful for css):
```typescript
height: number | 'auto'
```

## Dates

Dates are often stored as numbers:

```typescript
date: number
```

Then this can be used like

```typescript
date = Date.now()
```

Dates stored as strings:

```typescript
// assignment
date = 'Friday, January 3'

// interface
date: string
```

Dates stored as `Moment` objects:

```typescript
import moment from 'moment'

// in your interface

lastPublishedDate: moment.Moment
```

## React components:

```typescript
title: JsxElement
```

## React `children`:

```typescript
children: React.ReactNode
```

Another way to type React children, if you are returning a variety of things (strings, a React component, or a list of React components):

```typescript
children?:
    | JSX.Element
    | JSX.Element[]
    | string
    | Array<JSX.Element | JSX.Element[] | string>
```

# Medium - Arrays

## Array of numbers
```typescript
// assignment
countingList = [1,2,3,4,5]

// interface
countingList: number[]
```

## Array of strings
```typescript
// assignment
stringList = ['a', 'b', 'c', 'd']

// interface
stringList: string[]
```

## Array of custom objects
An array of __objects__ is more complicated. First, it's good to create an interface for your object:

```typescript
interface MyObject {
  name: string,
  type: string,
  date: number
}
```

The type declaration / interface would then be:

```typescript
listOfMyObjects: MyObject[]
```

Sometimes you will have interfaces that can return an `Array` of multiple types. In this case we stop using the `[]` notation and use the `Array<>` notation instead:

```typescript
result: Array<
    OneInterface | AnotherInterface | AThirdInterface
  >
```

# Medium - Functions

This is how you would type a function that doesn't have any parameters and does not return anything:

```typescript
// the function
() => { console.log('hello') }

// interface
emptyFunction: () => {}
```


Often, for events, you will need to pass in an event type:

```typescript
// the function
(event) => { console.log(event.target.value) }

// interface
onClick: (event:any?) => {}
```

For React, you can type this to `React.MouseEvent`

```typescript
// the function
(event) => { console.log(event.target.value) }

// interface
onClick: (event:React.MouseEvent) => {}
```



### Functions that return React Components

```typescript
loading: () => <Spinner />
```

### Curried functions

Without getting into a super-long explanation of what currying is, other than what we see it as in React:

```typescript
<SomeComponent onClick={onClick} />
```

A component takes an `onClick` event handler. React assumes that the `event` object is passed along.

```typescript
// handler
onClick = (event) => {
  console.log(event.target.value)
}
```

Often in React however, what we want more than the object is some bit of state passed along.

```typescript
<SomeComponent onClick={onClick(this.state.id)} />
```

Now the handler would be rewritten like this, with the help of arrow functions:

```typescript
onClick = (id) => (event) => {
  // do something with the id and maybe the event here
}
```

In the case of curried functions, you can define the interface / type definition of that value as an arrow function:

```typescript
// interface
onClick: (id: string) => (event?:any) => void
```


### Functions that return Promises

```typescript
// the function
() => { return new Promise() }

// interface
onClick: () => Promise<any>
```

If your promise returns, say, an array of strings, you can type it like this:

```typescript
// interface
onClick: () => Promise<string[]>
```

A lot of times, your promise will return json:

```typescript
// interface
result: () => Promise<JSON>
```


# Medium - Objects

## Objects with unknown key/value pairs
Sometimes you have objects where you don't know the key names up front (maybe just the values). In this case it's still handy to have a broad type like this:

```typescript
export interface EventLabel {
  [key: string]: number
}
```
## Objects with functions as values
Another case is typing an `object` that is really a list of functions that all return the same data type:

```typescript
// the interface
interface ValidateFunctionType {
  [key: string]: (value: any) => boolean
}

// the object
const validateFunctions: ValidateFunctionType = {
  dateRange: value => {
    return dateRangeValues.includes(value)
  },
  rankBy: value => {
    return sortTypeValues.includes(value)
  },
  // and so on...
}
```

