# Single sign on SSO POC at retailo

I have a blocker with SSO feature I will finalize POC today and let you update

kanban approach (sprint k ander chezain dalte Jayenge Jaise Jaise tickets ki clarity mill jaegi: Jaise Jaise Kam araha he hm krte Jain) (means a change in a ticket during the sprint)
scrum main Pehle se tickets logged hote hain with clarity and we don't change the requirements from the time when sprint start

change .json to another format
.txt

I guess these 2 packages are contradicting each other let me create a new app and install only react0native-fs in it and read file-path

get external directory path in react native android
https://stackoverflow.com/questions/63392170/write-files-to-the-android-external-storage-using-react-native-fs

try 1 not worked

not working its getting mobile internal storage path
var path = `${RNFS.DocumentDirectoryPath}/Hisaab`;
LOG path /data/user/0/com.app.retailohisaab/files/Hisaab
LOG error ! in read file path [Error: Folder does not exist]

https://github.com/itinance/react-native-fs/issues/462

write file working fine on both Android 7 and 12

but read the file only working in android 7
but not working in android 12
LOG error ! in read file path [Error: ENOENT: /storage/emulated/0/Hisaab/data.txt: open failed: EACCES (Permission denied), open '/storage/emulated/0/Hisaab/data.txt']

Hammad Bhai said public document ya download directory me Karo to chal jaega 12 main

not found the solution for these
https://stackoverflow.com/questions/48446407/react-native-fs-the-actual-document-directory-path-in-android

change to download directory  
 var path = `${RNFS.DownloadDirectoryPath}/Hisaab`;
I have installed but not reading from getting errro
LOG error ! in read file path [Error: ENOENT: /storage/emulated/0/Download/Hisaab/data.txt: open failed: EACCES (Permission denied), open '/storage/emulated/0/Download/Hisaab/data.txt']

it only worked when users have go-to app settings and permissions and allow management of all files rather than media only access

SendIntentAndroid.isAppInstalled("com.google.android.gm").then(isInstalled => {});

2

+25
You can pass your simple text from App1 to App2 via intents (Android )

for this, In App1

install this plugin

npm i react-native-send-intent
Then send your data in the following ways

Option 1: as implicit intent

var SendIntentAndroid = require('react-native-send-intent');

SendIntentAndroid.sendText({
title: 'Please share this text',
text: 'This is the description text of the title',
type: SendIntentAndroid.TEXT_PLAIN
});
Option 2: Specify Your App

// You can specify arbitrary intent extras to be passed to the app
SendIntentAndroid.openApp('com.App2',
{"App2PropData1": "just because", "App2PropData2": "This is the description text of the title"}).then((wasOpened) => {});
In App2

this data will be available in the props

    export default class App extends Component {

    render() {
        console.log('App props', this.props);
        console.log('App2PropData1', this.props.App2PropData1);
        console.log('App2PropData2', this.props.App2PropData2);
        //...
    }

}

https://stackoverflow.com/questions/49550963/sending-simple-data-to-other-apps-using-react-native-in-android

deep linking

```jsx showLineNumbers
<data android:scheme="deeplinking" android:host="retailo.co" />
```

npx uri-scheme open https://retailo.co --android

npx uri-scheme open retailo://hisaab.retailo.co --android

LOG initialUrl retailo://hisaab.retailo.co?token="accesstoken"

decode token and get user-id

```jsx showLineNumbers
{
"data": {
"id": "fd97ecd5-f041-4a95-9afa-c8dfc90ffdb9",
"name": null,
"username": "+923045464742",
"languagePref": "RU",
"customerId": 11566,
"customerLocationId": null,
"accessToken": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTE1NjYsInBob25lIjoiOTIzMDQ1NDY0NzQyIiwiY25pYyI6bnVsbCwicm9sZSI6eyJpZCI6OCwibmFtZSI6IkNPTlNVTUVSIn0sImlhdCI6MTY0Njk3NTM1MSwiZXhwIjoxNjQ2OTk2OTUxLCJhdWQiOiJyZXRhaWxlcnMiLCJpc3MiOiJyZXRhaWxvLmNvICJ9.DqOSTKhqQpQzKGDeYejT226SFG6dmZuFlubN2SvRZBGPAf1NfKd4gdvYrKGumyIM867B0W4XHmYGnLJ7gdbYP8WafL76D0XbU-SMmZ_OvmqKq0unf4oollYYAHt_7nXC4Nf0mvgzDo0Y7JQ8zuwPMcZa6midV9Z4Ra_vG-NUBZg",
"shopName": ""
}
}
```

2 quick questions:
1-what will be the flow when a user is a logout from retailo app
2-

references
Attempt #1: Linking Module
https://devblogs.microsoft.com/cse/2018/04/04/app-app-communication-react-native-android/

https://stackoverflow.com/questions/50980022/how-to-add-header-parameter-at-linking-openurlurl
https://reactnative.dev/docs/linking#send-intents-android

Send Intent Android. open App With Data in react native
Sending Simple Data to Other Apps using React Native in Android
https://stackoverflow.com/questions/49550963/sending-simple-data-to-other-apps-using-react-native-in-android
https://www.npmjs.com/package/react-native-send-intent
https://stackoverflow.com/questions/30446052/getlaunchintentforpackage-is-null-for-some-apps
https://github.com/lucasferreira/react-native-send-intent/issues/109
https://developer.android.com/training/sharing/send

not used
https://stackoverflow.com/questions/57370210/how-to-launch-and-receive-output-from-another-app-through-intent-in-react-native
https://cmichel.io/how-to-set-initial-props-in-react-native
how to receive intent in react native android activity
how to pass data react-native send intent react native
how to get data from intent into react-native
https://stackoverflow.com/questions/39351650/react-native-android-get-the-variables-from-intent
https://developer.android.com/training/app-links/deep-linking#handling-intents
https://github.com/MrToph/react-native-app-launcher/blob/83450c85fb2dd64437b44ffc9d84e580699197cf/android/src/main/java/io/cmichel/appLauncher/LauncherModule.java
https://medium.com/dev-channel/detect-if-your-native-app-is-installed-from-your-web-site-2e690b7cb6fb

SendIntentAndroid.isAppInstalled is not working
sol add this permission

```jsx showLineNumbers
<uses-permission android:name="android.permission.QUERY_ALL_PACKAGES" />
```

Exchange data between React Native Apps
https://stackoverflow.com/questions/52398411/exchange-data-between-react-native-apps
https://medium.com/sketchware/sharing-data-74f02ddf37d0

can we check from mobile chrome that this specific app is installed on android or not

How can I check if an app is installed from a web page on an iPhone
https://stackoverflow.com/questions/13044805/how-can-i-check-if-an-app-is-installed-from-a-web-page-on-an-iphone

React Native Android App Receive Data from Share Intent
https://www.bennettnotes.com/react-native-android-receive-data-from-share-intent/

[Android] Project with path ':@react-native-community_async-storage' could not be found in the project ': app'. #221
https://github.com/react-native-async-storage/async-storage/issues/221
https://react-native-async-storage.github.io/async-storage/docs/install/

Autolinking Native Modules
https://microsoft.github.io/react-native-windows/docs/native-modules-autolinking

npx uri-scheme open retailo://hisaab.retailo.co --android
npx uri-scheme open deeplinking://deeplink.retailo.co --android

```jsx showLineNumbers
Bro, this is the endpoint
POST /auth/users/profile
Request body
{
“accessToken”: string
} (edited)

```

New
3:40
Changes on Dev1

todo later security threads
https://stackoverflow.com/questions/60679685/what-does-query-all-packages-permission-do

references:

the navigation state parsed from the URL contains routes not present in the root navigator
https://reactnavigation.org/docs/configuring-links/

Why is Linking.getInitialURL always returning null?
solution:
3

Haven't been able to make getInitialURL() to work. However you can use:

```jsx showLineNumbers
Linking.addEventListener("url", (url) => {
  console.log("this is the url: ", url);
});
```

https://stackoverflow.com/questions/55482111/why-is-linking-getinitialurl-always-returning-null

Linking.removeEventListener required params
https://stackoverflow.com/questions/64582902/linking-removeeventlistener-required-params

Deep linking not working if navigator names are not unique #9267
solution:

```jsx showLineNumbers
config: {
screens: {
Chat: 'feed/:sort',
},
},
```

https://reactnavigation.org/docs/configuring-links/
https://github.com/react-navigation/react-navigation/issues/9267

android:name="android.permission.QUERY specific package
https://stackoverflow.com/questions/60679685/what-does-query-all-packages-permission-do

https://www.npmjs.com/package/react-native-exit-app

How do I exit/shut down a React Native app?

this is only used for closing the app from the foreground state but not removing the app from the background state
For Android, Use BackHandler to exit the App:
import React, { BackHandler } from 'react-native';
BackHandler.exitApp();
https://stackoverflow.com/questions/34801664/how-do-i-exit-shut-down-a-react-native-app

    how to destroy intent in react native
    Do not destroy android activity and should not be in the history
    https://stackoverflow.com/questions/45743461/do-not-destroy-android-activity-and-should-not-be-in-the-history


    r&D todo
    https://github.com/jamesisaac/react-native-background-task

Single sign-on POC is completed with login API integration  
I have tested by making 2 demo apps and verified on
Android 7
Android 11 and 12 as well.

first time in seem less login

Muiz khan
if retailo app exist show btn and if not don't show btn

Seamless Authentication - POC Demo

What does QUERY_ALL_PACKAGES permission do?
queries in react native android

```jsx showLineNumbers
<queries>
  <package android:name="com.google.android.gm" />
  <package android:name="com.facebook.katana" />
  <intent>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="https" />
  </intent>
  <intent>
    <action android:name="android.intent.action.DIAL" />
    <data android:scheme="tel" />
  </intent>
  <intent>
    <action android:name="android.intent.action.SEND" />
    <data android:mimeType="*/*" />
  </intent>
</queries>
```

https://developer.android.com/guide/topics/manifest/queries-element
https://support.google.com/googleplay/android-developer/answer/10158779?hl=en
https://stackoverflow.com/questions/60679685/what-does-query-all-packages-permission-do
