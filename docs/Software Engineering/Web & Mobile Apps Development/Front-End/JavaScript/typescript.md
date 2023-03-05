# Typescript

**What is typescript ?**

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. In this guide we will learn how to integrate TypeScript with webpack.

### What does the "as" keyword do?

That is not vanilla JavaScript, it is TypeScript. as any tells the compiler to consider the typed object as a plain untyped JavaScript object.

The as keyword is a Type Assertion in TypeScript which tells the compiler to consider the object as another type than the type the compiler infers the object to be.

```jsx showLineNumbers
var a = 'TEST STRING'
var b = a as string; //Means the compiler will assume it's a string

// or you can match enum type as well

export enum HefazatProductType {
  EW6M = 'EW6M',
  EW12M = 'EW12M',
  PP3M = 'PP3M',
  PP6M = 'PP6M',
  SC_ADPAD = 'ADPAD',
  SC_APAD = 'APAD',
  SA_PP12M = `SA_PP12M`,
  SC_AD = `AD`,
};

const hefazatProductType = request.ewPlan.planName as HefazatProductType;

```

https://stackoverflow.com/questions/55781559/what-does-the-as-keyword-do

**Prop types in typescript**

https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example/

**“decimal type in typescript” Code Answers decimal type in typescript react native**

// There is no int type, use number
const myInt: number = 17;
const myDecimal: number = 17.5;
https://www.codegrepper.com/code-examples/typescript/decimal+type+in+typescript

https://reactnavigation.org/docs/typescript/

**Enum constants support in typescript**

https://blog.logrocket.com/writing-readable-code-with-typescript-enums-a84864f340e9/
https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-4.html
https://stackoverflow.com/questions/29844959/enum-inside-class-typescript-definition-file

```jsx showLineNumbers
E.g
enum Colors {
 Red = "RED",
 Green = "GREEN",
 Blue = "BLUE"
}
```

The caveat is that string-initialized enums can’t be reverse-mapped to get the original enum member name. In other words, you can’t write Colors["RED"] to get the string "Red".

```jsx showLineNumbers
//types
enum AddCustomerEnum {
   ADD_CUSTOMER_SUCCESS = 'ADD_CUSTOMER_SUCCESS',
}
export default class Action {
   static readonly AddCustomerEnum = AddCustomerEnum;

   static AddCustomerSuccess(payload: any) {
       return {
           type: AddCustomerEnum.ADD_CUSTOMER_SUCCESS,
           payload,
       };
   }
}

```

## TypeScript errors

**Could not find a declaration file for module 'module-name'. '/path/to/module-name.js' implicitly has an 'any' type
**
"528

Here are two other solutions

When a module is not yours - try to install types from @types:

npm install -D @types/module-name
If the above install errors - try changing import statements to require:

// import \* as yourModuleName from 'module-name';
const yourModuleName = require('module-name');"

https://stackoverflow.com/questions/41292559/could-not-find-a-declaration-file-for-module-module-name-path-to-module-nam
