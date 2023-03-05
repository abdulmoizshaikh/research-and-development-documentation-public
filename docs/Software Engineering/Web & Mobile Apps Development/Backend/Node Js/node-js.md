# Node JS

**How to generate pdf using nodejs?**

You can use ejs to generate pdf in nodejs

https://ejs.co/ (Retailo consumer app using ejs to generate pdf using nodejs backend.)

**How to set columns in database table for translation in multiple languages ?**

**Database Internationalization(I18N)/Localization(L10N) design patterns 🌐**
https://medium.com/walkin/database-internationalization-i18n-localization-l10n-design-patterns-94ff372375c6

**What is a monolithic database?**

A monolithic application is built as a single unit. Enterprise applications are built in three parts: A database — consisting of many tables usually in a relational database management system. A client-side user interface — consisting of HTML pages and/or JavaScript running in a browser)

**Which database is good to social media app sql or nosql and why?**

Scalability. ... In contrast, NoSQL databases are horizontally scalable, which means that they can handle increased traffic simply by adding more servers to the database. NoSQL databases have the ability to become larger and much more powerful, making them the preferred choice for large or constantly evolving data sets.05-Mar-2018

OR

Most SQL databases are vertically scalable, which means that you can increase the load on a single server by increasing components like RAM, SSD, or CPU. In contrast, NoSQL databases are horizontally scalable, which means that they can handle increased traffic simply by adding more servers to the database.05-Mar-2018

NoSQL is a perfect solution when designing social network apps. Probably developing your social network with MySQL may be easier at start, but later, when the app grows and the number of users grows too you will have to think how to manage a MySQL cluster, dealing with master-slave configs, etc.08-Dec-2010

https://stackoverflow.com/questions/4386949/is-nosql-is-suitable-for-social-networking-kind-of-applications#:~:text=NoSQL%20is%20a%20perfect%20solution,master%2Dslave%20configs%2C%20etc.

**Why Amazon, Google, Netflix and Facebook Switched to NoSQL?**

https://www.linkedin.com/pulse/why-amazon-google-netflix-facebook-switched-nosql-shannon-block-cfe

**What Database Does Facebook Use?**
If you need a quick answer here it is:

MySQL is the primary database used by Facebook for storing all the social data. It started with the InnoDB MySQL database engine & then wrote MyRocksDB, which was eventually used as the MySQL Database engine.
https://www.scaleyourapp.com/what-database-does-facebook-use-a-1000-feet-deep-dive/

Many APIs, public or not, return JSON data that has deeply nested objects. Using data in this kind of structure is often very difficult for JavaScript applications, especially those using Flux or Redux.

https://www.npmjs.com/package/normalizr

searching in node by using minimal key values rather than full name pending we use 0/1 for boolean values of status values to making searching fast and occupy less memory

### NPM

**How to install old version of npm package in react native?**

Use npm install [package-name]@[version-number] to install an older version of a package. Prefix a version number with a caret (^) or a tilde (~) to specify to install the latest minor or patch version, respectively.17-Feb-2021
Using NPM To Install A Specific Version Of A Node.js Package

https://www.whitesourcesoftware.com › blog › npm-instal…

E.g
npm i react-native-contacts@6.0.5
Version no your can get from repo release section

## async module node

Async is a utility module which provides straight-forward, powerful functions for working with asynchronous JavaScript. Although originally designed for use with Node.js and installable via npm i async, it can also be used directly in the browser. A ESM/MJS version is included in the main async package that should automatically be used with compatible bundlers such as Webpack and Rollup.

https://www.npmjs.com/package/async

## ngrok

https://ngrok.com/download

```bash showLineNumbers
sudo tar xvzf ~/Downloads/ngrok-v3-stable-linux-amd64.tgz -C /usr/local/bin
```

```bash showLineNumbers
ngrok config add-authtoken 2F1Xcj2BwUOCiIVFJoSKBQbY2uj_YKLppABXdxjtq2PfCjW7
```

https://dashboard.ngrok.com/get-started/setup

Start a tunnel

```bash showLineNumbers
$ ngrok http 80
```

**How to generate pdf using nodejs**

You can use ejs to generate pdf in nodejs

https://ejs.co/

Retailo consumer app using ejs to generate pdf using nodejs backend.

**What is WebRTC?**

WebRTC (Web Real-Time Communication) is an API defined by the World Wide Web Consortium (W3C) to support browser-to-browser applications like voice calling, video chat, and P2P file sharing without the need for browser plugins.

### NODE JS

**How to set columns in database table for translation in multiple languages ?**

**Database Internationalization(I18N)/Localization(L10N) design patterns** 🌐

https://medium.com/walkin/database-internationalization-i18n-localization-l10n-design-patterns-94ff372375c6

**What is a monolithic database?**

A monolithic application is built as a single unit. Enterprise applications are built in three parts: A database — consisting of many tables usually in a relational database management system. A client-side user interface — consisting of HTML pages and/or JavaScript running in a browser)

**Which database is good to social media app sql or nosql and why?**

Scalability. ... In contrast, NoSQL databases are horizontally scalable, which means that they can handle increased traffic simply by `adding more servers to the database.` NoSQL databases have the ability to become larger and much more powerful, making them the preferred choice for large or constantly evolving data sets.05-Mar-2018

OR

Most SQL databases are vertically scalable, which means that you can increase the load on a single server by increasing components like RAM, SSD, or CPU. In contrast, NoSQL databases are horizontally scalable, which means that they can handle increased traffic simply by adding more servers to the database.05-Mar-2018

NoSQL is a perfect solution when designing social network apps. Probably developing your social network with MySQL may be easier at start, but later, when the app grows and the number of users grows too you will have to think how to manage a MySQL cluster, dealing with master-slave configs, etc.08-Dec-2010

https://stackoverflow.com/questions/4386949/is-nosql-is-suitable-for-social-networking-kind-of-applications#:~:text=NoSQL%20is%20a%20perfect%20solution,master%2Dslave%20configs%2C%20etc.

Why Amazon, Google, Netflix and Facebook Switched to NoSQL?

https://www.linkedin.com/pulse/why-amazon-google-netflix-facebook-switched-nosql-shannon-block-cfe

**1. What Database Does Facebook Use?**

If you need a quick answer here it is:

MySQL is the primary database used by Facebook for storing all the social data. It started with the InnoDB MySQL database engine & then wrote MyRocksDB, which was eventually used as the MySQL Database engine.

https://www.scaleyourapp.com/what-database-does-facebook-use-a-1000-feet-deep-dive/

Motivation

Many APIs, public or not, return JSON data that has deeply nested objects. Using data in this kind of structure is often very difficult for JavaScript applications, especially those using Flux or Redux.
https://www.npmjs.com/package/normalizr

searching in node by using minimal key values rather than full name pending we use 0/1 for boolean values of status values to making searching fast and occupy less memory

#### Heroku Learning

**Heroku devDependencies error resolved**

https://stackoverflow.com/questions/41797939/error-cannot-find-module-webpack-when-deploying-to-heroku/41799731?noredirect=1

**How to add delay in node api response**

#### Sleep in NodeJS

```jsx showLineNumbers
const { execSync } = require("child_process");

execSync("sleep 1"); // this will add 1 second in your response time
```

https://masteringjs.io/tutorials/node/sleep

**refresh token**

when a token expire then an api call request a server with some refresh token and grant type in body to request refresh token and update the token automatically in client local storage
this work done in background so client wont be logout when token expire and dont have to login again and again this will make good UX

**how to create a refresh token api**

How to use optional chaining in Node.js 12
node support optional chaining from version 14

https://stackoverflow.com/questions/59574047/how-to-use-optional-chaining-in-node-js-12

**Refresh token example: refToken eg**

```jsx showLineNumbers
import axios from "axios";
import errorMapper from "./middlewareConnect/errorMapper";
import { BASE_URL } from "./urls";

export const CONTENT_TYPE = {
  JSON: "application/json",
  MULTIPART: "multipart/form-data",
};

export default class API {
  constructor(
    baseURL,
    token,
    config = {
      headers: { contentType: CONTENT_TYPE.json },
    },
    tokenType = "Bearer"
  ) {
    this.config = {};
    this.instance = null;
    this.baseURL = baseURL;

    const accessToken = localStorage.getItem("access_token");

    this.config = {
      baseURL: this.baseURL || BASE_URL,
      headers: {
        // spaceId: 'aurora-default',
        "Content-Type": config?.headers?.contentType
          ? config.headers.contentType
          : CONTENT_TYPE.json,
      },
      timeout: 20000,
    };

    if (token) {
      this.config.headers.Authorization = `${tokenType} ${token}`;
      this.tokenType = "Bearer";
    } else if (accessToken) {
      this.config.headers.Authorization = `Bearer ${accessToken}`;
    }
    this.instance = axios.create(this.config);
    this.instance.interceptors.response.use(
      (response) => {
        if (response.status === 200 || response.status === 206) {
          return response.data;
        }
        throw errorMapper(response);
      },
      (error) => {
        const originalRequest = error.config;
        const refreshToken = localStorage.getItem("refresh_token");
        if (error.response?.status === 401 && refreshToken === null) {
          throw errorMapper(error);
        } else if (error.response?.status === 401 && refreshToken != null) {
          const bodyFormData = new FormData();
          bodyFormData.append("grant_type", "refresh_token");
          bodyFormData.append(
            "refresh_token",
            localStorage.getItem("refresh_token")
          );
          const tokenBasic = Buffer.from(
            `my-client:my-secret`,
            "utf8"
          ).toString("base64");

          return axios
            .post(
              "https://gateway-dev-new.dari.ae/authentication-service/oauth/token",
              bodyFormData,
              {
                headers: {
                  "Content-Type": "application/json",
                  Authorization: "Basic " + tokenBasic,
                },
              }
            )
            .then((res) => {
              console.log("new access_token res", res);
              localStorage.setItem("access_token", res.data.access_token);
              localStorage.setItem("refresh_token", res.data.refresh_token);
              axios.defaults.headers.common.Authorization =
                "Bearer " + res.data.access_token;
              originalRequest.headers.Authorization =
                "Bearer " + res.data.access_token;
              return axios(originalRequest);
            });
        } else {
          throw errorMapper(error);
        }
      }
    );
  }

  get(url, id, params) {
    let endpoint = url;
    if (id) {
      endpoint += `/${id}`;
    }
    return this.instance.get(endpoint, { params });
  }

  post(url, body, params) {
    return this.instance.post(url, body, { params });
  }

  delete(url, id) {
    return this.instance.delete(`${url}/${id}`);
  }

  put(url, body, id) {
    let endpoint = url;
    if (id) {
      endpoint += `/${id}`;
    }
    return this.instance.put(endpoint, body);
  }

  patch(url, body) {
    return this.instance.patch(url, body);
  }
}
```

## Send Email in nodejs

## Amazon SES

Get reliable, scalable email to communicate with customers at the lowest industry prices

Amazon SES pricing

Amazon Simple Email Service (SES) is a pay-as-you-go service based on the volume of emails sent and received. There are no subscriptions, no contract negotiations, and no minimum charges.

https://aws.amazon.com/ses/

### Send grid

getting nodemailer api key using sendgrid signup free plan 100emails/day forever

Create a sender identity

Before sending email, you’ll need to create a sender identity. There are two ways to do this, but we recommend creating a Single Sender to get set up quickly and test your email integration.

https://app.sendgrid.com/guide

Authenticate a domain instead

Your sender identity is the “from” email address your recipients will see in their inbox. Learn more about this.

Creating a single sender is recommend

now create a single sender

https://app.sendgrid.com/settings/sender_auth/senders

API Keys

Your application, mail client, or website can all use API (Application Programming Interface) keys to authenticate access to SendGrid services. They are the preferred alternative to using a username and password because you can revoke an API key at any time without having to change your username and password. We suggest that you use API keys for connecting to all of SendGrid’s services.

https://sendgrid.com/docs/ui/account-and-settings/api-keys/

send grid api key

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

https://app.sendgrid.com/settings/api_keys

useful

https://sendgrid.com/blog/sending-email-nodemailer-sendgrid/
https://github.com/nodemailer/nodemailer-sendgrid
https://stackoverflow.com/questions/34811307/nodemailer-sendgrid-with-apikey

from email address should be verify before sending an email

other ref not impsend grid

https://www.youtube.com/watch?v=zrXOjWICmGw&ab_channel=LearnCode.academy
https://blog.logrocket.com/how-to-send-emails-with-node-js-using-sendgrid/

```jsx showLineNumbers
var sgTransport = require("nodemailer-sendgrid-transport");

// const transporter = nodemailer.createTransport(smtpTransport(email.smtp));
const transporter = nodemailer.createTransport(
  sgTransport({ auth: email.smtp.auth })
);

const sendEmail = (mailOptions) => {
  console.log("email.smtp in node modules", email.smtp);
  if (mailOptions.template) {
    if (!mailOptions.templateValues) {
      throw Error(
        "values for template are not provided. Please add template values in `templateValues` object"
      );
    }
    const { template, templateValues } = mailOptions;
    const compiledTemplate = Handlebars.compile(template);
    mailOptions.html = compiledTemplate(templateValues);
  }
  return transporter.sendMail(mailOptions);
};
```

### mandrill

```jsx showLineNumbers
var mandrillTransport = require("nodemailer-mandrill-transport");

/*
*  send mail through mandrill
* Configuring mandrill transport.
* Copy your API key here.
*/
sendMail(subject, to_email, message, callback) {
var smtpTransport = nodemailer.createTransport(
mandrillTransport({
auth: {
apiKey: constant.mandrill_api_key,
},
})
);

// Put in email details.

let mailOptions = {
from: constant.from_email,
to: to_email,
subject: subject,
html: message,
};

// Sending email.
smtpTransport.sendMail(mailOptions, function (error, response) {
if (error) {
// throw new Error("Error in sending email");
console.log("error in sendMail", error);
callback(error, []);
}
console.log("Message sent: " + JSON.stringify(response));
callback("", response);
});
}
```

### gmail-smtp

using gmail

https://dev.to/chandrapantachhetri/sending-emails-securely-using-node-js-nodemailer-smtp-gmail-and-oauth2-g3a

reference

https://www.google.com/search?q=gmail+transport+nodemailder&oq=gmail+transport+nodemailder&aqs=chrome..69i57j0i8i13i30.5807j0j7&sourceid=chrome&ie=UTF-8
https://nodemailer.com/usage/using-gmail/
https://stackoverflow.com/questions/19877246/nodemailer-with-gmail-and-nodejs

## nodejs advance topics

- Serverless architecture https://docs.google.com/document/d/1RHjSdMuTIBFqanALneIOtsfXyr8CRNyNgDqlVoqAcuY/edit
- microservices in nodejs https://docs.google.com/document/d/1OQpfkOZPXXRdpMiOgnkdrBClSUIyu_v_9j7kiC8P_iU/edit

- [socket.io](http://socket.io/) in nodejs https://docs.google.com/document/d/1MF84L-6cXtqOZ1xx9T0N1_qdbAZZbfLD8sKoiwPu9io/edit

- nodejs fixes https://docs.google.com/document/d/1Ul_NJ5p2In6K1808W7rgiQ6IDG6AVtDo9dFA3E0w5sE/edit

- nodejs libraries comparision https://github.com/fastify/fastify

- clousures in javascript
  [A closure is a function having access to the parent scope, even after the parent function has closed.](https://www.w3schools.com/js/js_function_closures.asp)

## validation

params validation in nodejs

useful lib for params validation in nodejs , weekly downloads

1. joi
   https://www.npmjs.com/package/joi

   3,401,741 https://joi.dev/api/?v=17.4.0

2. ajv
   https://www.npmjs.com/package/ajv

   46,396,407 https://ajv.js.org/

3. express-validator
   https://www.npmjs.com/package/express-validator

   288,049 https://express-validator.github.io/docs/

references

https://ranvir.xyz/blog/how-to-write-a-request-parameter-validation-middleware-in-node.js/

## Load testing

`import data from csv in nodejs login API`

https://www.youtube.com/watch?v=aEJNc3TW-g8&ab_channel=JMeterTutorial

**Tools used for load testing in nodejs**

- Jmeter
- NewRelic

## debugging in nodejs

**This solution will surely work 100% experimented and tested**

[nodejs debugging guide](./Nodejs%20Debugging%20guide/nodejs-debugging-guide.md) this will guide you from start to end recommend method

RND of debugging and IDE in nodejs

installed atom, webstrome,

try debugging in all installed IDE's

not an best IDE for nodejs development

sublime text

https://stackoverflow.com/questions/24758683/can-i-debug-node-js-applications-in-sublime-2
brackets

atom is also worst for debugging in nodejs we have to install third party packaged for debugging feature in atom which is not updating on daily progress etc

because I have tried to debug nodejs code in atom its not even start and give me error

tried this https://medium.com/javascript-tales/debugging-nodejs-with-atom-editor-baa56f7146ee
https://github.com/willyelm/xatom-debug/issues/24

that was reported May 19, 2017 3 years ago but not resolved till 2021

Best complete full bound IDE for debug nodejs Code is Webstorm recommended

and completed development IDE is vs code recommended

## Bookmarks

### AchieveON

### Paypal Integration in nodejs

- [paypal1.png](https://www.nodejsera.com/assets/img/paypal1.png)

- [Paypal integration using node.js | part 1 | node.js | nodejsera](https://www.nodejsera.com/paypal-payment-integration-using-nodejs-part1.html)

- [paypal-rest-sdk](https://www.npmjs.com/package/paypal-rest-sdk)

- [PayPal REST SDKs - PayPal Developer](https://developer.paypal.com/docs/api/rest-sdks/)

- [PayPal REST SDK with Node.js](https://github.com/bradtraversy/node_paypal_sdk_sample)

- [Intro To The Node.js PayPal REST SDK](https://www.youtube.com/watch?v=7k03jobKGXM)

- [node_paypal_sdk_sample/app.js at master · bradtraversy/node_paypal_sdk_sample](https://github.com/bradtraversy/node_paypal_sdk_sample/blob/master/app.js)

- [GitHub - MattFoley/react-native-paypal: Paypal wrapper for React Native](https://github.com/MattFoley/react-native-paypal)

- [Set up Stripe in React Native + NodeJS](https://blog.bam.tech/developer-news/setup-stripe-react-native-nodejs)

- [Integrating Paypal in your React Native App - Part 2 | Coding the React Native App](https://www.youtube.com/watch?v=40a0qbgAkmk)

### repositories

- [apeiron3 / pay — Bitbucket](https://bitbucket.org/apeiron3/pay/src/master/)

### AON-issues-RND

### database not connecting

- [php - connect to PostgreSQL server: FATAL: no pg_hba.conf entry for host -](https://dba.stackexchange.com/questions/83984/connect-to-postgresql-server-fatal-no-pg-hba-conf-entry-for-host)

- [perl - no pg_hba.conf entry for host](https://stackoverflow.com/questions/1406025/no-pg-hba-conf-entry-for-host)

- [How To Install and Use PostgreSQL on Ubuntu 18.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04)

- [Ignore invalid self-signed ssl certificate in node.js with https.request? -](https://stackoverflow.com/questions/10888610/ignore-invalid-self-signed-ssl-certificate-in-node-js-with-https-request)

- [Stack Can't use SSL with Postgres · Issue #956 · sequelize/sequelize](https://github.com/sequelize/sequelize/issues/956)

- [Creating user, database and adding access on PostgreSQL | by Arnav Gupta |](https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e)

- [Install pgAdmin 4 on Ubuntu 20.04/18.04/16.04 | ComputingForGeeks](https://computingforgeeks.com/how-to-install-pgadmin-4-on-ubuntu/)

- [How to Install PostgreSQL and pgAdmin4 in Ubuntu 20.04](https://www.tecmint.com/install-postgresql-and-pgadmin-in-ubuntu/)

- [AON : WBS - Google Sheets](https://docs.google.com/spreadsheets/d/1tWYlhAMGRDcUZW3BUekAYdZAcQ7UR8aNI0GDMPhDtbY/edit#gid=568898991)

- [InVision](https://projects.invisionapp.com/)

- [API Requirements - Google Sheets](https://docs.google.com/spreadsheets/d/1j7YEaAasxTfJNTHQffd7CazZLeXjcXbP6FyUOMkJVgM/edit#gid=1603225692)

- [Stripe API Reference - List all charges](https://stripe.com/docs/api/charges/list)

- [AchieveOn-App - Zeplin](https://app.zeplin.io/project/5c939fb2ebdbb566f1ea8cce/dashboard?q=payment)

- [Stripe payments integration with NodeJS | by Vishnu | Medium](https://medium.com/@vishnuit18/stripe-payments-integration-with-nodejs-13f6a5b21c23)

- [Stripe fee calculation](https://stackoverflow.com/questions/36907341/stripe-fee-calculation)

- [direct_charges](https://stripe.com/img/docs/connect/direct_charges.svg)

- [Creating direct charges](https://stripe.com/docs/connect/direct-charges#collecting-fees)

- [direct charges and Checkout](https://github.com/stripe-samples/connect-direct-charge-checkout)

- [connect-direct-charge-checkout/server.js at master ·](https://github.com/stripe-samples/connect-direct-charge-checkout/blob/master/server/node/server.js)

1. [What is stripe payment?](https://www.youtube.com/watch?v=1vpwfDDyINk&list=PLyzY2l387AlMy6r_JhflipKqKrhVK17gP)

- [Connecting | node-postgres](https://node-postgres.com/features/connecting)

- [pgAdmin 4 Getting Started - Sequelize | The Node.js / io.js ORM for PostgreSQL, MySQL,](http://127.0.0.1:42169/browser/#)

- [SQLite and MSSQL](https://sequelize.org/v3/docs/getting-started/)

- [Stripe Connect account id, customer id security issues](https://stackoverflow.com/questions/44503552/stripe-connect-account-id-customer-id-security-issues)

- [Is it dangerous to store in my database stripe customers ids?](https://stackoverflow.com/questions/41576896/is-it-dangerous-to-store-in-my-database-stripe-customers-ids)

### RND image upload

- [UsingAWS S3 To Store And Upload files In Node JS | Amazon Web Services](https://www.agiratech.com/blog/using-aws-s3-to-store-and-upload-files-in-node-js)

- [node.js - Simple file upload to S3 using aws-sdk and Node/Express](https://stackoverflow.com/questions/17930204/simple-file-upload-to-s3-using-aws-sdk-and-node-express)

- [What is the best way to upload images when using Node.js S3 or any image](https://www.quora.com/What-is-the-best-way-to-upload-images-when-using-Node-js-S3-or-any-image-hosting-solution)

- [Uploading files to AWS S3 using Nodejs](https://www.zeolearn.com/magazine/uploading-files-to-aws-s3-using-nodejs)

- [node.js - good practice to upload file to s3 using nodejs scalability and](https://stackoverflow.com/questions/58021874/good-practice-to-upload-file-to-s3-using-nodejs-scalability-and-perfomance-shoul)

### SELF DEVELOPMENT RND SITES

- [GitHub - goldbergyoni/nodebestpractices: The Node.js best practices list October 2020](https://github.com/goldbergyoni/nodebestpractices)

- [Node.js & JavaScript Testing Best Practices](https://medium.com/@me_37286/yoni-goldberg-javascript-nodejs-testing-best-practices-2b98924c9347)

- [node.js - How to mock mysql database?](https://stackoverflow.com/questions/57622027/how-to-mock-mysql-database)

- [REST Resource Naming Guide - REST API Tutorial](https://restfulapi.net/resource-naming/)

- [node.js - Automatically start forever on system restart](https://stackoverflow.com/questions/13385029/automatically-start-forever-node-on-system-restart)

### RND

- [GitHub - yug95/node-mysql: Node with mysql boilerplate](https://artillery.io/)
- [Artillery - a modern load testing toolkit](https://github.com/yug95/node-mysql)

- [Swagger Documentation](https://swagger.io/docs/)

- [Node Js With MySQL BoilerPlate for Rest API Creation | by Yogesh Agrawal](https://medium.com/@yugagrawal95/hello-everybody-who-is-new-to-rest-api-and-how-to-create-it-c0e0f8db4d97)

- [Express morgan middleware](http://expressjs.com/en/resources/middleware/morgan.html)

### socialsignin to server

- [Protect REST API after social login with Node.js and Express.js](https://medium.com/@spyna/how-really-protect-your-rest-api-after-social-login-with-node-js-3617c336ebed)

### image-upload-aws

- [Access Control List Overview - Amazon Simple Storage Service](https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl)

- [multer-s3](https://www.npmjs.com/package/multer-s3)
- [multer](https://www.npmjs.com/package/multer)
- [aws-sdk](https://www.npmjs.com/package/aws-sdk)

- [How to set up simple image upload with Node and AWS S3](https://www.freecodecamp.org/news/how-to-set-up-simple-image-upload-with-node-and-aws-s3-84e609248792/)

- [Manual | Sequelize](https://sequelize.org/master/manual/model-basics.html#data-types)

### validation

- [GitHub - skaterdav85/validatorjs: A data validation library in JavaScript for the browser and Node.js, inspired by Laravel's Validator.](https://github.com/skaterdav85/validatorjs#readme)

- [We’re under attack! 23+ Node.js security best practices | by Node.js Best](https://medium.com/@nodepractices/were-under-attack-23-node-js-security-best-practices-e33c146cb87d)

- [How To Implement API Authentication with JSON Web Tokens and Passport |](https://www.digitalocean.com/community/tutorials/api-authentication-with-json-web-tokensjwt-and-passport)

### RND

### multilingual

- [Node.js Tutorial on Creating a Multilingual Web App | by Phrase | i18n and](https://medium.com/i18n-and-l10n-resources-for-developers/node-js-tutorial-on-creating-a-multilingual-web-app-df24d8471482)

- [GitHub - noveogroup-amorgunov/localizify: Easy localize your messages](https://github.com/noveogroup-amorgunov/localizify)

- [GitHub - mashpie/i18n-node: Lightweight simple translation module for node.js](https://github.com/mashpie/i18n-node)

- [GitHub - DanielBaulig/node-gettext: An adaption of Joshua I. Miller's Javascript Gettext library for node.js.](https://github.com/DanielBaulig/node-gettext)

- [node.js - Multilanguage express app](https://stackoverflow.com/questions/10866778/multilanguage-express-app)

- [Node.js i18n and Express.js localization - Lokalise Blog](https://lokalise.com/blog/node-js-i18nexpress-js-localization/)

- [Testing Node.js in 2018 | Hacker Noon](https://hackernoon.com/testing-node-js-in-2018-10a04dd77391)

- [How To Unit Test RESTful API With Mocha & Mock MongoDB | JavaScript](https://www.youtube.com/watch?v=7VNgjfmv_fE&ab_channel=CodeWithKris)

- [Front end API's Signatures ](https://docs.google.com/document/d/147IZCNNc5ej0BeSOnJzTm9RXk0t0J-5sE2Uxm6J7QfA/edit)

### logout

- [node.js - How to destroy JWT Tokens on logout?](https://stackoverflow.com/questions/37959945/how-to-destroy-jwt-tokens-on-logout)

- [node.js - logout using express and passport](https://stackoverflow.com/questions/55193862/logout-using-express-and-passport)

- [How to log out when using JWT. One does not simply log out when using… | by](https://medium.com/devgorilla/how-to-log-out-when-using-jwt-a8c7823e8a6#:~:text=As%20already%20said%2C%20you%20cannot,Or%2C%20unless%2C%20you%20can%E2%80%A6)

- [expire jwt token mannualy - Google Search](https://www.google.com/search?q=expire+jwt+token+mannualy&oq=expire+jwt+token+mannualy&aqs=chrome..69i57j0i13i457j0i13l3j0i13i30l2.7890j1j1&sourceid=chrome&ie=UTF-8)

- [jwt.expire token - Google Search](https://www.google.com/search?q=jwt.expire+token&oq=jwt.expire+token&aqs=chrome..69i57j0i457j0j0i30l5.5239j0j1&sourceid=chrome&ie=UTF-8)

- [do we need to store JWT token in db - Google Search](https://www.google.com/search?q=do+we+need+to+store+JWT+token+in+db&oq=do+we+need+to+store+JWT+token+in+db&aqs=chrome..69i57j69i64.8860j1j1&sourceid=chrome&ie=UTF-8)

- [passport-linkedin](http://www.passportjs.org/packages/passport-linkedin/)

### social register

- [Package - passport-linkedin-token-oauth2](https://developer.aliyun.com/mirror/npm/package/passport-linkedin-token-oauth2)

- [passport.authenticate linkedin-token](<https://www.google.com/search?q=passport.authenticate(%27linkedin-token%27)&oq=passport.authenticate(%27linkedin-token%27)&aqs=chrome..69i57.14376j0j1&sourceid=chrome&ie=UTF-8>)

- [passport-linkedin-token-v2](https://www.npmjs.com/package/passport-linkedin-token-v2)

- [with Facebook access tokens using the OAuth 2.0 API.](https://github.com/drudge/passport-facebook-token)

- [express - Local and social authorization with node.js on mobile app](https://stackoverflow.com/questions/20094710/local-and-social-authorization-with-node-js-on-mobile-app)

- [express-passport-facebook-token-example/server.js at master ·](https://github.com/philipbrack/express-passport-facebook-token-example/blob/master/server.js)

- [GitHub - philipbrack/express-passport-facebook-token-example-client:](https://github.com/philipbrack/express-passport-facebook-token-example-client)

- [node.js - Passportjs Facebook login flow passport-facebook vs passport-token](https://stackoverflow.com/questions/35065226/passportjs-facebook-login-flow-passport-facebook-vs-passport-token)

- [Stack OAuth 2.0 Client Credentials Flow | LinkedIn Developer Network](https://developer.linkedin.com/docs/v2/oauth2-client-credentials-flow)

- [How can I verify a LinkedIn access token?](https://stackoverflow.com/questions/37115035/how-can-i-verify-a-linkedin-access-token)

- [Authorization Code Flow - LinkedIn | Microsoft Docs](https://docs.microsoft.com/en-us/linkedin/shared/authentication/authorization-code-flow)

- [Profile API - LinkedIn | Microsoft Docs](https://docs.microsoft.com/en-us/linkedin/shared/integrations/people/profile-api)

- [Search | Microsoft Docs](https://docs.microsoft.com/en-us/search/?terms=user%20profile&scope=LinkedIn)

- [passport-facebook-token](https://www.npmjs.com/package/passport-facebook-token)

- [Manually Build a Login Flow - Facebook Login](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow)

- [node.js - Can I use the passport-google callback to authenticate android/ios](https://stackoverflow.com/questions/35107090/can-i-use-the-passport-google-callback-to-authenticate-android-ios-users)

- [Client Credential Flow - LinkedIn | Microsoft Docs](https://docs.microsoft.com/en-us/linkedin/shared/authentication/client-credentials-flow?context=linkedin/context)

- [Developers | Linkedin](https://www.linkedin.com/developers/)

- [How to Get a LinkedIn API Access Token | by Esther Liao | Medium](https://medium.com/@esther.liao/how-to-get-a-linkedin-access-token-a53f9b62f0ce)

### Nodejs with SQL

- [Access SQL Server in Node.js](https://www.tutorialsteacher.com/nodejs/access-sql-server-in-nodejs)

- https://www.w3schools.com/nodejs/nodejs_mysql.asp
- [Node.js MySQL](https://www.npmjs.com/package/mssql)
- [Using MySQL With Node.js](https://www.youtube.com/watch?v=EN6Dx22cPRI)
- [What do you think of Node.js drivers for MS SQL and MySQL ? - Hashnode](https://hashnode.com/post/what-do-you-think-of-nodejs-drivers-for-ms-sql-and-mysql-ciiimgyo700t3lc5386f01n7d)

- [MySQL :: MySQL 8.0 Reference Manual :: 2.5.5 Installing MySQL on Linux Using](https://dev.mysql.com/doc/refman/8.0/en/linux-installation-debian.html)

- [hapi](https://www.npmjs.com/package/hapi)

- [AdonisJs - Node.js web framework](https://adonisjs.com/)
