# JavaScript

**javascript language developed in**

`1995`

JavaScript was invented by Brendan Eich in 1995. It was developed for Netscape 2, and became the ECMA-262 standard in 1997. After Netscape handed JavaScript over to ECMA, the Mozilla foundation continued to develop JavaScript for the Firefox browser.

**How to convert es5 to es6 javascript**

https://parthpadhiar.medium.com/convert-es5-to-es6-node-js-a061d7b2403a

https://stackoverflow.com/questions/44005242/how-can-i-check-app-installed-in-react-native-code

https://stackoverflow.com/questions/41655898/react-native-rtl-on-android

<br/>

### Datastructure in javascript

**JavaScript Hash Table – Associative Array Hashing in JS**

implement hashtable using Map and set in Javascript

https://javascript.info/map-set

https://www.freecodecamp.org/news/javascript-hash-table-associative-array-hashing-in-js/

## Destructuring assignment

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

## Sets in Javascript

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set

## Using async/await with a forEach loop

Sure the code does work, but I'm pretty sure it doesn't do what you expect it to do. It just fires off multiple asynchronous calls, but the `printFiles` function does immediately return after that.

### Reading in sequence

If you want to read the files in sequence, **you cannot use `forEach`** indeed. Just use a modern `for … of` loop instead, in which `await` will work as expected:

```js showLineNumbers
async function printFiles() {
  const files = await getFilePaths();

  for (const file of files) {
    const contents = await fs.readFile(file, "utf8");
    console.log(contents);
  }
}
```

dont use foreach for async tasks use for loop or for of loop to do blocking tasks like if you want to call api in sequence

https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop

### How to convert number into comma separated value ?

Solution:

```jsx showLineNumbers
import numeral from "numeral";
export const numberWithCommas = (x) => numeral(x).format("0,0");
```

### FOR of vs For loop

both are synchonous by nature means they can executer async operation as well in sync manner

For off syntex is good and readable as compare to for loop

The difference between for of and for loop is that

for off loop can run on only 1 array

but in for loop we can run multiple array in it of same length

for off

```jsx showLineNumbers
for (const span of spans) {
  const productModelPrice = span.innerText;
  if (productModelPrice != null) {
    modelsPrices.push(productModelPrice);
  }
}
```

for loop

```jsx showLineNumbers
for (let i = 0; i < spans.length; i++) {
  const productModel = h4Elements[i].querySelector("a").getAttribute("title");
  const productPrice = spans[i].innerText;
  if (productPrice != null && productModel != null) {
    modelsAndPrices.push({
      price: productPrice,
      model: productModel,
    });
  }
}
```

**For await loop in javascript**

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of

**foreach async vs for of sync**

https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop

**Fastest way to convert JavaScript NodeList to Array?**

With ES6, we now have a simple way to create an Array from a NodeList: the [`Array.from()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from) function.

```js showLineNumbers
// nl is a NodeList
let myArray = Array.from(nl);

or;
document.querySelectorAll("img").forEach(highlight);
```

https://stackoverflow.com/questions/3199588/fastest-way-to-convert-javascript-nodelist-to-array

### JAVASCRIPT :

**how to add property based on condition ternary operator javascript**

“javascript ternary add property to object” Code Answer’s

Solution:

```jsx showLineNumbers
const a = {
   ...(someCondition && {b: 5})
}


 ...(params && { params }),

_navigator.dispatch(
   CommonActions.navigate({
     name: routeName,
     ...(params && { params }),
   }),
 );
```

https://www.codegrepper.com/code-examples/javascript/javascript+ternary+add+property+to+object

**How to create array of dynamic length in javascript**

How to create dynamic array in javascript by just passing it length
javascript - Create Simple Dynamic Array
dynamic create array javascript

```jsx showLineNumbers
{
  Array.from({ length: dotCount }).map((item, index) => (
    <LoaderComponent key={index} />
  ));
}
```

https://stackoverflow.com/questions/10451893/javascript-create-simple-dynamic-array

**How do you get a timestamp in JavaScript?**

```jsx showLineNumbers
Date.now();
```

https://stackoverflow.com/questions/221294/how-do-you-get-a-timestamp-in-javascript

**How do I check that a number is float or integer?**

how to check numbers is floating point in javascript

```jsx showLineNumbers
400
check for a remainder when dividing by 1:

function isInt(n) {
   return n % 1 === 0;
}
If you don't know that the argument is a number you need two tests:

function isInt(n){
    return Number(n) === n && n % 1 === 0;
}
// make sure to pass number in it not string
function isFloat(n){
    return Number(n) === n && n % 1 !== 0;
}

```

Actual code implementation”

```jsx showLineNumbers
//utils.js
export const isFloat = (n) => Number(n) === n && n % 1 !== 0;

   const handleSubmit = () => {
       let updatedTotal = getUpdateAmount();
       if (isFloat(Number(updatedTotal))) { // this code
           updatedTotal = Boolean(updatedTotal) && Number(updatedTotal).toFixed(2);
       }

       const data = new FormData();
       if (photos && photos.length > 0) {
           photos.forEach((element: any, i: number) => {
               const newFile = {
                   uri: element?.uri,
                   type: element?.type,
                   name: element?.fileName,
               };
               data.append(`images[${i}]`, newFile); //image or images
           });
       }
```

https://stackoverflow.com/questions/3885817/how-do-i-check-that-a-number-is-float-or-integer

**What is context of an object?**

A context object encapsulates the references/pointers to services and configuration information used/needed by other objects. It allows the objects living within a context to see the outside world. Objects living in a different context see a different view of the outside world.

https://wiki.c2.com/?ContextObject

**What is context and scope in JS?**

Context is related to objects. It refers to the object to which a function belongs. When you use the JavaScript “this” keyword, it refers to the object to which function belongs. Scope refers to the visibility of variables, and content refers to the object to which a function belongs.

https://blog.kevinchisholm.com/javascript/difference-between-scope-and-context/

**What is context in javascript? (ask by sunoono lead in Aleem NGI interview)**

In JavaScript, “context” `refers to an object`. Within an object, the keyword “this” refers to that object (i.e. “self”), and provides an interface to the properties and methods that are members of that object. When a function is executed, the keyword “this” refers to the object that the function is executed in.

**Replacing switch statements with Object literals**

https://ultimatecourses.com/blog/deprecating-the-switch-statement-for-object-literals

**execution context javascript **

Main chez hain js ki yehi se javascript shuru hoti hy
Apko pata chalega program chal kaise raha hy

**Convert object into Array:**

```jsx showLineNumbers

let obj={name:'moiz',val:'1'}
Object.keys(yourObject) return keys of object in array form
Object.values(yourObject) return values of that object keys in array form
E.g

let obj={name:'moiz',val:'1'}

Object.values(obj)
(2) ['moiz', '1']

Object.keys(obj)
(2) ['name', 'val']


How to trim string and add … at last
var string = "this is a string";
var length = 20;
var trimmedString = string.length > length ?
                    string.substring(0, length - 3) + "..." :
                    String;
```

https://stackoverflow.com/questions/7463658/how-to-trim-a-string-to-n-chars-in-javascript

https://stackoverflow.com/questions/34151834/javascript-array-contains-includes-sub-array

**difference between array.includes and array.sub **
https://stackoverflow.com/questions/34151834/javascript-array-contains-includes-sub-array

**difference between array.includes and array.sub **
https://www.npmjs.com/package/react-native-tab-view

**use this library with react navigation library as given in example**
https://reactnavigation.org/docs/material-top-tab-navigator/

this.addEventListener

Addeventlistner will be use for listening dom element
This in event listener dom element will give dom element and we can access dom through this

**difference between array.call or array.apply**

c for comma (call me comma separated values dyte hain)
a for array (apply main array dyte hain params main)

**Namaste javascript playlist for All Javascript concepts : (recommended by Arsalan bhai and Zubair)**

https://www.youtube.com/watch?v=pN6jk0uUrD8&list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP&ab_channel=AkshaySaini

# Javascript.info

### The Modern JavaScript Tutorial

**ECMAScript**

ECMAScript (/i.si.ɛmˈeɪskrɪpt/) (or ES)[1] is a general-purpose programming language, standardised by Ecma International according to the document ECMA-262. It is a JavaScript standard meant to ensure the interoperability of Web pages across different Web browsers.[2] ECMAScript is commonly used for client-side scripting on the World Wide Web, and it is increasingly being used for writing server applications and services using Node.js.

## Javascript-concepts

array.find javascript that return boolean use array.some()

https://stackoverflow.com/questions/41943912
/is-there-a-function-which-returns-true-or-false-when-searching-for-an-object-in?rq=1"

**closures in for loop javascript using iife**

```jsx showLineNumbers

e.g with IIFE is closures

for (var j = 0; j < 10; j++) {
// IIFE
(function(j) {
setTimeout(function() {
console.log(""IIFE "" + j);
}, 1000 _ j);
})(j);
}
response
IIFE 0
VM82:5 IIFE 1
VM82:5 IIFE 2
VM82:5 IIFE 3
VM82:5 IIFE 4
VM82:5 IIFE 5
VM82:5 IIFE 6
VM82:5 IIFE 7
VM82:5 IIFE 8
VM82:5 IIFE 9


not closures


for (var j = 0; j < 10; j++) {
// IIFE
// (function(j) {
setTimeout(function() {
console.log(""IIFE "" + j);
}, 1000 _ j);
// })(j);
}
(10) IIFE 10 "

```

https://stackoverflow.com/questions/49625909/invoke-
settimeout-in-iife-against-standard-in-a-loop

https://stackoverflow.com/questions/750486/javascrip
t-closure-inside-loops-simple-practical-example

what does double question mark mean in javascript

The JavaScript double question mark is also known as the nullish
coalescing operator. It's an operator that simply returns the right-side
expression when the left side expression is either null or undefined .20-May-2021"

https://sebhastian.com/javascript-double-question-mark/#:~:text=The%20JavaScript%20double%20question%20mark,is%20either%20null%20or%20undefined%20.

shallow copy vs deep copy

spread operator do deep clone in first level child but sallow cloning in nested child
solution JSON.parse(JSON.stringify(object)) but one problem is that this will not work with function in nested clild cloned

https://www.google.com/search?q=shallow+copy+vs+deep+copy&oq=shallow+cop&aqs=chrome.2.69i57j0i512l9.5679j0j7&sourceid=chrome&ie=UTF-8

https://stackoverflow.com/questions/122102/what-is-the-most-efficient-way-to-deep-clone-an-object-in-javascript

memory leak in javascript

"What is == called in JavaScript?

In Javascript, we have couple of options for

checking equality: == (Double equals operator):

Known as the equality or abstract comparison operator. === (Triple equals operator):

Known as the identity or strict comparison operator.12-Oct-2019"

Array.prototype.groupBy to the rescue! Javascript Array new method

https://www.charpeni.com/blog/array-prototype-group-by-to-the-rescue

## Bookmarks

### Explore Topics and integrate in app

- [Build Apps with JavaScript | Meteor](https://www.meteor.com/)

**How to resolve setTimeout() inside for loop**

how to add timeout inside for loop in javascript

https://www.linkedin.com/pulse/how-resolve-settimeout-inside-loop-ibe-stephen/
