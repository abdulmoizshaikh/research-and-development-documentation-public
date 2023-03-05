# Gaper.io

Moiz tech assessment interview at 25 Oct 2021 from 9:30am to 10 am
Adeel from gaper team

Questions

Nodejs
1-what is event loop?

interview questions gaper.io adeel

what will the output for this code ?

code:

```jsx showLineNumbers
function foo() {
  console.log(1);
  setTimeout(() => {
    console.log(2);
  }, 0);
  const task = new Promise((resolve, reject) => {
    resolve(3);
  });
  task.then((res) => console.log(res));
  console.log("bye");
}
foo();

answer;
1;
bye;
3;
2;
```

what is the schema for

group chat of user and 1-1 chat of users in db

- Sql vs no sql
- have you worked on vue.js
- how much you rate yourself on english speaking = 7
- how much you rate yourself on redis = 8
- are you comfortable working with backend = yes hi bolna tha or kuch keh nhe sakta q k muje apni job nhe gawani thi job main yehi hota hy hr chez hr call pe han kehna parhta hy q k companies k pass boht selective projects hote hain ap apne marzi ki tech pe kam nhe kr sakte wo alag bat hy k unhe need ho apki favourite tech ki

**What is the difference between settimeout with 0 time and set interval**

```jsx showLineNumbers
setTimeOut(() => console.log(1), 0);
Vs;
setImmediate(() => {});
```

What will happen if we call setTimeout () with a time of 0 ms?

Explanation : If you call setTimeout() with a time of 0 ms, the function you specify is not invoked right away. Instead, it is placed on a queue to be invoked “as soon as possible” after any currently pending event handlers finish running.

**FAQs**

They people are hiring tech partners or individual contractors and allocate their resources to their clients having specific tech skills requirements ( not for themselves )

They chose those client who are willing to atleast one year contract and have that amount of money they can pay at 1 year atleast for making better relation with clients and partners.

Correction in CV

Correct the spelling of requirctment to recruitment (q to c)
Remove UX/UI designer from CV because you are not an UX UI designer any more
Only add those skills in your CV in which you want to work in future. And remove all extra skills that you don't want to work in future.
