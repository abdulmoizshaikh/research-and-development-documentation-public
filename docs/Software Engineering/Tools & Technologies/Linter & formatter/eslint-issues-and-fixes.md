# Eslint issues and fixes

1 getStuff(model = this.state.model) { // eslint-disable-line

https://stackoverflow.com/questions/53285530/react-eslint-destructuring-assignment

// eslint-disable-line

https://stackoverflow.com/questions/40271230/how-to-run-eslint-fix-from-npm-script

## eslint-error-fixing

**ESLint with React gives `no-unused-vars` errors**

https://thomaslombart.com/setup-eslint-prettier-react

https://github.com/yannickcr/eslint-plugin-react

https://stackoverflow.com/questions/42541559/eslint-with-react-gives-no-unused-vars-errors

```json showLineNumbers
{
""env"": {
""commonjs"": true,
""es6"": true,
""node"": true
},
""extends"": [""eslint:recommended"", ""plugin:react/recommended""],
""parser"": ""babel-eslint"",
""parserOptions"": {
""ecmaVersion"": 2020,
""sourceType"": ""module"",
""allowImportExportEverywhere"": true
},
""rules"": {
""no-console"": ""error""
}
}
```

**ignore eslint error: 'import' and 'export' may only appear at the top level**

```jsx showLineNumbers
{
""parser"": ""babel-eslint"",
""parserOptions"": {
""sourceType"": ""module"",
""allowImportExportEverywhere"": true
}
}
```

https://stackoverflow.com/questions/39158552/ignore-eslint-error-import-and-export-may-only-appear-at-the-top-level

**error 'document' is not defined : eslint / React**

Add "browser": true your env to include global variables (like document, window, etc.)

```json showLineNumbers
"env"": {
""commonjs"": true,
""es6"": true,
""node"": true,
""browser"": true
},
```

https://eslint.org/docs/user-guide/configuring/language-options#specifying-environments
