# NextJS

**from which file next js start bootstrap**

`the Next. js entry pages/\_app. js file`

To load Bootstrap in our project, we only need to load the stylesheet in our \_app. js file like so: import 'bootstrap/dist/css/bootstrap. css'; function MyApp({Component, pageProps}) { return <Component {...20-Oct-2021

Following the installation of Bootstrap, we can import the minified Bootstrap CSS file into the Next. js entry pages/\_app. js file, as shown below: import "bootstrap/dist/css/bootstrap.08-Jul-2022

https://daily-dev-tips.com/posts/using-bootstrap-in-nextjs-free-starter/#:~:text=To%20load%20Bootstrap%20in%20our,return%20%3CComponent%20%7B...

## Let's see how to configure Prettier in Next.js.

[Next.js] Prettier

Solution:

```bash showLineNumbers
npm install --save-dev prettier
```

```jsx showLineNumbers title=".prettierrc.js"
module.exports = {
  semi: false,
  singleQuote: true,
  trailingComma: "all",
};
```

```jsx showLineNumbers title="package.json"
"scripts": {
  ...
  "format": "prettier --check --ignore-path .gitignore .",
  "format:fix": "prettier --write --ignore-path .gitignore ."
},
```

```bash showLineNumbers  title="terminal"
npm run format

npm run format:fix

npm run format

Checking formatting...
All matched files use Prettier code style!
```

https://dev-yakuza.posstree.com/en/react/nextjs/prettier/

## Build and Deploy THE PERFECT Portfolio Website | Create a Portfolio from Scratch

https://www.youtube.com/watch?v=OPaLnMw2i_0&list=PL6QREj8te1P7gixBDSU8JLvQndTEEX3c3&ab_channel=JavaScriptMastery
