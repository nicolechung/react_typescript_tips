# Typescript, Webpack and aliases

Sometimes instead of typing a longer path:


```javascript
import SomeModule from './src/components/SomeModule'
```

You'd like to type a shorter version, for example:

```javascript
import SomeModule from './components/SomeModule'
```

Webpack will use `resolve.alias` provide shortcuts to certain folders:

Something like the following in your webpack config:
`webpack.common.config.js`
```javascript
alias: {
  components: path.resolve(__dirname, './src/components'),
}
```



However, if you set up an alias in Webpack, it also needs to be set up in your typescript configuration:

`tsconfig.json`
```javascript
"paths": {
  "components": [
    "./src/components"
  ]
}

```