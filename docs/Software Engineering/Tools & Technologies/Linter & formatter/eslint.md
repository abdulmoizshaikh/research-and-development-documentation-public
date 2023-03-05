# Eslint

To extend the eslint rules. I put some custom rules for better coding conventions. If your want to extend eslint rules, Goto theeslintc.jsonfile and put your custom rules inside the "rules":{}.

If you interested in custom rules please refer:

https://github.com/ShalithaCell/Eslint-Rules-ReactJs

https://github.com/ShalithaCell/Eslint-Rules-ReactJs

https://medium.com/geekculture/setting-up-a-react-app-from-scratch-withwebpack-babel-and-eslint-57eb3dcaf2e9

These errors are coming from the Eslint.

Errors! What do I do?

There are multiple ways to resolve Eslint errors and warnings.

use — fix command

setup IDE to check Eslint configurations.

1. Use — fix

   Add the following line to package.json the file.

   scripts: {
   lint: "eslint --fix --ext .js,.jsx ."
   }

   now script tag like,

   scripts: {
   start: "webpack serve --mode development",
   lint: "eslint --fix --ext .js,.jsx .",
   test: "echo \"Error: no test specified\" && exit 1"
   },

   Then run it with npm run lint

   So we again run the project npm run startand check errors are gone.

2. Setup IDE to check Eslint configurations.

   Refer to the below link for configuring WebStrom and VS Code.

   Enabling ESLint on Intellij & VSCode

   ESLint is a pretty cool tool that cleans up your Javascript code for you! But when you're deving on an IDE such as…

   dev.to

https://dev.to/blaytenshi/enabling-eslint-on-intellij-vscode-3614

HOW TO SETUP ESLINT AND PRETTIER FOR YOUR REACT APPS

https://thomaslombart.com/setup-eslint-prettier-react

eslint rules a big list of rules

https://eslint.org/docs/rules/
