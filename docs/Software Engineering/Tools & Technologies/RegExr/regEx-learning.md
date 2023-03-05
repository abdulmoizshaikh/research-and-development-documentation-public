# RegEx learning

Learning Guide : https://regexr.com/

Javascript remove all '|' in a string [duplicate]

```jsx showLineNumbers
const text = "A | normal | text |";
let final = text
  .split("")
  .filter((c) => c !== "|")
  .join("");
console.log(final);
```

OR

```jsx showLineNumbers
var text = "A | normal | text |";
var final = text.replace(/\|/g, "");
console.log(final);
```

https://stackoverflow.com/questions/42554744/javascript-remove-all-in-a-string

## Regex templates

### regex used in hisaab app project

```jsx showLineNumbers
import { Toast } from "native-base";
import { Fonts, Colors } from "../theme";
const passwordRegex = /^(?=.*d)(?=.*[A-Z])(?=.*[a-z])([^s]){8,16}$/;
const emailRegex = /^w+([.-]?w+)*@{1}w+([.-]?w+)*(.[a-zA-Z]{2,3})+$/;
const fullNameRegex =
  /^([a-zA-Z]+|[a-zA-Z]+s{1}[a-zA-Z]{1,}|[a-zA-Z]+s{1}[a-zA-Z]{3,}s{1}[a-zA-Z]{1,})$/;
const phoneNoRegex = /^[+]?[(]?[0-9]{3}[)]?[-s.]?[0-9]{3}[-s.]?[0-9]{4,6}$/im;
const cityRegex = /^([^0-9]*)$/;
const newFullNameRegex = /^[ws]{4,20}$/;
const pollTitleRegex = /^[ws]{3,50}$/;
export function validatePassword(password: string) {
  return passwordRegex.test(password);
}
export function validatePhoneNumber(phone: string) {
  return phoneNoRegex.test(phone);
}
export function validateEmail(email: string) {
  return emailRegex.test(email);
}

export function validateAlpha(name: string) {
  return fullNameRegex.test(name);
}

export function validateFullName(name: string) {
  //return fullNameRegex.test(name);
  return newFullNameRegex.test(name);
}
export function validateTitle(name: string) {
  //return fullNameRegex.test(name);
  return pollTitleRegex.test(name);
}

export function validateCity(name: string) {
  return cityRegex.test(name);
}

export function showToast(message: string, type = "danger") {
  Toast.show({
    text: message,
    position: "bottom",
    type,
    textStyle: { fontFamily: Fonts["Poppins-Regular"], textAlign: "center" },
    duration: 3000,
  });
}
```
