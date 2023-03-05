# NestJS

## NestJs and typescript concepts:

**Learn Nest.js from Scratch by building an API :**
https://www.youtube.com/watch?v=F_oOtaxb0L8&list=WL&index=22&ab_channel=AndyVanSlaars

**Nest.js with MongoDB - Complete Example**
https://www.youtube.com/watch?v=ulfU5vY6I78&ab_channel=Academind

**Type inference:**

Typescript has a feature which is called type inference which will automatically detect the return type a function based on its return statement written in code if no return statement in function then the type will be void: by this user haven't add manually add return type to function in parameter typescript do this for you automatically

which means its actually able to infer that you're returning a string beacuse you have a return statement here and there well you return a string

https://youtu.be/F_oOtaxb0L8?t=2338

**Modules** are used to bundle your controllers and services so then services can be injected in controllers and modules are then imported in root module using imports:[] in app module or its parent module to work

you need tie your feature togather using modules otherwise your app wont work

```javascript

// product model / schema
export class Product {
  //   long cut
  //   id: string;
  //   title: string;
  //   description: string;
  //   price: number;
  //   constructor(id: string, title: string, description: string, price: number) {
  //     this.id = id;
  //     this.title = title;
  //     this.description = description;
  //     this.price = price;
  //   }

  //   shortcut for above code in typescript by just add access modifier before params name
  constructor(
    public id: string,
    public title: string,
    public description: string,
    public price: number,
  ) {}
}

```

**string** -> this is a typescript type (used in type of params in function let say)

**String** -> this is a Javascript type (used in mongoose models let say)

same goes for other types like number in ts and Number in JS (in js first letter is capital)

**NestJS - How to use .env variables in main app module file for database connection**

Solution: (**recommended**)

**Keeping using ConfigModule**

You need to set `NODE_ENV` in npm scripts so that it can be used to load an env file based on the env.

```json showLineNumbers
"scripts": {
  "start:local": "NODE_ENV=local npm run start"
  "start:dev": "NODE_ENV=dev npm run start"
}
```

Now you can just use the `ConfigModule`:

```js showLineNumbers

@Module({
  imports: [
    ConfigModule.forRoot({ envFilePath: `${process.env.NODE_ENV}.env` }),
MongooseModule.forRoot(`mongodb+srv://${process.env.DB_USER}:${process.env.DB_PASS}@myhost.net?retryWrites=true&w=majority&db=dbname`, { useNewUrlParser: true, dbName: 'dbname' })
    ...
})
```

**2. Using `dotenv`**

```bash showLineNumbers
npm install dotenv
```

Add some scripts to your `package.json` to set what env you are in.

```json showLineNumbers
"scripts": {
  ...
  "start:local": "NODE_ENV=local npm run start"
  "start:dev": "NODE_ENV=dev npm run start"
}
```

Import `dotenv` in `main.ts` file. Make sure you do it at the top of the file.

```js showLineNumbers
require("dotenv").config({ path: `../${process.env.NODE_ENV}.env` });
```

**3. Using `env-cmd`**

You can use `env-cmd` npm package.

```bash showLineNumbers
npm install env-cmd
```

And add some commands for different envs in `package.json`, for example:

```json showLineNumbers
"scripts": {
  ...
  "start:local": "env-cmd -f local.env npm run start"
  "start:dev": "env-cmd -f dev.env npm run start"
}
...
```

---

Now you can use the env variables, for example:

```js showLineNumbers
MongooseModule.forRoot(
  `mongodb+srv://${process.env.DB_USER}:${process.env.DB_PASS}@myhost.net?retryWrites=true&w=majority&db=dbname`,
  { useNewUrlParser: true, dbName: "dbname" }
);
process.env.MONGO_CONNECTION_STRING;
```

**Update:**

To overcome the env set command problem in different platforms, you can install `cross-env` package.

```js showLineNumbers

npm install -D cross-env
```

And update the scripts:

```js showLineNumbers

"scripts": {
  "start:local": "cross-env NODE_ENV=local npm run start"
  "start:dev": "cross-env NODE_ENV=dev npm run start"
}
```

https://stackoverflow.com/questions/63285055/nestjs-how-to-use-env-variables-in-main-app-module-file-for-database-connecti

### **Dependency Injection**

multiple instances creation ko avoid krne liye dependency injection use krte hain is se sirf aik instance banta hy class main or usko multiple times use kr skte hain

benefis of using typscript in your projects is that you will be femilier with other languages code as well like

c#, java, swift etc

## learn nest js from your hisab app backend developed using nestjs and nodejs.

## Logging request/response in Nest.js

log req/res in nestjs server

https://github.com/winstonjs/winston#motivation

https://www.npmjs.com/package/nest-winston

https://stackoverflow.com/questions/55093055/logging-request-response-in-nest-js

```jsx showLineNumbers
providers;
Injectable;
```

https://docs.nestjs.com/providers

## dto in nestjs stand for?

But first (if you use TypeScript), we need to determine the DTO (**Data Transfer Object**) schema. A DTO is an object that defines how the data will be sent over the network.

Why DTO is used in NestJS?

DTO is used **in order to validate incoming requests**. The DTO on its own is more of a guideline for the developer and those who consume the API to know what kind of shape the request body expects to be, it doesn't actually run any validations on its own!!!.

### making docket container for nestjs

https://nodejs.org/en/docs/guides/nodejs-docker-webapp/

## Debugging NestJS in VSCode

[Debugging NestJS in VSCode ](<https://javascript.plainenglish.io/debugging-nestjs-in-vscode-d474a088c63b#:~:text=Then%2C%20navigate%20to%20the%20debug,the%20keyboard%20shortcut%20(F5).>)(Recommended):

[Debugging nest.js application with vscode](https://stackoverflow.com/questions/49504765/debugging-nest-js-application-with-vscode)

Solution: worked in hefazatapi project tested and working condition

```json showLineNumbers
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "hefazatapi",
      "args": ["${workspaceFolder}/src/main.ts"],
      "runtimeArgs": [
        "--nolazy",
        "-r",
        "ts-node/register",
        "-r",
        "tsconfig-paths/register"
      ],
      "sourceMaps": true,
      "envFile": "${workspaceFolder}/.env",
      "cwd": "${workspaceRoot}",
      "console": "integratedTerminal",
      "protocol": "inspector"
    }
  ]
}
```

### [Cannot find module 'ts-node/register'](https://stackoverflow.com/questions/40910864/cannot-find-module-ts-node-register)

Solution:

```bash showLineNumbers
npm install ts-node --save-dev
```

**Customise the response on verification failure for a jwt Strategy NestJs**

custom error in JwtAuthGuard nestjs?
how to change error message in UseGuards?

Solution:

This answer is not useful
You can use the AuthGuard('jwt')'s handleRequest method to throw any exception on JWT Validation failure.

```jsx showLineNumbers
@Injectable()
export class JwtAuthGuard extends AuthGuard("jwt") {
  handleRequest(err: any, user: any, info: any, context: any, status: any) {
    if (info instanceof JsonWebTokenError) {
      throw new UnauthorizedException("Invalid Token!");
    }

    return super.handleRequest(err, user, info, context, status);
  }
}
```

JsonWebTokenError comes from jsonwebtoken library, which is used internally by passport.

> Demo in our code in Hefazat server

```jsx showLineNumbers
import { UnauthorizedException } from "@nestjs/common";
import { AuthGuard } from "@nestjs/passport";
import { JsonWebTokenError } from "jsonwebtoken";
export class JwtAuthGuard extends AuthGuard("jwt") {
  constructor() {
    super();
  }
  handleRequest(err: any, user: any, info: any, context: any, status: any) {
    if (info instanceof JsonWebTokenError) {
      throw new UnauthorizedException(
        "You are logged out ,Please login again."
      );
    }

    return super.handleRequest(err, user, info, context, status);
  }
}
```

Output:

```json showLineNumbers
{
  "statusCode": 401,
  "message": "You are logged out ,Please login again.",
  "error": "Unauthorized"
}
```

https://stackoverflow.com/questions/60042350/customise-the-response-on-verification-failure-for-a-jwt-strategy-nestjs

**@nestjs/swagger**

for swagger setup in nestjs project (have used in hefazatapi)

Documentation:

https://www.npmjs.com/package/@nestjs/swagger

https://docs.nestjs.com/openapi/introduction

> A working example is available here.

https://github.com/nestjs/nest/tree/master/sample/11-swagger

## Serialization

Serialization is a process that happens before objects are returned in a network response. This is an appropriate place to provide rules for transforming and sanitizing the data to be returned to the client. For example, sensitive data like passwords should always be excluded from the response. Or, certain properties might require additional transformation, such as sending only a subset of properties of an entity. Performing these transformations manually can be tedious and error prone, and can leave you uncertain that all cases have been covered.

### Class-transformer in nestjs

```jsx showLineNumbers
import { Exclude, Expose, Transform } from "class-transformer";
import { RoleEntity } from "./role.entity";

export class UserEntity {
  id: number;
  firstName: string;
  lastName: string;

  @Exclude()
  password: string;

  @Expose()
  get fullName(): string {
    return `${this.firstName} ${this.lastName}`;
  }

  @Transform(({ value }) => value.name)
  role: RoleEntity;

  constructor(partial: Partial<UserEntity>) {
    Object.assign(this, partial);
  }
}
```

https://docs.nestjs.com/techniques/serialization

### Interceptors in nestjs

e.g

```jsx showLineNumbers
import { Observable } from "rxjs";
import {
  ExecutionContext,
  Injectable,
  NestInterceptor,
  CallHandler,
} from "@nestjs/common";

import { UserEntity } from "../modules/user/user.entity";
import { AuthService } from "../modules/auth/auth.service";

@Injectable()
export class AuthUserInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    const request = context.switchToHttp().getRequest();

    const user: UserEntity = request.user;
    AuthService.setAuthUser(user);

    return next.handle();
  }
}
```

https://github.com/aneudysamparo/NestJS-Boilerplate/blob/master/src/interceptors/auth-user-interceptor.service.ts

### What is the --watch and --debug option in nest start

nest start vs nest start debug

```json showLineNumbers
    "start:dev": "nest start --watch",
    "start:debug": "nest start --debug --watch",
```

In general, --watch means the terminal will stay open and watch for any file changes and then reload the server. --debug means it will log more messages to the console (e.g. info or warnings), which can be helpful for debugging.

https://stackoverflow.com/questions/63967171/what-is-the-watch-and-debug-option-in-nest-start

## Middleware In NestJs

https://docs.nestjs.com/middleware#middleware

### Logger Middleware in nestjs

> **implemented in hefazatapi project**

> tags and other part of research <br/>

How can I make the HTTP request object visible to my winston logger?<br/>
morgan logger in nestjs<br/>
how to log http request with body in nestjs<br/>

```
This package has been deprecated
Author message:

Deprecated and unmaintained. Check out nestjs-pino as alternative.
```

https://www.npmjs.com/package/nest-morgan

https://www.npmjs.com/package/nestjs-pino

**Logging request/response in Nest.js**

middleware structure in nestjs

> make new folder of middleware in src/common and create logger.middleware.ts in it

```jsx showLineNumbers title="logger.middleware.ts"

import { Injectable, NestMiddleware, Logger } from '@nestjs/common';

import { Request, Response, NextFunction } from 'express';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  private readonly logger = new Logger(`HTTP`);

  use(request: Request, response: Response, next: NextFunction): void {
    const { ip, method, path: url, body } = request;
    const userAgent = request.get('user-agent') || '';

    response.on('close', () => {
      const { statusCode } = response;
      const contentLength = response.get('content-length');

      this.logger.log(`${method} ${url} ${statusCode} ${contentLength} - ${userAgent} ${ip} body: ${JSON.stringify(body)} `);
    });

    next();
  }
}

```

```jsx showLineNumbers title="app.module.ts"
import { LoggerMiddleware } from "./common/middleware/logger.middleware";

export class AppModule {
  configure(consumer: MiddlewareConsumer) {
    consumer.apply(LoggerMiddleware).forRoutes("api");
  }
}
```

OR

```jsx showLineNumbers title="app.module.ts"
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer): void {
    consumer.apply(AppLoggerMiddleware).forRoutes("*");
  }
}
```

https://docs.nestjs.com/middleware#middleware

https://stackoverflow.com/questions/55093055/logging-request-response-in-nest-js

https://docs.nestjs.com/techniques/logger#use-external-logger

## Send Emails with NestJS (worth reading article cover all things)

danish bhai followed this article to send email in hefazatapi project

https://github.com/notiz-dev/nestjs-mailer

https://notiz.dev/blog/send-emails-with-nestjs

## Amazon ses setup in nestjs project

hefazatapi

Source code:

```jsx showLineNumbers title='mail.module.ts
import { MailerModule } from "@nestjs-modules/mailer";
import { Global, Module } from "@nestjs/common";
import { MailService } from "./mail.service";
import { join } from "path";
import { HandlebarsAdapter } from "@nestjs-modules/mailer/dist/adapters/handlebars.adapter";

@Global()
@Module({
  imports: [
    MailerModule.forRoot({
      transport: {
        host: process.env.MAIL_SMTP_HOST,
        port: 465,
        secure: true,
        auth: {
          user: process.env.MAIL_USER,
          pass: process.env.MAIL_PASS,
        },
      },
      defaults: {
        from: process.env.MAIL_FROM,
      },
      template: {
        dir: join(__dirname, "templates"),
        adapter: new HandlebarsAdapter(), // or new PugAdapter() or new EjsAdapter()
        options: {
          strict: true,
        },
      },
    }),
  ],
  providers: [MailService],
  exports: [MailService],
})
export class MailModule {}
```

```jsx showLineNumbers title="mailService.ts"
import { MailerService } from '@nestjs-modules/mailer';
import { Injectable, Logger } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';
import { getSubjectFromEnviornment, setFromEmailBasedUponTemplateId } from 'src/config/util/handlers';

@Injectable()
export class MailService {
  private readonly logger = new Logger(MailService.name);

  constructor(private mailer: MailerService, private config: ConfigService) {}

  public async sendEmail(template: string, subject: string, toEmail: string, params: any, attachments: any = []) {
    try {
      const fromEmail = setFromEmailBasedUponTemplateId(template);
      const _subject = getSubjectFromEnviornment(process.env.Environment, subject);
      await this.mailer.sendMail({
        to: toEmail,
        from: fromEmail,
        subject: _subject,
        template: `${template}`,
        context: params,
        attachments: attachments,
      });
    } catch (e: any) {
      this.logger.error(`Error while sending email to ${toEmail}, ${JSON.stringify(e)}`);
    }
  }
}

```

.env

```jsx showLineNumbers title=".env"
# Amazon SES
MAIL_SMTP_HOST="email-smtp.us-east-1.amazonaws.com"
MAIL_USER="aws smtp user"
MAIL_PASS="aws smtp password"
MAIL_FROM="'No Reply' <no-reply@hefazattech.com>"
```

references:

Using the Amazon SES API to send email

https://docs.aws.amazon.com/ses/latest/dg/send-email-api.html

Using the Amazon SES SMTP interface to send email

https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html

Obtaining Amazon SES SMTP credentials

https://docs.aws.amazon.com/ses/latest/dg/smtp-credentials.html

Set up email sending with Amazon SES

https://docs.aws.amazon.com/ses/latest/dg/send-email.html

Sending emails programmatically through the Amazon SES SMTP interface

https://docs.aws.amazon.com/ses/latest/dg/send-using-smtp-programmatically.html#send-email-smtp-code-examples

Amazon SES pricing

https://aws.amazon.com/ses/pricing/

https://calculator.aws/

https://nodemailer.com/transports/

https://nodemailer.com/transports/ses/

https://www.npmjs.com/package/@aws-sdk/client-ses

https://www.npmjs.com/package/aws-sdk

```
[NestWinston] Error	2/6/2023, 5:12:52 PM Error while sending email to moiz.mustaqeem@nextgeni.com, {"code":"EMESSAGE","response":"554 Message rejected: Email address is not verified. The following identities failed the check in region US-EAST-1: moiz.mustaqeem@nextgeni.com","responseCode":554,"command":"DATA"} - {"stack":["MailService"]} +46s

```

solution:

only send mail to registered verified domain

```
[NestWinston] Error	2/6/2023, 5:21:40 PM Error while sending email to services@hefazattech.com, {"library":"SSL routines","function":"ssl3_get_record","reason":"wrong version number","code":"ESOCKET","command":"CONN"} - {"stack":["MailService"]} +21s
or
"SSL: WRONG_VERSION_NUMBER" when use AWS SES SMTP server in GCP Composer Airflow
wrong version number amazon ses
```

solution:

change port to **465**

https://stackoverflow.com/questions/68687737/ssl-wrong-version-number-when-use-aws-ses-smtp-server-in-gcp-composer-airflow

nestjs mailer with aws, amazon ses with nestjs

AWS SES transport with handlebars
#192

https://github.com/nest-modules/mailer/issues/192
