# Logger in nestjs

## API logs Logging on aws cloud watch - through nest js connector #27

```bash showLineNumbers
npm install --save  winston nest-winston winston-cloudwatch
```

```jsx showLineNumbers
import * as WinstonCloudWatch from 'winston-cloudwatch';
import {
  utilities as nestWinstonModuleUtilities,
  WinstonModule,
} from 'nest-winston';
import { format, transports } from 'winston';


async function bootstrap() {
  const app = await NestFactory.create(AppModule, {
    logger: WinstonModule.createLogger({
      format: format.uncolorize(), //Uncolorize logs as weird character encoding appears when logs are colorized in cloudwatch.
      transports: [
        // for logging logs in console
        new transports.Console({
          format: format.combine(
            format.timestamp(),
            format.ms(),
            nestWinstonModuleUtilities.format.nestLike(),
          ),
          // format: format.combine(format.timestamp(), format.json()),
        }),
        // for logging logs in file
        // new transports.File({
        //   filename: 'log',
        //   format: format.combine(
        //     format.timestamp(),
        //     format.ms(),
        //     nestWinstonModuleUtilities.format.nestLike(),
        //   ),
        // }),
        // for loggins logs in aws cloudwatch
        new WinstonCloudWatch({
          name: 'Cloudwatch Logs',
          awsRegion: 'us-east-1',
          awsOptions: {
            credentials: {
              accessKeyId: '',
              secretAccessKey: '',
            },
          },
          logGroupName: 'hefazatapi_local',
          logStreamName: 'moiz-local-server-logs',
          messageFormatter: function (item) {
            return (
              item.level + ': ' + item.message + ' ' + JSON.stringify(item.meta)
            );
          },
        }),
      ],
    }),
  });
```

references:

[nest-winston](https://github.com/gremo/nest-winston)
[Log Monitoring NestJS using Winston and Logtail](https://www.youtube.com/watch?v=QOvrper7TWA&ab_channel=AgikSetiawan)

[winston logger | Log into MongoDB | File | Console | nodejs tutorial](https://www.youtube.com/watch?v=PdVlAi7nrRU&ab_channel=TechnicalBabaji)

[winston-cloudwatch](https://github.com/lazywithclass/winston-cloudwatch)

[Log monitoring NodeJS (NestJS) dengan menggunakan Winston dan Logtail](https://agiksetiawan.medium.com/log-monitoring-nodejs-nestjs-dengan-menggunakan-winston-dan-logtail-70847c326b6c)

[stackoverflow:Winston with AWS Cloudwatch on Nestjs](https://stackoverflow.com/questions/69433044/winston-with-aws-cloudwatch-on-nestjs)

### Winston not logging debug levels in node.js

logger.debug not working in winston logger

Solution:

`Ok, looks like I misunderstood the documentation about default logging levels. As stated in this issue, I need to tell winston that it should output certain log levels`

add this line

```jsx showLineNumbers
level: "debug";
```

```jsx showLineNumbers
import { Logger, format, createLogger, transports } from "winston";

export const exampleLogger = (): Logger => {
  return createLogger({
    transports: [new transports.Console({ level: "debug" })],
    format: format.combine(
      format((info) => {
        info.level = info.level.toUpperCase();
        return info;
      })(),
      format.json()
    ),
  });
};
```

https://stackoverflow.com/questions/68127079/winston-not-logging-debug-levels-in-node-js
