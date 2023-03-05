# prettier format configure

1. VSCode single to double quote automatic replace https://stackoverflow.com/questions/48864985/vscode-single-to-double-quote-automatic-replace

   missing trailing comma error coming https://stackoverflow.com/questions/61876933/how-to-turn-off-the-prettier-trailing-comma-in-vs-code

   add this in setting.json (CTRP+SHIPT+P and type setting.json ENTER)

   // Controls the printing of trailing commas wherever possible. Valid options:

   // - `none` - No trailing commas

   // - `es5` - Trailing commas where valid in ES5 (objects, arrays, etc)

   // - `all` - Trailing commas wherever possible (function arguments)

   **prettier.trailingComma: "all",**

2. **when i format the code using prettier this error comes > Unexpected parentheses around single function argument having a body with no curly braces in prettier**
   paste this line in setting ,json

   `"prettier.arrowParens": "avoid"` arrow-parens prettier

   https://github.com/prettier/prettier-vscode/issues/390

3. HOW TO SETUP ESLINT AND PRETTIER FOR YOUR REACT APPS

   https://thomaslombart.com/setup-eslint-prettier-react
