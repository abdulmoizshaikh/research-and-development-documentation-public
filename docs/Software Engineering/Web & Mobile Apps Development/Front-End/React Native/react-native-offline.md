https://www.mindbowser.com/mobile-app-offline-data-synchronization/

**react ntaive offline**
https://medium.com/@InspireNL/redux-offline-queue-open-source-413b20a29e2b

## Firebase admin alternative for react native

Via REST
If you are unable to use a Firebase Admin SDK, Firebase also provides support for sending messages to devices via a POST request:

```json showLineNumbers
POST https://fcm.googleapis.com/v1/projects/myproject-b5ae1/messages:send HTTP/1.1

Content-Type: application/json
Authorization: Bearer ya29.ElqKBGN2Ri_Uz...HnS_uNreA

{
"message":{
"token":"bk3RNwTe3H0:CI2k_HHwgIpoDKCIZvvDMExUdFQ3P1...",
"data":{},
"notification":{

        "body":"This is an FCM notification message!",
        "title":"FCM Message"
      }

}
}
```

https://rnfirebase.io/messaging/notifications#via-rest

how to get client secret for firebase project
https://stackoverflow.com/questions/50507877/where-do-i-get-the-web-client-secret-in-firebase-google-login-for-android
https://console.cloud.google.com/projectselector2/apis/credentials?supportedpurview=project
