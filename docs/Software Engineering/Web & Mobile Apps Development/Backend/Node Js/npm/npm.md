# NPM

## npm commands cheat sheet

```bash showLineNumbers
Short forms
i = install
-D = --save-dev
```

`shortcut to install dev dependency by -D flag`

e.g npm install -D nodemon

OR

```bash showLineNumbers
$ npm install --save-dev nodemon
```

Because -dev is deprecated and commands are case sensitive -D !== -d in npm

**--silent flag :**

This will install all the dependencies in a very linear and clean way without showing any error.

e.g

```bash showLineNumbers
$ npm install --silent
```

https://stackoverflow.com/questions/34426332/how-to-suppress-output-when-running-npm-scripts
