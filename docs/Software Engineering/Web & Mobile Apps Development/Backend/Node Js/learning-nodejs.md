# Learning NodeJs

## 15 Best Node.js Tools for Developers

https://brainhub.eu/library/node-js-tools-for-developers

## Debugging nodejs

launch .json by baqir bhai

```json showLineNumbers
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Vendians backend",
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}/server.js",
      "outFiles": ["${workspaceFolder}/**/*.js"]
    }
  ]
}
```

https://code.visualstudio.com/docs/editor/debugging#_launch-configurations

close process from terminal and run project through debugger in debug mode and add break points and check if its works

## Nodejs Learning and Fixes

Online counselling app fixes

To allow mail server smtp using your personal gmail account in nodemailer you have to enable and allow these two things

1. Enable less secure app
   https://myaccount.google.com/lesssecureapps

   Gmail SMTP error - Temporary block?

   ```
   If you are using your free Gmail account to send bulk emails your are likely to see this kind of responses early on as the service is not intended to send application transaction messages, newsletters etc., event to subscribers that has opted in. The IMAP/SMTP service provided is for you to be able to use an email client like Microsoft Outlook with your Gmail account.

   If you need to send transaction messages, I suggest you google "AWS SES" for starters.
   ```

   Gmail free service is not intended to send bulk emails or newsletters
   Solution:
   We have to use Amazon SES for email sending.

   https://stackoverflow.com/questions/39097834/gmail-smtp-error-temporary-block

2. Allow access to your Google account
   https://accounts.google.com/b/0/DisplayUnlockCaptcha

Nodejs Learning Articles /blogs

**Push notification using Node.js**

https://stackoverflow.com/questions/45100293/push-notification-system-in-nodejs-with-android-and-ios
https://onesignal.com/

**Setting Schedule Push notification using Node.js and MongoDB**

https://medium.com/@izaanjahangir2/setting-schedule-push-notification-using-node-js-and-mongodb-95f73c00fc2e

**Project Setup**

In order to understand how our project is set up, we will go through the individual folder structures which follow the MVC (Model View Controller) pattern. As a recap of the MVC pattern, the model defines the schema of the data in the database and how it will be stored. Controllers hold the business logic of the application while the view holds all our routes.

Inside the app folder, we have user and utils folders which are responsible for the user resource and database configuration respectively. The index.js file, which is the entry point of our app, is responsible for express setup. In this project, we will use ES6 and Babel to compile the code. I have also configured nodemon to listen to any changes made to the app then reload the server.

**BEST PRACTICES**

Use

`"use strict";`

In top of every .js file in nodejs project

Delete user.password not working then do first .toObject() the given respose then delete it will works as below e.g

```jsx showLineNumbers
const response = await (await User.findById(req.params.vendorId)).toObject();
delete response.password;
```

Ref: https://stackoverflow.com/questions/7503450/how-do-you-turn-a-mongoose-document-into-a-plain-object

**Push repo to heroku**

https://devcenter.heroku.com/articles/getting-started-with-nodejs#deploy-the-app

**Remove heroku remote url only**

Removing a remote in git is achieved with the following command:

> git remote rm heroku

**ERR_HTTP_HEADERS_SENT: Cannot set headers after they are sent to the client**

Answer:

That particular error occurs whenever you try to send more than one response to the same request and is usually caused by improper asynchronous code.

https://stackoverflow.com/questions/52122272/err-http-headers-sent-cannot-set-headers-after-they-are-sent-to-the-client

**which one is better for server side**

q,or or blue bird utils.promisify and native promise

use utils.promisify and native promise because it by default installed and promise npm lib is use where it is not included by default like client side on browser if not available by default

not recommended
Es6-promisify,for only one fun we don’t need whole npm pkg
Blue bird ,q we don’t need out off the box function that’s why not required

**ENVIRONMENT VARIABLES IN NODE JS (JOHN PAPA)**

https://medium.com/the-node-js-collection/making-your-node-js-work-everywhere-with-environment-variables-2da8cdf6e786

**Vs code DotENV extension**

https://marketplace.visualstudio.com/items?itemName=mikestead.dotenv&wt.mc_id=node-nodecollection-jopapa

You could write your own code to find the file, parse it, and read them into your Node.js app. Or you could look to npm and find a convenient way to read the variables into your Node.js app in one fell swoop. You’d likely run across the dotenv package on npm, which is a favorite of mine and what I recommend you use. You can install it like this npm install dotenv.

**Note: .env file must be place in root directory of your node project**

Debug node js code in vscode | debugging in nodejs

1 Answer

Are you running the NodeJS in debug mode inside npm start? You need to use the --inspect flag. Without this flag, the NodeJS interpreter won't open the debug port to the VSCode to attach to.

Refer to: https://nodejs.org/en/docs/guides/debugging-getting-started/

Another option is to attach using a port definition. I usually do something like this in the launch.json:

```json showLineNumbers
{
  "type": "node",
  "request": "attach",
  "name": "Attach",
  "port": 9229,
  "restart": true,
  "sourceMaps": true,
  "protocol": "inspector"
}
```

Then I start the NodeJS process as: node --inspect=0.0.0.0:9229 start.js (recommended command and run in vscode embedded terminal not separate terminal)

---

Launch.json

---

// pehle referesh kro debugger ko then check kro break point red hi hain na or
// botton status bar orange hojae to api call kro postman se phr break point work karnge
// make shure you have app.js file opened
// f5 se next break point pe jata hy
// f10 se line by line chalta hy inner procress ignore krta hy
// f11 se line by line bhe jata hy or ander tk bhe jata hy process se bhe

```json showLineNumbers
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attach",
      "port": 9229,
      "restart": true,
      "sourceMaps": true,
      "protocol": "inspector"
    },
    {
      "type": "node",
      "request": "attach",
      "name": "Node: Nodemon",
      "processId": "${command:PickProcess}",
      "restart": true,
      "protocol": "inspector"
    }
  ]
}
```

---

Ref: https://stackoverflow.com/questions/53563469/cannot-find-node-process-using-vscode-debugger (Recommended)

Ref : https://github.com/Microsoft/vscode-recipes/tree/master/nodemon
https://code.visualstudio.com/docs/nodejs/nodejs-debugging
https://www.digitalocean.com/community/tutorials/how-to-debug-node-js-code-in-visual-studio-code

**VSCode debugging not working for NodeJs application**

This below tip will work for me.
Your breakpoints are probably set too early and are not registered by node. It should help if you set the breakpoints after you have attached.

Ref: https://stackoverflow.com/questions/30662723/vscode-debugging-not-working-for-nodejs-application

**Use vim (recommended because it is by default installed in linux distributions)**

```bash showLineNumbers
To open file

> Sudo vi pathtofile
> Press i to goto insert mode
> To clear all content in file
> Type gg (goto top line) then dG (delete all content)
> To backspace press ESC then x to delete content or X
> To save
> Press ESC then :wq hit enter
```

ref:https://vitux.com/how-to-edit-config-files-in-ubuntu/
https://www.google.com/search?q=backspace+in+vim&oq=backspace+in+vim&aqs=chrome..69i57j0l7.3157j0j1&sourceid=chrome&ie=UTF-8

**Queries related document receive specify parnther and admin portal flow**

- All active partners should be visible on the user application
  Is this user application is partner portal or user mobile app

Beanstack username: muhammadmoiz :@iwtsmbsa

review again

**Understant All customer routes apis till 12 pm**

Encrypted server api url
updateLatLng apis

edit api called when account status change to private
add photo api add photo to the user profile
Edit profile(same api pe sari profile related changes update ho rahi hain)
edit profile api update only those fields which are changed

**create account steps signup flow,1,2,3,4,5**

1. check phone no
2. signup (take phone,country_code,device_token,device_type,time_zone,login_type,lat,lng and password then send otp to users number using twilio. sendOtp func
3. verify otp
4. sigup2 (take username. )
5. signup3 (take email)

chat token

discover list api (get by radiues like with in 100meters from me) get near by from me by radius set by user
in dashboard get user with in the given metered range

saved search

work on like when ever i go today i save my location in save search api
and get all save searched list by searchsavesearch list

getdiscoveredprofile details

kisi or ki profile pe jate hain to call hoti hy
me jiski profile see kr raha hun to ye api us user ki deatils le kr ati hy k wo mera friend hy ya nhe y etc

message krte hain to kisi user ko
getisuserblock api 2 bar jati hy

chattoken jb user login hota hy to generate hota hy or user k apne record me save ho jata hy q k chat k feature ko user krne k liye

getsavesearchlist (multiple location jo save ki thi unki list la rahi hy)
jo jo mene search save ki thi wo sari get krne k
user time and address and lat log etc

getSaveSearchDiscoveredFriendList
get save search list item pe click krne pa ye api us location me us waqt jitne users thy unki profiles ki list la dy gi

get use ki base pe save search reponse me send krti hy

Not found

1. savesearch api not found

review search api's in nodejs
create acl in nodejs

**apis ? resolve queries**

getSaveSearchList

getDiscoveredProfileDetails

getSaveSearchDiscoveredFriendList

## Nodejs Learning AskWho

**Social Signin - Facebook Nodejs**

We will use passport-facebook-token, the Passport strategy for authenticating with Facebook access tokens using the OAuth 2.0 API. There is also the passport-facebook library that contains a strategy for Facebook authentication, but this library is not suitable for REST API. It is better suited for Express.js applications which are used for server rendering.

Ref: https://codeburst.io/node-js-rest-api-facebook-login-121114ee04d8

**NodeJs enabling SSL**

https://timonweb.com/posts/running-expressjs-server-over-https/
https://stackoverflow.com/questions/22584268/node-js-https-pem-error-routinespem-read-biono-start-line/34004949

**LOAD TESTING OF API’s**

Using jmeter

JMeter - Open Source Functional and Load Testing. Apache JMeter is open source software, a 100% pure Java desktop application, designed to load test functional behavior and measure performance of web sites. It was originally designed for load testing web applications but has since expanded to other test functions.

https://jmeter.apache.org/

Apache JMeter Review

https://reviews.financesonline.com/p/apache-jmeter/

Example

https://www.youtube.com/watch?v=HGMVnUmqut0&feature=emb_logo

**ERROR 1698 (28000): Access denied for user 'root'@'localhost'**

Solution

```bash showLineNumbers
sudo mysql -u root # I had to use "sudo" since is new installation

mysql> USE mysql;
mysql> SELECT User, Host, plugin FROM mysql.user;

+------------------+-----------------------+
| User | plugin |
+------------------+-----------------------+
| root | auth_socket |
| mysql.sys | mysql_native_password |
| debian-sys-maint | mysql_native_password |
```

Option 1:

```bash showLineNumbers

$ sudo mysql -u root # I had to use "sudo" since is new installation

mysql> USE mysql;
mysql> UPDATE user SET plugin='mysql_native_password' WHERE User='root';
mysql> FLUSH PRIVILEGES;
mysql> exit;

$ service mysql restart
```

Ref: https://stackoverflow.com/questions/39281594/error-1698-28000-access-denied-for-user-rootlocalhost

**Cors:**

```jsx showLineNumbers
var corsOptions = {
  origin: "http://localhost:8081",
};

app.use(cors(corsOptions));
```

https://bezkoder.com/node-js-express-sequelize-mysql/

## Nodejs Learning (JS serverside runtime)

### Responsecode

Response codes:
Usage and meanings of most frequently response codes

- 200 is for success (success when you successfully get your data back specially for get api used)
- 201 is for success for when something change in db and new resource was created mosty used for post apis.
- 401 is for un authorize (auth related stuffs)
- 500 means internal server error
- 404 resourse not found

### Learning nodejs and q/a

nodejs courses

learn rest api from linkedin

https://www.linkedin.com/learning/learning-rest-apis/the-six-constraints-of-rest

interview q/a

1 48+ Top Node.js Interview Questions and Answers in 2021

https://www.simplilearn.com/tutorials/nodejs-tutorial/nodejs-interview-questions

aggregation in mongodb

https://masteringjs.io/tutorials/mongoose/aggregate
https://mongoosejs.com/docs/api/aggregate.html
https://www.youtube.com/watch?v=Kk6Er0c7srU&ab_channel=MikeDane

encodeURL and decodeURL for search API

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURI

### preparation

**Nodejs all topics from office guide**

1. Node.js v15.13.0 documentation https://nodejs.org/api/
2. ECMAScript 2015 (ES6) and beyond https://nodejs.org/en/docs/es6/
3. Guides https://nodejs.org/en/docs/guides/
4. Dependencies https://nodejs.org/en/docs/meta/topics/dependencies/

ye 4ro site chat lo puri nodejs (duniya k sare sawalat) ki tariari hojaegi BC
BC company senior balke architect ki job dyge agr ye sb samjh lia to

https://www.guru99.com/node-js-generators-compare-callbacks.html

## Bookmarks

### Nodejs

- [Node JS Tutorial for Beginners #1 - Introduction](https://www.youtube.com/watch?v=w-7RQ46RgxU&list=PL4cUxeGkcC9gcy9lrvMJ75z9maRw4byYp)

- [FrontendMasters Course Player](https://frontendmasters.com/courses/api-node-rest-graphql/introduction/)

- [CRUD app in expressjs using Mongodb | Mlab in URDU | HINDI](https://www.youtube.com/watch?v=ZMaTY5K_P2E)

- [Coding Interview Questions -Complex Algorithms](https://onlinecourses.ooo/coupon/coding-interview-questions-complex-algorithms/)

- `https://www.facebook.com/groups/205747229871444/?multi_permalinks=448548762257955%2C448402448939253%2C448350662277765&notif_id=1526062221712084&notif_t=group_activity&ref=notif`

- [Express.js Node.js & MongoDB](https://onlinecourses.ooo/coupon/express-js-node-js-mongodb/)

- [ZayTuts | The Complete NodeJS Course: Build a Full Business Rating App](https://zaytuts.com/course/the-complete-nodejs-course-build-a-full-business-rating-app/?utm_source=SocialAutoPoster&utm_medium=Social&utm_campaign=Facebook)
