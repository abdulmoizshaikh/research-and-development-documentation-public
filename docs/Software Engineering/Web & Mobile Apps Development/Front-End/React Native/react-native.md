---
sidebar_position: 1
---

# React Native

apk stands for android Android application Package

> Write only important and time taking tasks not very easy tasks in this sheet

**Environment Variables in React native: (.env)**

Tools like [react-native-dotenv](https://github.com/goatandsheep/react-native-dotenv) and [react-native-config](https://github.com/luggit/react-native-config/) are great for adding environment-specific variables like API endpoints, but they should not be confused with server-side environment variables, which can often contain secrets and API keys.

https://reactnative.dev/docs/security#storing-sensitive-info

## Supporting safe areas :

safeareaview in drawer navigation react native

**Summary**

- Use `react-native-safe-area-context` instead of `SafeAreaView` from `react-native`
- Don't wrap your whole app in `SafeAreaView`, instead wrap content inside your screens
- Use the `edges` prop to apply safe area to specific sides
- Use the `useSafeAreaInsets` hook for more control over where the insets are applied

https://reactnavigation.org/docs/handling-safe-area/

## Higher Order Components :

```jsx showLineNumbers
import React from "react";
import { StatusBar, View } from "react-native";
import styles from "./styles";
import { AppHeader, MediaPlayerFooter } from "../../../components";
import { THEME_COLORS } from "../../../config/constants";
const MediaPlayerWrapper = (props) => {
  const {
    route: { params },
  } = props;
  return (
    <View style={styles.container}>
      <StatusBar backgroundColor={THEME_COLORS.primaryDark} />
      <AppHeader {...props} goBack />
      {props?.children}
      <MediaPlayerFooter {...params} />
    </View>
  );
};
export default MediaPlayerWrapper;
```

```jsx showLineNumbers
// child
import React from "react";
import ImageViewer from "react-native-image-zoom-viewer";
import MediaPlayerWrapper from "../../MediaPlayerWrapper";
const _ImageViewer = (props) => {
  const {
    route: { params },
  } = props;
  const { uri } = params;
  const image = {
    url: uri,
  };
  return (
    <MediaPlayerWrapper {...props}>
      <ImageViewer imageUrls={[image]} renderIndicator={() => {}} />
    </MediaPlayerWrapper>
  );
};
export default _ImageViewer;
```

## React Navigation :

**Navigating to a screen in a nested navigator**

```jsx showLineNumbers
function Root() {
  return (
    <Drawer.Navigator>
      <Drawer.Screen name="Home" component={Home} />
      <Drawer.Screen name="Profile" component={Profile} />
      <Stack.Screen name="Settings" component={Settings} />
    </Drawer.Navigator>
  );
}

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen
          name="Root"
          component={Root}
          options={{ headerShown: false }}
        />
        <Stack.Screen name="Feed" component={Settings} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

https://reactnavigation.org/docs/nesting-navigators/#navigating-to-a-screen-in-a-nested-navigator

**Passing data/parameter using drawer navigation in react navigation 5** how to pass parameter from drawer to screen react navigation

Solution:

```jsx showLineNumbers
<Drawer.Screen
  name="Home"
  initialParams={{ params: route.params }}
  component={BottomTabs}
/>
```

​

```jsx showLineNumbers
// Try this:
import * as React from "react";
import { createDrawerNavigator } from "@react-navigation/drawer";

import Home from "../Screen/Home";
import Profile from "../Screen/Profile";
import Settings from "../Screen/Settings";
import CustomDrawerContent from "./CustomDrawerContent";

const Drawer = createDrawerNavigator();

function DrawerNavigator({ route, navigation }) {
  console.log("params", route.params);
  return (
    <Drawer.Navigator
      initialRouteName="Home"
      drawerContent={(props) => <CustomDrawerContent {...props} />}
    >
      <Drawer.Screen
        name="Home"
        initialParams={{ params: route.params }}
        component={BottomTabs}
      />
      <Drawer.Screen name="Profile" component={Profile} />
      <Drawer.Screen name="Settings" component={Settings} />
    </Drawer.Navigator>
  );
}

export default DrawerNavigator;
```

https://stackoverflow.com/questions/63571033/passing-data-parameter-using-drawer-navigation-in-react-navigation-5

**Screen On focus event integration work in images screen. v6**

```jsx showLineNumbers
  const ImagesSection = props => {
    const {navigation} = props;
    const {imagesMedia, fecthWhatsappStatus} = useWhatsApp();
    React.useEffect(() => {
      const unsubscribe = navigation.addListener('focus', () => {
        // The screen is focused
        // Call any action
        fecthWhatsappStatus();
      });
      // Return the function to unsubscribe from the event so it gets removed on unmount
      return unsubscribe;
    }, [navigation]);
```

https://reactnavigation.org/docs/function-after-focusing-screen/

**Detecting installed apps for sharing :**

What if we wanted to detect if a user has an app installed? Luckily for us, the React Native Share package provides us with a useful method for that.

```jsx showLineNumbers
     const singleShare = async (customOptions) => {
        try {
          const { isInstalled } = await Share.isPackageInstalled(
            "com.whatsapp.android"
            // reference :https://play.google.com/store/apps/details?id=com.whatsapp&hl=en&gl=US
           'com.whatsapp',
          );

          if (isInstalled) {
            await Share.shareSingle(customOptions);
          } else {
            Alert.alert(
              "Whatsapp not installed",
              "Whatsapp not installed, please install.",
              [{ text: "OK", onPress: () => console.log("OK Pressed") }]
            );
          }
        } catch (err) {
          console.log(err);
        }
      };

```

https://blog.logrocket.com/sharing-content-react-native-apps-using-react-native-share/

https://blog.logrocket.com/sharing-content-react-native-apps-using-react-native-share/

**how to share image in react native**

**Sharing media files in react native**

Note: I have already done this share image work in my WhatsAppStatusSaver app here: https://github.com/abdulmoizshaikh/WhatsAppStatusSaver

Next, let’s share an image and a PDF file. To share media files, you’ll need to share the base64 encoded format of the file. For this tutorial, I’ve included a base64.js file that contains an image and PDF converted to the base64 format.

```jsx showLineNumbers
import { StatusBar } from "expo-status-bar";
import React from "react";
import { StyleSheet, Text, View, Button, Image } from "react-native";
import Share from "react-native-share";
import file from "./assets/base64";

const url = "https://awesome.contents.com/";
const title = "Awesome Contents";
const message = "Please check this out.";

const options = {
  title,
  url,
  message,
};
export default function App() {
  const [image, setImage] = React.useState(
    "file:///data/user/0/com.rnshare/cache/rn_image_picker_lib_temp_0f9dbf03-c89c-4728-a763-6b15e3752f8e.jpg"
  );
  const share = async (customOptions = options) => {
    try {
      await Share.open(customOptions);
    } catch (err) {
      console.log(err);
    }
  };

  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
      <Image
        source={{
          uri: image,
        }}
        style={{ ...styles.containerImg, ...styles.stretchImg }}
      />
      <View style={{ marginVertical: 5 }}>
        <Button
          onPress={async () => {
            await share();
          }}
          title="Share Text"
        />
      </View>
      <View style={{ marginVertical: 5 }}>
        <Button
          onPress={async () => {
            await share({
              title: "Sharing image file from awesome share app",
              message: "Please take a look at this image",
              url: file.img,
            });
          }}
          title="Share Image"
        />
      </View>
      <View style={{ marginVertical: 5 }}>
        <Button
          onPress={async () => {
            await share({
              title: "Sharing pdf file from awesome share app",
              message: "Please take a look at this file",
              url: file.pdf,
            });
          }}
          title="Share pdf"
        />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
  containerImg: {
    paddingTop: 50,
    marginVertical: 20,
  },
  stretchImg: {
    width: 200,
    height: 200,
    resizeMode: "stretch",
  },
});
```

https://blog.logrocket.com/sharing-content-react-native-apps-using-react-native-share/

https://www.itechinsiders.com/how-we-share-the-images-in-react-native/

## Storing Sensitive Info

**react-native-keychain:**

**Remember me login details functionality in react native**

Keychain Services allows you to securely store small chunks of sensitive info for the user. This is an ideal place to store certificates, tokens, passwords, and any other sensitive information that doesn’t belong in Async Storage.

What is react native Keychain used for? **Android - Keystore**

The Android Keystore system lets you store cryptographic keys in a container to make it more difficult to extract from the device. react-native-encrypted-storage - uses Keychain on iOS and EncryptedSharedPreferences on Android.22-Jun-2022

https://reactnative.dev/docs/security#secure-storage https://reactnative.dev/docs/security#storing-sensitive-info https://www.npmjs.com/package/react-native-keychain?activeTab=versions https://reactnative.dev/docs/security

**Encryption in react native**

```bash showLineNumbers
You can use crypto-js library https://github.com/brix/crypto-js. Works fine within React Native app.
npm install crypto-js --save
```

---

```bash showLineNumbers
var CryptoJS = require("crypto-js");

var ciphertext = CryptoJS.AES.encrypt('my message', 'secret key 123');
console.log("encrypted text", ciphertext.toString());

var bytes  = CryptoJS.AES.decrypt(ciphertext.toString(), 'secret key 123');
var plaintext = bytes.toString(CryptoJS.enc.Utf8);
console.log("decrypted text", plaintext);
```

https://stackoverflow.com/questions/42826782/how-to-encrypt-and-decrypt-a-text-in-react-native

How to Encrypt and decrypt a Text in react native? [closed]

# encryption decryption in react native

#react native encryption decryption library

sol

You can use crypto-js library https://github.com/brix/crypto-js. Works fine within React Native app.

```jsx showLineNumbers
npm install crypto-js --save
var CryptoJS = require("crypto-js");

var ciphertext = CryptoJS.AES.encrypt('my message', 'secret key 123');
console.log("encrypted text", ciphertext.toString());

var bytes  = CryptoJS.AES.decrypt(ciphertext.toString(), 'secret key 123');
var plaintext = bytes.toString(CryptoJS.enc.Utf8);
console.log("decrypted text", plaintext);

```

https://www.npmjs.com/package/crypto-js

https://stackoverflow.com/questions/42826782/how-to-encrypt-and-decrypt-a-text-in-react-native

Native crypto module could not be used to get secure random number. #256
solution
@rkdqudtjs1 Hmm, the fix is to not use v3.2.0 but instead fix the version to v3.1.9-1

I had moved from crypto version 4.1.1 to 3.1.9-1 and issue was fixed

    	"crypto-js": "v3.1.9-1",

https://github.com/brix/crypto-js/issues/256#

## **Patch-package**

**How to use patch package in react native** Solution:

    1. First do changes in your package in node_modules and check if all working fine
    then follow these steps:

    $ yarn add patch-package postinstall-postinstall
    OR
    $ npm i patch-package postinstall-postinstall

    $ npx patch-package <package-name>
    $ npx patch-package react-native-video

    `muhammadmoiz@nextgeni-HP-ProBook-450-G3:~/Desktop/projects/whatsStatu
    sDownloader$ npx patch-package react-native-video
    patch-package 6.4.7
    • Creating temporary folder
    • Installing react-native-video@5.2.0 with npm
    • Diffing your files with clean files
    ✔ Created file patches/react-native-video+5.2.0.patch

    💡 react-native-video is on GitHub! To draft an issue based on your patch run

        npx patch-package react-native-video --create-issue`

​  
​

    add this line In package.json

     "scripts": {
    +  "postinstall": "patch-package"
     }

    lastly test by running npm install in your project

    `muhammadmoiz@nextgeni-HP-ProBook-450-G3:~/Desktop/projects/whatsStatusDownloader$ npm install

    > whatsStatusDownloader@0.0.1 postinstall
    > patch-package

    patch-package 6.4.7
    Applying patches...
    react-native-video@5.2.0 ✔

    up to date, audited 1360 packages in 3s

    106 packages are looking for funding
      run `npm fund` for details

    found 0 vulnerabilities
    `

I have used this in whatsStatusDownloader app

https://github.com/react-native-video/react-native-video/issues/2611 https://www.npmjs.com/package/patch-package https://gist.github.com/OscarYuen/21f2f8d5c133caef7d31475cfec2d5b0

Using npm patch-package : https://youtu.be/zBPcVGr6XPk

**React native video**

**Add Video to Your React Native App Using react-native-video**

how to get video thumbnail #700 React Native generate thumbnail for video url how to render video thumbnail in react native video

    Actually,I have sloved this by myself. I leave this issue here to help any other who are looking for the solution. :-)
    it's a surprise for me to find that if we put a video uri(such as video generated by react-native-camera) to Image of react-native component, it will show us a thumbnail of the video automatically.
    <Image source={{uri : this.state.videoUri}} />

    and make custom play icon and place it in center and on icon press play the video simple.

https://www.npmjs.com/package/react-native-video#usage

https://betterprogramming.pub/add-video-to-your-react-native-app-using-react-native-video-f020e90059de

**How to use video as a background in React Native** video background react native

https://www.freecodecamp.org/news/how-to-create-a-background-video-in-react-native-cb53304ee4f6/

**React Native Unable to find a matching configuration of project (Build only)** Solution: just remove configuration of package from setting.gradle and the issue gone I have fixed in react-native-videos package after version update

reference: https://github.com/abdulmoizshaikh/WhatsAppStatusSaver/pull/4/commits/0d1bd92ebffdea40ac7cfd9f558affea45f0569f

## Migration in React Native:

I have tried to migrate from 0.60.5 to 0.69.0 but there are alot of changes to merge using react native upgrade helper tool and concluded that its not best practice to use react-native helper when there are lot of changer and version differences are high

and if version differences are not high and file differences are less then is better to use react native upgrade helper tool to upgrade or react-native upgrade helper cli to upgrade

otherwise make new projec at latest react native version and move file and folers in that and upgrade library verisons and configration manually

references:

https://reactnative.dev/docs/upgrading

https://react-native-community.github.io/upgrade-helper/

https://react-native-community.github.io/upgrade-helper/?from=0.60.5&to=0.69.5

## Toast message in React native Android & IOS

Solution:

react-native-toast-message

https://github.com/calintamas/react-native-toast-message

## Pinch to Zoom Image in React Native:

Example of Pinch to Zoom Image in React Native

zoom feature in react native image

zoom image in react native

npm i react-native-image-pan-zoom

https://www.npmjs.com/package/react-native-image-pan-zoom

https://aboutreact.com/react-native-pinch-to-zoom-image/

react-native-image-zoom-viewer (recommended I have tried for Android project WhatsAppstatussave app)

https://www.npmjs.com/package/react-native-image-zoom-viewer

options

## Debugging React Native

**How do you debug React Native?**

how to open debug menu in ios simulator react native

Can I reload my React Native application using a command?

adb shell input keyevent 82 for ios

There is no way to open the dev menu without shaking the phone. Here is the issue related to this problem: the.

Nevertheless, you can always try your code inside an iPhone emulator and open the dev menu using ⌃⌘Z.

https://stackoverflow.com/questions/40441533/can-i-reload-my-react-native-application-using-a-command

https://reactnative.dev/docs/debugging#:~:text=You%20can%20access%20the%20developer,M%20on%20Windows%20and%20Linux.

**How to enable network inspector in chrome react native debugger?**
How can I view network requests (for debugging) in React Native?

Solution:

```jsx showLineNumbers
// To see all the requests in the chrome Dev tools in the network tab.
global.XMLHttpRequest = global.originalXMLHttpRequest || global.XMLHttpRequest;
```

```jsx showLineNumbers
// Add above code in App.js or index.js
/**
 * @format
 */

import { AppRegistry } from "react-native";
import App from "./App";
import { name as appName } from "./app.json";

// To see all the requests in the chrome Dev tools in the network tab.
global.XMLHttpRequest = global.originalXMLHttpRequest || global.XMLHttpRequest;

// fetch logger
// global._fetch = fetch;
// global.fetch = function (uri, options, ...args) {
//   return global._fetch(uri, options, ...args).then(response => {
//     console.log('Fetch', {request: {uri, options, ...args}, response});
//     return response;
//   });
// };

AppRegistry.registerComponent(appName, () => App);
```

Demo:

:::warning

make sure you open debugger using ip address other wise you will get this error

```jsx showLineNumbers
Access to XMLHttpRequest at 'http://192.168.0.198:8081/symbolicate' from origin 'http://localhost:8081' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

:::

![demo1](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image107.png)
![demo2](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image108.png)

you can see API calls from your terminal as well no need to run debugger if your laptop is not of high specs
this way your development will be fast because it's light weight

![demo2](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image109.png)

https://stackoverflow.com/questions/33997443/how-can-i-view-network-requests-for-debugging-in-react-native

https://medium.com/att-israel/debugging-react-native-de1f5396fe83#:~:text=react%2Dnative%2Ddebugger&text=We%20can%20also%20inspect%20network,select%20%E2%80%9CEnable%20Network%20Inspect%E2%80%9D.

:::tip
but chrome debugger with react native have some issues like this so recommended option is react native debugger to debugging react native apps
:::

![demo2](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image110.png)

## Project Structure

https://drive.google.com/drive/u/1/folders/1Np_NaJLpFlj-1ulVnvup_DoM7iqRJjhB

## How to open an app from another app in react native

use these package

```bash showLineNumbers
react-native-send-intent
```

## React Native fabric

https://www.qed42.com/blog/react-native-fabric-why-am-i-so-excited

https://formidable.com/blog/2019/fabric-turbomodules-part-3/

## image caching in react native

https://www.npmjs.com/package/react-native-compress-image
https://stackoverflow.com/questions/60566603/image-compression-in-react-native

## image compression in react native

Q- image compression or size reduce in react native
Q- how whatsapp compress images on mobile end or server end

on Askwho project we had used imagekit for compression
https://imagekit.io/

https://github.com/ivpusic/react-native-image-crop-picker

React Native Image Resizer whatsapp like image compression in react native
A React Native module that can create scaled versions of local images (also supports the assets library on iOS).
https://www.npmjs.com/package/react-native-image-resizer
https://github.com/bamlab/react-native-image-resizer
https://stackoverflow.com/questions/37639360/how-to-optimise-an-image-in-react-native

### react-native-compress-image

https://github.com/Shobbak/react-native-compressor
https://www.npmjs.com/package/react-native-compressor
Output : https://docs.google.com/spreadsheets/d/13TsnC1c7NOC9aCjzN6wkKurJQPeGRNwDhWsQOkXQskU/edit#gid=0

React Native's Image component handles image caching like browsers for the most part. If the server is returning proper cache control headers for images you'll generally get the sort of built in caching behavior you'd have in a browser. Even so many people have noticed:

https://www.npmjs.com/package/react-native-fast-image

https://www.npmjs.com/package/react-native-image-picker

https://stackoverflow.com/questions/58745953/how-to-compress-image-only-when-its-too-large-with-react-native-image-picker

try this

## react-native-fetch-blob

https://blog.notesnook.com/scoped-storage-in-react-native/

https://github.com/ammarahm-ed/react-native-scoped-storage

https://stackoverflow.com/questions/51030576/how-to-read-the-data-from-text-file-in-android-react-native

https://dev-yakuza.posstree.com/en/react-native/react-native-fs/

https://getstream.io/chat/docs/react-native/creating_channels/

### How do I find my IP Address from the command line?

command to get ip address in mac

```bash showLineNumbers
ifconfig | grep "inet " | grep -Fv 127.0.0.1 | awk '{print $2}'
```

https://apple.stackexchange.com/questions/20547/how-do-i-find-my-ip-address-from-the-command-line

## Mobile screen sharing software

Vysor

https://www.vysor.io/

## How to set change app icon in react native (Android && IOS)

`You just have to replace image in respected folder for android and ios and make new build again that's it done`

https://aboutreact.com/react-native-change-app-icon/

### recommended is to use xcode to paste app icon in required places and make build again app icon will be updated

1. Icon Set Creator for iOS ( I have implemented this app icon work for both android and ios in sweet connect baker app)

https://apps.apple.com/us/app/icon-set-creator/id939343785?mt=12 (install this free software on your make and generate very easily)

https://stackoverflow.com/questions/34329715/how-to-add-icons-to-react-native-app

https://appicon.co/

`change the device version on iphone 13 to 13 pro now icon are showing`

https://instamobile.io/react-native-tutorials/react-native-app-icon-ios-android/

# Dropdown picker in react native (Android & IOS)

Solution:

recommended package worked for both platform no extra configuration needed just install and use
I Used in sweet connect project mobile app

e.g

```jsx showLineNumbers
    "react-native-dropdown-picker": "^5.4.2",
```

```bash showLineNumbers
npm install react-native-dropdown-picker
```

Usage:

```jsx showLineNumbers
import DropDownPicker from "react-native-dropdown-picker";

const [open, setOpen] = useState(false);
const [state, setState] = useState(null);
const [items, setItems] = useState(US_STATES);

export const US_STATES = [
  { label: "AL", value: "AL" },
  { label: "AK", value: "AK" },
  { label: "AZ", value: "AZ" },
  { label: "AR", value: "AR" },
];

<DropDownPicker
  open={open}
  value={state}
  items={items}
  setOpen={setOpen}
  setValue={setState}
  setItems={setItems}
  placeholder={"State"}
  disableBorderRadius={true}
  containerStyle={styles.stateDropdown}
  // style={{ borderWidth: 0 }}
/>;
```

https://hossein-zare.github.io/react-native-dropdown-picker-website/docs/usage

## SUSPENSE IN REACT NATIVE

**Is suspense supported in react native**

Yes https://reactnative.dev/docs/react-18-and-react-native#react-18-and-the-react-native-new-architecture

**Disable Paste on React Native TextInput**

```jsx showLineNumbers
<TextInput contextMenuHidden={true} />
```

https://stackoverflow.com/questions/46790050/disable-paste-on-react-native-textinput

### React Native

**\*How to resize TouchableOpacity according to the component present inside it?**

OR
width according to content touchableOpacity ?

Solution: (recommended It works I have tried)

You can actually use alignSelf: 'flex-start' or 'flex-end' depending on which side you want to pin

https://stackoverflow.com/questions/49724094/how-to-resize-touchableopacity-according-to-the-component-present-inside-it

koi bhe issue ho react native main to project android studio main open kr k packages install krlo like gradle update etc
project main jo bhe gradle related issue honge wo fix hojaenge

**Storybook in react native:**

1- Configure Storybook | Building a React Native Component Library with Storybook

https://www.youtube.com/watch?v=nWgKVEEI47Q&ab_channel=ReactNativeSchool

Build a Button Component | Building a React Native Component Library with Storybook

https://www.youtube.com/watch?v=s8dP0GC0nvU&ab_channel=ReactNativeSchool

Docs
https://storybook.js.org/tutorials/intro-to-storybook/react-native/en/get-started/

**Atomic Design Methodology**

Atoms, molecules, organisms, templates, and pages

https://atomicdesign.bradfrost.com/chapter-2/

**Detox**

**React Native graybox testing**

https://infinitbility.com/react-native-detox-with-react-navigation-example
https://github.com/wix/Detox

**husky**

Modern native Git hooks made easy

Husky improves your commits and more 🐶 woof!

Husky used for pre commit and pre push commands to be run

https://www.npmjs.com/package/husky
https://typicode.github.io/husky/#/

**Reselect**

A library for creating memoized "selector" functions. Commonly used with Redux, but usable with any plain JS immutable data as well.

https://www.npmjs.com/package/reselect

```jsx showLineNumbers
import NetInfo from "@react-native-community/netinfo";

export default class ConnectivityCheck {
  static async isNetworkAvailable() {
    const response = await NetInfo.fetch();
    return response.isConnected || false;
  }
}
```

```jsx showLineNumbers
import { useIsEmulator } from "react-native-device-info";
import { BUILD_ENV_NAMES } from "@constants/config";
import { ENV } from "@envconfig";

export const useDetectEmulator = () => {
  const { loading, result } = useIsEmulator();
  return {
    isEmulator: ENV.BUILD_ENV !== BUILD_ENV_NAMES.PRODUCTION ? false : result,
    isCheckingEmulator: loading,
  };
};
```

**error: cannot find symbol import com.facebook.react.bridge.ColorPropConverter;**

Solution:

```bash showLineNumbers
npm i --legacy-peer-deps
```

and open project on android studio error will be fixed

Lottie files used for animation in react native
Lottie files are just json files which we are using to show animation in react native apps
E.g

```jsx showLineNumbers
import * as animationData from "./pinjump.json";
```

https://www.npmjs.com/package/react-lottie

**How to access navigation without passing navigation in nesting child through props in react navigation**

Solution

Always use useNavigation() hook to access navigation in all screens without passing navigation props in each component.
how to use navigation.navigate without by props in react navigation

https://reactnavigation.org/docs/use-navigation

Usage:

Index.js

```jsx showLineNumbers
/**
 * @format
 */
import React from "react";
import { AppRegistry } from "react-native";
import App from "./App";
import { name as appName } from "./app.json";
import "react-native-gesture-handler";
import { NavigationContainer } from "@react-navigation/native";

const Root = () => {
  return (
    <NavigationContainer>
      <App name="moiz" />
    </NavigationContainer>
  );
};
AppRegistry.registerComponent(appName, () => Root);
```

App.js

```jsx showLineNumbers
const App = () => {
 const navigation = useNavigation();
 console.log('navigation',navigation);
```

**how to detect route change in react navigation useNavigation()**

Solution:
Use navigation.addlistener react navigation

```jsx showLineNumbers
import { useNavigation } from "@react-navigation/native";

const navigation = useNavigation();

const handleNavigationChange = (_ding) => {
  navigation.addListener("state", () => {
    const currentRouteName = navigation?.getCurrentRoute()?.name;

    if (currentRouteName) {
      if (!whiteListRoutes.includes(currentRouteName) && _ding?.isPlaying()) {
        _ding.stop(() => {
          setIsPlaying(false);
        });
      }
    }
  });
};
```

#### React native webview

**how to disable zoom with fingers in react native webview**

Disable zoom on web-view react-native?
Disable Pinch to Zoom #1649
Solution

replace this line in your public/index.html folder or react project:

```bash showLineNumbers
<meta name="viewport" content="initial-scale=1.0, maximum-scale=1.0">
```

https://stackoverflow.com/questions/44625680/disable-zoom-on-web-view-react-native
https://github.com/react-native-webview/react-native-webview/issues/1649

**React Native - Accessing drawer navigation outside of AppNavigator**

https://stackoverflow.com/questions/58563204/react-native-accessing-drawer-navigation-outside-of-appnavigator

**navigation.pop and navigation.push not working with drawer navigation #4793**

navigationservice.push not working inside drawer navigation
https://github.com/react-navigation/react-navigation/issues/4793

**Multi bundle mini app in react native**

https://github.com/varunon9/react-native-multiple-bundle
https://varunon9.medium.com/loading-multiple-bundles-in-react-native-code-splitting-using-metro-44d45530e958

**Error [ERR_UNSUPPORTED_ESM_URL_SCHEME]: Only file and data URLs are supported by the default ESM loader - Vue 3**

My problem is because my Node.js version is too low. Upgrade to Node.js 16 solved the problem.

https://stackoverflow.com/questions/69665780/error-err-unsupported-esm-url-scheme-only-file-and-data-urls-are-supported-by

**How to upgrade node version using node version manager nvm**

how to update node version using nvm

First uninstall node version installed globally and then run this commands

```bash showLineNumbers
Nvm install node-version
Nvm use node-version
```

```bash showLineNumbers

This may work:

nvm install NEW_VERSION --reinstall-packages-from=OLD_VERSION
For example:

nvm install 6.7 --reinstall-packages-from=6.4
then, if you want, you can delete your previous version with:

nvm uninstall OLD_VERSION
Where, in your case, NEW_VERSION = 5.4 OLD_VERSION = 5.0

Alternatively, try:

nvm install stable --reinstall-packages-from=current
```

https://stackoverflow.com/questions/34810526/how-to-properly-upgrade-node-using-nvm

**Electrode Native: The Platform For Integrating React Native Into Your Apps**

https://medium.com/walmartglobaltech/electrode-native-the-platform-for-integrating-react-native-into-your-apps-129cbabda7b8

**How to remove nodejs from Ubuntu 16.04?**

```bash showLineNumbers
sudo apt-get purge nodejs
```

https://askubuntu.com/questions/786015/how-to-remove-nodejs-from-ubuntu-16-04

**Update app work in react native**

About
A version checker for react-native applications
https://www.npmjs.com/package/react-native-version-check
https://github.com/kimxogus/react-native-version-check

Usage

```jsx showLineNumbers
import * as React from "react";
import { Variable } from "../constants";
import { Platform, AppState } from "react-native";
import VersionCheck from "react-native-version-check";
import { store } from "../store";
import { AppSettingActions, AuthActions } from "../store/actions";
import { useNavigation } from "@react-navigation/native";
import { useRoute } from "@react-navigation/native";
import AsyncStorageAdapter from "../utills/asyncStorageAdapter";
import { getNotNowFirst, getLangScreenContinue } from "../utills/asyncStorage";
const { storeData } = new AsyncStorageAdapter("@HisaabApp");
const useBuildInfo = () => {
  const navigation = useNavigation();
  const route = useRoute();

  const [country, setCountry] = React.useState("");
  const [latestVersion, setLatestVersion] = React.useState("");
  const [currentVersion, setCurrentVersion] = React.useState("");
  const [needUpdate, setNeedUpdate] = React.useState(false);
  const [currentBuildNumber, setCurrentBuildNumber] = React.useState("0.0.0");
  const [packageName, setPackageName] = React.useState("");
  const [fmVisible, setFMVisible] = React.useState(false);
  const notNow = store?.getState()?.AppSetting?.notNow;
  const appState = React.useRef(AppState.currentState);
  const [appStateVisible, setAppStateVisible] = React.useState(
    appState.current
  );
  const getInfo = async () => {
    try {
      let country = await VersionCheck.getCountry();
      let latestVersion = await VersionCheck.getLatestVersion({
        provider:
          Platform.OS === Variable.ANDROID
            ? Variable.PROVIDER.ANDROID
            : Variable.PROVIDER.IOS,
      });
      let needUpdate = await VersionCheck.needUpdate();
      let currentVersion = await VersionCheck.getCurrentVersion();
      let currentBuildNumber = await VersionCheck.getCurrentBuildNumber();
      let packageName = await VersionCheck.getPackageName();
      setCountry(country);
      setLatestVersion(latestVersion);
      setNeedUpdate(needUpdate);
      setCurrentVersion(currentVersion);
      setCurrentBuildNumber(currentBuildNumber);
      setPackageName(packageName);
    } catch (err) {
      console.warn(err);
    }
  };

  React.useEffect(() => {
    getInfo();
    (async () => {
      if (route.name == "SelectLanguage") {
        getNotNowFirst().then((notNowFirst) => {
          if (!notNowFirst) {
            if (needUpdate?.isNeeded) {
              setFMVisible(true);
            } else {
              setFMVisible(false);
            }
          }
        });
      } else {
        if (!notNow) {
          if (needUpdate?.isNeeded) {
            setFMVisible(true);
          } else {
            setFMVisible(false);
          }
        }
      }
    })();
  }, []);

  React.useEffect(() => {
    const unsubscribe = navigation.addListener(Variable.FOCUS, async () => {
      let needUpdate = await VersionCheck.needUpdate();
      const notNow = store?.getState()?.AppSetting?.notNow;
      if (route.name == "SelectLanguage") {
        getNotNowFirst().then((notNowFirst) => {
          if (!notNowFirst) {
            if (needUpdate?.isNeeded) {
              setFMVisible(true);
            } else {
              setFMVisible(false);
            }
          }
        });
      } else {
        if (!notNow) {
          if (needUpdate?.isNeeded) {
            setFMVisible(true);
          } else {
            setFMVisible(false);
          }
        }
      }
    });

    return unsubscribe;
  }, []);

  React.useEffect(() => {
    const subscription = AppState.addEventListener(
      "change",
      async (nextAppState) => {
        const langSelect = await getLangScreenContinue();

        if (!langSelect) {
          let needUpdate = await VersionCheck.needUpdate();
          const notNowAppState = store?.getState()?.AppSetting?.notNowAppState;
          //if (appState.current.match(/inactive|background/) && nextAppState === 'active') {
          if (appState.current.match(/inactive|background/)) {
            store.dispatch(
              AppSettingActions.updateAppStateActive({ activeAppState: true })
            );
            if (!notNowAppState) {
              await storeData("activeAppState", JSON.stringify(true));
            }
          }
          appState.current = nextAppState;
          setAppStateVisible(appState.current);

          if (!notNowAppState) {
            if (needUpdate?.isNeeded) {
              setFMVisible(true);
            } else {
              setFMVisible(false);
            }
          }
        }
      }
    );

    return () => {
      subscription.remove();
    };
  }, []);
  return {
    country,
    latestVersion,
    currentVersion,
    needUpdate,
    currentBuildNumber,
    packageName,
    fmVisible,
    setFMVisible,
    appStateVisible,
  };
};

export default useBuildInfo;
```

Usage

```jsx showLineNumbers
import { useBuildInfo, useEvent, useForceUpdateApp } from "../../hooks";

const { fmVisible, setFMVisible } = useBuildInfo();

<ForceUpdateModal
  cmVisible={fmVisible}
  setCMVisible={setFMVisible}
  hideNotNow={hideNotNow}
/>;

import * as React from "react";
import { Linking, BackHandler } from "react-native";
import { Colors, Fonts, Metrix } from "../../theme";
import { AppButton } from "../AppButton";
import { StyledText } from "../../theme/styles";
import { Variable } from "../../constants";
import { StatusCard } from "../StatusCard";
import { ConfirmationModal } from "../ConfirmationModal";
import { AppModal } from "../AppModal";
import { useTranslation } from "react-i18next";
import { store } from "../../store";
import { AppSettingActions } from "../../store/actions";
import { useDispatch } from "react-redux";
import AsyncStorageAdapter from "../../utills/asyncStorageAdapter";
import { getAppState } from "../../utills/asyncStorage";
const { removeData, storeData } = new AsyncStorageAdapter("@HisaabApp");
import { useRoute } from "@react-navigation/native";
/**
 *ForceUpdateModal Transaction Detail Modal
 */
interface ForceUpdateModalProps {
  hideNotNow: boolean;
  setCMVisible: Function;
  cmVisible: boolean;
  fromLang?: boolean;
}

export const ForceUpdateModal: React.FC<ForceUpdateModalProps> = React.memo(
  ({ hideNotNow, setCMVisible, cmVisible, fromLang = false }) => {
    const { t } = useTranslation();
    const dispatch = useDispatch();
    const route = useRoute();

    return (
      <AppModal
        backDropClose={false}
        handleModal={() => setCMVisible(!cmVisible)}
        modalVisible={cmVisible}
        children={
          <ConfirmationModal
            title={t("APP_NEW_VERSION_TITLE")}
            message={t("APP_NEW_VERSION_TEXT")}
            setModalVisible={() => setCMVisible(!cmVisible)}
            handleAction={() => {
              BackHandler.exitApp();
              Linking.openURL(Variable.HISAAB_PLAYSTORE_URL);
            }}
            hideNotNow={hideNotNow}
            handleCancel={async () => {
              const appStateChange = await getAppState();

              if (appStateChange) {
                let ans = await removeData("activeAppState");
                dispatch(
                  AppSettingActions.updateVersionNotNowOnAppState({
                    notNowAppState: true,
                  })
                );
              }
              if (route.name == "SelectLanguage") {
                let ans = await storeData("notNowFirst", JSON.stringify(true));
              }
              setCMVisible(false);
              dispatch(AppSettingActions.updateVersionNotNow({ notNow: true }));
            }}
          />
        }
      />
    );
  }
);
```

### REACT NATIVE

**How do you hide the warnings in React Native iOS simulator?**

According to React Native Documentation, you can hide warning messages by setting disableYellowBox to true like this:
console.disableYellowBox = true;
Update: React Native 0.63+
console.disableYellowBox is removed and now you can use:

```jsx showLineNumbers
import { LogBox } from "react-native";
LogBox.ignoreLogs(["Warning: ..."]); // Ignore log notification by message
LogBox.ignoreAllLogs(); //Ignore all log notifications
```

https://stackoverflow.com/questions/35309385/how-do-you-hide-the-warnings-in-react-native-ios-simulator

**React Native OTP Input (used by other developers in sweet connect app not ideal approach I guess)**

@twotalltotems/react-native-otp-input is a tiny Javascript library which provides an elegant UI for the end user to input one time passcode (OTP). It handles the input suggestion on iOS when the OTP SMS is received. For Android, it will autofill when the user presses the copy button on the SMS notification bar. It also features a carefully crafted flow to handle edge cases for volatile user gestures. We provide default UI, but you can always customize the appearance as you like.

https://www.npmjs.com/package/@twotalltotems/react-native-otp-input

**What Is a Blob?**

According to Wikipedia: "A binary large object (BLOB or blob) is a collection of binary data stored as a single entity. Blobs are typically images, audio, or other multimedia objects, though sometimes binary executable code is stored as a blob."

What this means is that a blob is essentially a container for data, so it's more easily handled by protocols that fetch and manipulate large media files. So, if you're planning on working in an application with limited resources handling media files like photos or music, you'll be handling blobs.

**toast in react native (used in sweetconnect project)**

https://www.npmjs.com/package/react-native-flash-message

**Make Use of requestAnimationFrame**

Sometimes, if we do an action in the same frame that we are adjusting the opacity or highlight of a component that is responding to a touch, we won't see that effect until after the onPress function has returned. If onPress does a setState that results in a lot of work and a few frames dropped, this may occur. A solution to this is to wrap any action inside of your onPress handler in requestAnimationFrame :

```jsx showLineNumbers
handleOnPress() {
    requestAnimationFrame(() => {
        this.doExpensiveAction();
    });
}

```

https://www.pluralsight.com/guides/how-to-use-requestanimationframe-with-react

**React-native-background-timer**

used this package in hisaab package by zohaib after QA report an issue of timer not working when app isint background state and it was working fine using this package.
for run timer in background as well

```jsx showLineNumbers
"react-native-background-timer": "^2.4.1”,
```

**generate random phone number method javascript**

```jsx showLineNumbers
phoneNumber: `03 ${Math.floor(100000000 + Math.random() * 900000000)}`, // temp added this
```

**location permission not granted in react native**

invalid authorization level provided react native

https://stackoverflow.com/questions/59892302/location-permission-not-granted-in-react-native

**how to change current location on ios emulator**

in iOS Simulator menu, go to Debug -> Location -> Custom Location. There you can set the latitude and longitude and test the app accordingly.

https://stackoverflow.com/questions/214416/set-the-location-in-iphone-simulator#:~:text=in%20iOS%20Simulator%20menu%2C%20go,and%20test%20the%20app%20accordingly.

**How get latitudeDelta and longitudeDelta from any region?#505**

How to zoom in/out in react-native-map?

```jsx showLineNumbers
MAP_VIEW: {
   LATITUDE_DELTA: 0.0922,
   LONGITUDE_DELTA: 0.0421,
 },

```

https://stackoverflow.com/questions/36685372/how-to-zoom-in-out-in-react-native-map/36688156#36688156 (recommended)
https://github.com/react-native-maps/react-native-maps/issues/505
https://stackoverflow.com/questions/50882700/react-native-mapview-what-is-latitudedelta-longitudedelta
https://stackoverflow.com/questions/50882700/react-native-mapview-what-is-latitudedelta-longitudedelta
https://github.com/react-native-maps/react-native-maps/issues/637
https://stackoverflow.com/questions/51116342/get-latitudedelta-and-longitudedelta-from-viewport-in-react-native

**What is the difference between reset password and change password?**

You change your password when you KNOW your current password. You reset your password when you DON'T KNOW your current password, but HAVE created a password profile.27-Aug-2019

**error: bundling failed: Error: Unable to resolve module `@react-native-community/toolbar-android` from `/Users/freelancing/Desktop/Freelancing/Work/Projects/Mobile-Apps/RoccoFriend/lazzyapp-mobile/node_modules/react-native-vector-icons/lib/toolbar-android.js`: Module `@react-native-community/toolbar-android` does not exist in the Haste module map**

This might be related to https://github.com/facebook/react-native/issues/4968
To resolve try the following:

1. Clear watchman watches: `watchman watch-del-all`.
2. Delete the `node_modules` folder: `rm -rf node_modules && npm install`.
3. Reset Metro Bundler cache: `rm -rf /tmp/metro-bundler-cache-*` or `npm start -- --reset-cache`.

Error Bundling Failed Error Unable To Resolve Module React Native Community Toolbar
Error: Unable to resolve module `@react-native-community/toolbar-android`

Solution:

```jsx showLineNumbers
npm install --save @react-native-community/toolbar-android
```

```jsx showLineNumbers
@react-native-community/toolbar-android": "^0.1.0-rc.1
"@react-native-picker/picker": "^1.9.7”
```

https://stackoverflow.com/questions/62769564/error-unable-to-resolve-module-react-native-community-toolbar-android

**react-native, bundling failed**
error: bundling failed: Error: Program(path) {
bundling failed error program(path) react native

Solution:

Just close all programs and restart the computer and fresh start all things it will be fixed

https://stackoverflow.com/questions/51068105/react-native-bundling-failed

**unexpected identifier '\_classcallcheck' react native**

Solution:

In my case it was babel, actually i removed the yarn.lock file and after a fresh yarn the babel version was updated so its creating this issue, so what i did i just revert the yarn.lock file and remove ( ^ ) from "@babel/core" version and did a yarn and then it works....

https://stackoverflow.com/questions/70737126/react-native-error-unexpected-identifier-classcallcheck-import-call-expects

**Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './lib/tokenize' is not defined by "exports" in the package.json of a module in node_modules**

Just go for node.js v14.18.1 and remove the latest version just use the stable version v14.18.1

https://stackoverflow.com/questions/69693907/error-err-package-path-not-exported-package-subpath-lib-tokenize-is-not-d

**Installing node from command line**
Node.js v16.x:

```jsx showLineNumbers
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt-get install -y nodejs
```

https://github.com/nodesource/distributions/blob/master/README.md#debinstall

**Error: Cannot find module 'mkdirp'**

solution

```jsx showLineNumbers
Rm -rf ./node_modules
Delete package-lock.json
npm install
npm run android
```

https://stackoverflow.com/questions/22625024/error-cannot-find-module-mkdirp

**React-Native: Module AppRegistry is not a registered callable module**

https://stackoverflow.com/questions/34969858/react-native-module-appregistry-is-not-a-registered-callable-module

ios like toggle switch for android react native use this package :

toggle-switch-react-native

**you must complete the advertising id declaration before releasing an app that target android 13 in react native**

Solution:

```jsx showLineNumbers
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

https://stackoverflow.com/questions/71473553/action-requested-declare-your-ad-id-permission
https://forum.unity.com/threads/android-13-advertising-id-declaration-required-by-google-play.1314465/

https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient
https://support.google.com/googleplay/android-developer/answer/6048248?hl=en
https://www.npmjs.com/package/react-native-advertising-id#usage

https://androidx.tech/artifacts/ads/ads-identifier/1.0.0-alpha02-source/androidx/ads/identifier/AdvertisingIdClient.java.html
https://developer.android.com/reference/androidx/ads/identifier/AdvertisingIdClient

**how to prevent keyboard close in react native scrollview**

Solution:
Prevent keyboard dismiss. React native
Use keyboardShouldPersistTaps to handle this.

```jsx showLineNumbers
    <ScrollView
    keyboardShouldPersistTaps={'always'}
    >
```

https://stackoverflow.com/questions/45883463/prevent-keyboard-dismiss-react-native

How to add event listener in react native functional components

```jsx showLineNumbers
useEffect(() => {
  const unsubscribe = navigation.addListener("focus", () => {
    dispatch(fetchUserSummary());
  });
  return unsubscribe;
}, []);
```

React Native MoEngage (retailo was using this in consumer app)

Install MoEngage's React Native plugin using the npm package manager. And then link your native dependencies :

https://www.npmjs.com/package/react-native-moengage

**Lottie splash screen in react native (used in retailo consumer app by consumer team)**

https://www.npmjs.com/package/react-native-lottie-splash-screen

**For pull to refresh without using flatlist in react native on any type of screen**

https://reactnative.dev/docs/refreshcontrol

**react native splash screen (Android)**

https://www.youtube.com/watch?v=yFrx8HZlNtI&ab_channel=ReactNativeSchool

**react native splash screen (IOS)**

https://www.youtube.com/watch?v=H0CC1UsvjDQ&ab_channel=ReactNativeSchool

**Should I use Redux Toolkit or Redux?**

However, we strongly recommend using Redux Toolkit for all Redux apps. Overall, whether you're a brand new Redux user setting up your first project, or an experienced user who wants to simplify an existing application, using Redux Toolkit will make your code better and more maintainable.24-May-2022

https://redux.js.org/redux-toolkit/overview

**Why You Should Use Redux Toolkit**

Redux Toolkit makes it easier to write good Redux applications and speeds up development, by baking in our recommended best practices, providing good default behaviors, catching mistakes, and allowing you to write simpler code. Redux Toolkit is beneficial to all Redux users regardless of skill level or experience. It can be added at the start of a new project, or used as part of an incremental migration in an existing project.

Note that you are not required to use Redux Toolkit to use Redux. There are many existing applications that use other Redux wrapper libraries, or write all Redux logic "by hand", and if you still prefer to use a different approach, go ahead!
However, we strongly recommend using Redux Toolkit for all Redux apps.

Overall, whether you're a brand new Redux user setting up your first project, or an experienced user who wants to simplify an existing application, using Redux Toolkit will make your code better and more maintainable.

https://redux.js.org/redux-toolkit/overview#:~:text=Redux%20Toolkit%20makes%20it%20easier,of%20skill%20level%20or%20experience.
https://redux.js.org/style-guide/#use-redux-toolkit-for-writing-redux-logic

```json showLineNumbers
{
  "plugins": [
    [
      "module-resolver",
      {
        "root": ["./src"],
        "alias": {
          "test": "./test",
          "underscore": "lodash"
        }
      }
    ]
  ]
}
```

https://www.npmjs.com/package/babel-plugin-module-resolver

npm install --save-dev eslint-plugin-react-native

https://github.com/Intellicode/eslint-plugin-react-native
https://eslint.org/docs/latest/user-guide/configuring/rules#:~:text=ESLint%20comes%20with%20a%20large,0%20%2D%20turn%20the%20rule%20off

```json showLineNumbers

module.exports = {
  root: true,
  extends: '@react-native-community',
  rules: {
    'react-native/no-unused-styles': 2,
    'react-native/split-platform-components': 2,
    'react-native/no-inline-styles': 2,
    'react-native/no-color-literals': 2,
    'react-native/no-raw-text': 2,
    'react-native/no-single-element-style-arrays': 2,
  },
};

```

**react native stylesheet formatter prettier**

Format Code Style with Prettier in React Native (recommended)

https://blog.reactnativecoach.com/format-code-style-with-prettier-in-react-native-1e10e6b7169f
https://github.com/typicode/husky
https://github.com/IronTony/react-native-redux-toolkit-starter-app/blob/master/package.json

**Error: No similarly named formulae found. Error: No available formula or cask with the name "python"**

rm -fr $(brew --repo homebrew/core)
Error: No similarly named formulae found. It was migrated from homebrew/cask to homebrew/core.

Solution:

```bash showLineNumbers
brew install python3
```

https://stackoverflow.com/questions/66032996/error-no-similarly-named-formulae-found-error-no-available-formula-or-cask-wi

**how to uninstall homebrew on mac ?**
How to uninstall home-brew for Mac?

Solution:

```bash showLineNumbers
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall.sh)"
```

https://osxdaily.com/2018/08/12/how-uninstall-homebrew-mac/
https://appuals.com/install-and-uninstall-homebrew-on-macos/

**How to install brew on Mac**

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
https://brew.sh/

Rename a JavaScript file to be \*.tsx
Run yarn tsc to type-check your new TypeScript files.

Run npm run compile to check typescript files errors in file before push code to remote repo
We have used in Reatilo consumer app

```json showLineNumbers
"compile": "tsc",


"husky": {
   "hooks": {
     "pre-commit": "lint-staged",
     "pre-push": "npm run compile && npm run test"
   }
 },
```

https://reactnative.dev/docs/typescript

```jsx showLineNumbers
getMobileLoadOrders = async (
  baseUrl: string,
  id: string,
  duration?: string,
  startDate?: string,
  endDate?: string,
  page?: allAnyTypes
): Promise<allAnyTypes> => {
  try {
    const apiResponse = await this.get(
      `${baseUrl}/mobile-load/api/v1/users/${id}/mobile-load-orders`,
      {
        ...(duration && { duration }),
        ...(startDate && { startDate }),
        ...(endDate && { endDate }),
        ...(page && { page }),
      },
      undefined,
      API_TIMEOUT.CUSTOMER_FEATURES
    );
    return prepareResponseObject(apiResponse, RESPONSE_TYPES.SUCCESS);
  } catch (error) {
    throw prepareErrorResponse(error);
  }
};
```

**What is enableHermes? In react native**

Hermes is an open-source JavaScript engine optimized for React Native. For many apps, enabling Hermes will result in improved start-up time, decreased memory usage, and smaller app size. At this time Hermes is an opt-in React Native feature, and this guide explains how to enable it.10-May-2022

https://reactnative.dev/docs/hermes

Copy of ProtectedSheet
URL to Encrypt/Decrypt -
Web Tutorial - http://skipser.com/502

react-native :app:installDebug FAILED

```jsx showLineNumbers
Just clear android build
Cd android && ./gradlew clean
```

https://stackoverflow.com/questions/37500205/react-native-appinstalldebug-failed

### Code push

https://microsoft.github.io/code-push/

**Code push by app center in react native**

This short tutorial guide you through the codepush setup in react native application.
Github project link :

https://github.com/deepaksisodiya/rea...
https://www.youtube.com/watch?v=f6I9y7V-Ibk
https://github.com/microsoft/react-native-code-push#example-apps--starters

**How to use Microsoft Code Push with React Native (it will update installed react native bundle with updated bundle from code push server)**

https://www.youtube.com/watch?v=uN0FRWk-YW8&ab_channel=BilalBudhani

**CodePush Strategy for Beta Testing**

https://www.youtube.com/watch?v=TLSguWxnzwo&ab_channel=ReactNativeSchool

**Gray box testing in react native | react native automation testing | react native detox**

https://github.com/wix/Detox
https://blog.logrocket.com/react-native-end-to-end-testing-detox/

**cannot read property getCountryCode of null in react native**
ON android 11 its not working when I unintsll react antive country picker lib
but on android 8 workign

now testing with lib on both devices
yes by using this libaray issues fixed

https://www.npmjs.com/package/react-native-device-country

**How to get phone country code in react native with access location permission**
https://www.npmjs.com/package/react-native-device-country

Or directly use prebuid native modules by react native

I had tried to fetch country from playstore using this package but its giving me US all the time I had tried on multiple devices (not worked using this package not recommended

```jsx showLineNumbers
       "react-native-version-check": "^3.4.2",
)
           let country = await VersionCheck.getCountry();
           console.log('country from playstore', country);
```

Output:

country from playstore US

The below method worked :

```jsx showLineNumbers
import { NativeModules } from "react-native";
const { DeviceCountryModule } = NativeModules;

React.useEffect(() => {
  setDefaultCountryCode();
}, []);

const setDefaultCountryCode = () => {
  DeviceCountryModule.getCountryCode("any")
    .then((result) => {
      const countryCode =
        JSON.parse(result)?.code?.toUpperCase() || result?.code?.toUpperCase();
      console.log("countryCode", countryCode);
      if (Variable.SUPPORTED_COUNTRY_CODES.includes(countryCode))
        setCountryCode(countryCode);
    })
    .catch((e: any) => {
      console.warn(e);
    });
};

// const setDefaultCountryCode = async () => {
//  try {
//      const result = await fetchDeviceCountryCode();
//      const countryCode = JSON.parse(result)?.code?.toUpperCase() || result?.code?.toUpperCase();
//      console.log('countryCode', countryCode);
//      setCountryCode(countryCode);
//  } catch (error) {
//      console.warn(error);
//  }
// };
```

**Android Virtual devices (AVD manager in android studio):**

We can create virtual device from android studio of any specific Android version to test build and fix OS specific issue.

**How to change device location to another country or region or sector etc?**

Solution:

Fake GPD or lokito mobile apps are used to change location of mobile device for testing geofencing etc
Or vpn or open vpn is also another option
https://play.google.com/store/apps/details?id=fr.dvilleneuve.lockito&hl=en&gl=US
https://play.google.com/store/apps/details?id=com.blogspot.newapphorizons.fakegps&hl=en&gl=US

// Instead of navigator.geolocation, just use Geolocation.
https://enappd.com/blog/geolocation-geocoding-react-native-apps/84/

https://developers.google.com/maps/documentation/geocoding/get-api-key
https://www.npmjs.com/package/react-native-geocoding
https://github.com/marlove/react-native-geocoding

**User current location permission work in react native android**

React native current location asking for permission in AndroidManifiest.xml ACCESS_FINE_LOCATION, but already added

Answer:

You need to add ACCESS_FINE_LOCATION and ACCESS_COARSE_LOCATION permission in manifest

make sure you have added the permission in manifest file

```bash showLineNumbers
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

if you are targetting android api 23 and above than you have to ask run-time permission

Because Beginning in Android 6.0 (API level 23), users grant permissions to apps while the app is running, not when they install the app.

Reference:

https://developer.android.com/training/permissions/requesting
https://stackoverflow.com/questions/48108919/react-native-current-location-asking-for-permission-in-androidmanifiest-xml-acce
https://reactnative.dev/docs/permissionsandroid
https://stackoverflow.com/questions/45822318/how-do-i-request-permission-for-android-device-location-in-react-native-at-run-t

**Geocoding API:**

https://developers.google.com/maps/documentation/geocoding/get-api-key

**How to get user country without gps**

Solution:

Use react-native-localize:

I have done POC on my personal device but its not working properly its getting country from mobile language like my mobile language is En-US to its giving me US in countrycode and USB as currency which is not useful for me its not getting user location or based on location

R&D of npm i react-native-localize package checking if city is fetching or not

RNLocalize.getLocales() [{"countryCode": "US", "isRTL": false, "languageCode": "en", "languageTag": "en-US"}, {"countryCode": "GB", "isRTL": false, "languageCode": "en", "languageTag": "en-GB"}]

https://stackoverflow.com/questions/53922584/how-to-get-user-country-without-gps

**How can I get the device's ip on React Native?**

https://stackoverflow.com/questions/38595282/how-can-i-get-the-devices-ip-on-react-native

By default our code start from root index.js file (file placed on root directory of the project)
But If we want to change its path let say start project from index.js or index.ts file from src/index.js then we have to add this source line in our package .json like this

"source": "src/index.tsx",
E.g see source line (no index.js file in root directory it starting from src/index.js

```jsx showLineNumbers
{
 "name": "offline-sync-react",
 "version": "1.0.2",
 "description": "A package that allows synchronizing of locally stored data on availability of a network connection",
 "author": "angaza_elimu",
 "license": "LGPL 3.0",
 "repository": "Angaza-Elimu/react-offline-sync",
 "main": "dist/index.js",
 "source": "src/index.tsx",//this line
 "engines": {
   "node": ">=10"
 },
 "scripts": {
```

**how to prevent user to double tap on a button in react native ?**

Sol:

```jsx showLineNumbers
“prevent double tap in react native” Code Answer
import debounce from 'lodash.debounce'; // 4.0.8

const withPreventDoubleClick = (WrappedComponent) => {

  class PreventDoubleClick extends React.PureComponent {

    debouncedOnPress = () => {
      this.props.onPress && this.props.onPress();
    }

    onPress = debounce(this.debouncedOnPress, 300, { leading: true, trailing: false });

    render() {
      return <WrappedComponent {...this.props} onPress={this.onPress} />;
    }
  }

  PreventDoubleClick.displayName = `withPreventDoubleClick(${WrappedComponent.displayName ||WrappedComponent.name})`
  return PreventDoubleClick;
}
```

https://www.codegrepper.com/code-examples/javascript/prevent+double+tap+in+react+native

**Q Debounce effect throteling in react native using lodash**

```jsx showLineNumbers
_.debounce( func, wait, options )
Parameters: This method accepts three parameters as mentioned above and described below:
```

func: It is the function that has to be debounced.
wait: It is the number of milliseconds for which the calls are to be delayed. It is an optional parameter. The default value is 0.
options: It is the options object that can be used for changing the behaviour of the method. It is an optional parameter.

https://www.geeksforgeeks.org/lodash-_-debounce-method/

```jsx showLineNumbers
import _ from "lodash";
const handleSearch = _.debounce((cb) => {
  cb();
}, 500);

React.useEffect(() => {
  handleSearch(() =>
    dispatch(
      HomeActions.getTransaction({
        id: ledgerId,
        text: text,
        type: khataFilter.find((item) => item.isSelected)?.type,
      })
    )
  );
}, [text]);

<Search
  ref={inputRef}
  placeholder={t("NAAM_YA_NUMBER_TYPE_KARAIN")}
  onChange={(e: any) => {
    setText(e);
  }}
  value={text}
/>;
```

**Automatic otp verification**

Setup

```jsx showLineNumbers
mainActivity.java
import com.faizal.OtpVerify.RNOtpVerifyPackage;

android/app/build.gradle
    compile project(':react-native-otp-verify')

android/setting.gradle
include ':react-native-otp-verify'
project(':react-native-otp-verify').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-otp-verify/android')

```

This package is use to auto fill otp from message in react native (zubair have implement this feature in hisaab app).

```js showLineNumbers
       "react-native-otp-verify": "^1.0.4",
```

E.g:

```jsx showLineNumbers
import React, { useState, useEffect } from "react";
import { PinInput, Center, FormControl, Alert } from "native-base";
import OTPInputView from "@twotalltotems/react-native-otp-input";
import RNOtpVerify from "react-native-otp-verify";
// Styles imports
import { PinnedStyles } from "./style";
import { Keyboard } from "react-native";

export const PinInputField = ({ onPinCodeComplete }) => {
  const [code, setCode] = useState("");
  const [enableBtn, setEnableBtn] = useState(false);

  const handlePinChange = (number) => {
    setCode(number);
  };
  useEffect(() => {
    onPinCodeComplete(code);
    startListeningForOtp();
    return () => RNOtpVerify.removeListener();
  }, [code]);
  const getHash = () =>
    RNOtpVerify.getHash().then(console.log).catch(console.log);

  const startListeningForOtp = () => {
    RNOtpVerify.getOtp()
      .then((p) => RNOtpVerify.addListener(otpHandler))
      .catch((p) => console.log(p));
  };

  const otpHandler = (message: string) => {
    const otp = /(\d{5})/g.exec(message)?.[1];
    setCode(otp);
    RNOtpVerify.removeListener();
    Keyboard.dismiss();
  };
  return (
    <Center>
      <OTPInputView
        style={{ height: 50 }}
        pinCount={5}
        code={code}
        onCodeChanged={handlePinChange}
        autoFocusOnLoad
        codeInputFieldStyle={PinnedStyles.fieldStyleBase}
        codeInputHighlightStyle={PinnedStyles.borderStyleHighLighted}
        onCodeFilled={(code) => {
          console.log(`Code is ${code}, you are good to go!`);
        }}
      />
    </Center>
  );
};
```

**usestate not working in setinterval setstate**

State not updating when using React state hook within setInterval

Solution:
The reason is because the callback passed into setInterval's closure only accesses the time variable in the first render, it doesn't have access to the new time value in the subsequent render because the useEffect() is not invoked the second time.

time always has the value of 0 within the setInterval callback.

```jsx showLineNumbers
From
setTime(partime+1)
To
setTime(prevTime => prevTime + 1); // <-- Change this line!
Make this arrow function fix issue because function will get last updated value in setState
```

https://stackoverflow.com/questions/53024496/state-not-updating-when-using-react-state-hook-within-setinterval

Sol 2:

**useRef can solve this problem, here is a similar component which increase the counter in every 1000ms**

```jsx showLineNumbers
import { useState, useEffect, useRef } from "react";

export default function App() {
  const initalState = 0;
  const [count, setCount] = useState(initalState);
  const counterRef = useRef(initalState);

  useEffect(() => {
    counterRef.current = count;
  });

  useEffect(() => {
    setInterval(() => {
      setCount(counterRef.current + 1);
    }, 1000);
  }, []);

  return (
    <div className="App">
      <h1>The current count is:</h1>
      <h2>{count}</h2>
    </div>
  );
}
```

https://itnext.io/how-to-work-with-intervals-in-react-hooks-f29892d650f2
https://stackoverflow.com/questions/53024496/state-not-updating-when-using-react-state-hook-within-setinterval

**How to publish app android app to google play store step by step guide :**

How to Publish an Android App on Google Play Store: A Step-by-Step Guide (recommended)

https://orangesoft.co/blog/how-to-publish-an-android-app-on-google-play-store (must read)

**how to delete app from google play console shared with internal testers only**

Cannot remove "Internal test track" build from Google Play Console
How to remove application from app listings on Android Developer Console
how to delete app from play store after rollout

solution:
For this you have to upload new release build and publish new release build not publish old version build to the live.

Or other sol

To remove a closed test track that you created, select Deactivate track. You can access deactivated tracks on the App releases page in the “Closed tracks” section.
To end an open, closed alpha, or internal test, select Remove testers.

https://stackoverflow.com/questions/50626453/cannot-remove-internal-test-track-build-from-google-play-console

https://medium.com/@pawardeepakv/google-play-console-internal-test-c6e4ea369ed8#:~:text=To%20remove%20a%20closed%20test,internal%20test%2C%20select%20Remove%20testers.

https://stackoverflow.com/questions/11074972/how-to-remove-application-from-app-listings-on-android-developer-console

**How to move to down in flatlist using this**

Inverted key
And you have to reverse data as well in order to show in correct order

**For crop image in react native**

iOS/Android image picker with support for camera, video, configurable compression, multiple images and cropping
https://www.npmjs.com/package/react-native-image-crop-picker

react-native-image-crop-picker

https://www.npmjs.com/package/react-native-image-crop-picker

**Image compression in react native:**

We had used react-native-image-picker library for upload and compressing image size by quality parameter

**Camera not opening in android 8 issue fixed.**

Solution:

Add permission in manifest.xml and ask request permission before launch camera.
react-native-image-picker not working in android 10
launchCamera not working in android 8 for react native image picker
camera not opening in android 8 in react native image picker

https://stackoverflow.com/questions/64054870/react-native-image-picker-not-working-in-android-10

```js showLineNumbers
IMG_PICKER_ACTIONS: [
       {
           title: 'CAMERA_SAY_UPLOAD_KARAIN',
           type: 'capture',
           options: {
               mediaType: 'photo',
               includeBase64: false,
               includeExtra,
               selectionLimit: 1,
           },
       },
       {
           title: 'GALLERY_SAY_UPLOAD_KARAIN',
           type: 'library',
           options: {
               mediaType: 'photo',
               includeBase64: false,
               includeExtra,
               selectionLimit: 2,
           },
       },
   ],
```

```jsx showLineNumbers
import { PermissionsAndroid, Platform } from "react-native";
import { Variable } from "../constants";

export const useCameraPermission = () => {
  return new Promise(async (resolve, reject) => {
    try {
      if (Platform.OS === Variable.IOS) {
      } else if (Platform.OS === Variable.ANDROID) {
        // add write external storage permission for saveToPhotos: true
        const granted = await PermissionsAndroid.request(
          PermissionsAndroid.PERMISSIONS.CAMERA
        );
        if (granted === PermissionsAndroid.RESULTS.GRANTED) {
          resolve(true);
        } else {
          reject("Camera permission denied");
        }
      }
    } catch (error) {
      reject(error);
    }
  });
};

import { useCameraPermission } from "../../hooks/useCamera";

const onButtonPress = React.useCallback(async (type, _options) => {
  try {
    const options = {
      ..._options,
      quality: generalConfig?.imageQuality,
    };
    if (type === "capture") {
      const response = await useCameraPermission();
      if (response) launchCamera(options, handleSetResponse);
    } else {
      launchImageLibrary(options, handleSetResponse);
    }
  } catch (error) {
    console.warn(error);
  }
}, []);

const handleSetResponse = (res: any) => {
  const { assets, didCancel } = res;

  if (didCancel) {
    handleModalClose();
  }

  // file count validation
  let finalAsset = [];
  if (assets && assets?.length > 0) {
    if (assets.length > 2 - props?.len) {
      Alert.alert(
        `You can select max ${2 - props?.len} image only please try again`
      );
      return;
    }

    for (let i = 0; i < assets?.length; i++) {
      //2e6 is 2mb limit of an image
      const maxSizeLimit = 5000000;
      Alert.alert(
        `assets[i]?.fileSize in kbs ${assets[i]?.fileSize / 1000}kbs`
      );
      if (assets[i]?.fileSize > maxSizeLimit) {
        showToast(t("RECEIPT_MAX_SIZE_REACHED_ERROR"), "danger");
      } else {
        finalAsset.push(assets[i]);
      }
      handleModalClose();
    }
  }

  assets?.length > 0 && uploadAttachmentCB(finalAsset);
};
```

#### Animation in react native.

**Flatlist animation in react native**

https://www.youtube.com/watch?v=V2FEEgeEk_o&ab_channel=BrunoOliveira

https://start-react-native.dev/

animation in react native from one point to another
How to change Text in Animation in react-native?

ConnectingActivityLoader.tsx

```jsx showLineNumbers
import React, { useEffect, useRef, useState } from "react";
import { Image, View } from "react-native";
import { BlackCircleIcon } from "../../assets/images";

export const ConnectingActivityLoader = () => {
  const initialState = 0;
  const [dotCount, setDotCount] = useState(initialState);

  const counterRef = useRef(initialState);

  useEffect(() => {
    counterRef.current = dotCount;
  });

  useEffect(() => {
    const _setInterval = setInterval(() => {
      setDotCount(counterRef.current + 1);
      if (counterRef.current >= 9) setDotCount(initialState);
    }, 200);
    return () => clearInterval(_setInterval);
  }, []);

  return (
    <View
      style={{
        flex: 1,
        marginHorizontal: 10,
        flexDirection: "row",
        alignItems: "center",
        overflow: "hidden",
      }}
    >
      {Array.from({ length: dotCount }).map((item, index) => (
        <Image
          key={index}
          source={BlackCircleIcon}
          style={{ width: 5, height: 5, marginHorizontal: 3 }}
        />
      ))}
    </View>
  );
};

Usage: return <ConnectingActivityLoader />;
```

**How to animate a Single View one by one in react native?**

move from one point to another in x or y axis animation in react native?
Sol:

https://snack.expo.dev/rJjzdKC04
https://stackoverflow.com/questions/56561761/how-to-animate-a-single-view-one-by-one-in-react-native

**useReducer in react hooks.**

Its just use to access state and dispatch of a reducer we can pass root reducer in it to access all actions and states in reducer.

![IMAGE](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image131.png)

https://reactjs.org/docs/hooks-reference.html#usereducer

![IMAGE](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image132.png)

**mobile screen sharing in ubuntu**

how to use vyson in ubuntu

```bash showLineNumbers
sudo apt install scrcpy
```

https://www.codegrepper.com/code-examples/shell/install+vysor+on+ubuntu+20.04

**Animation in react native:**

https://docs.google.com/document/d/1ATI-NfzgOQjMUpek-yOtH-GxuGAQsXgYxfj3zqKKBpw/edit

**How to generate QR code in react native ?**

Generation of QR Code in React Native is very easy as we just have to install react-native-svg and react-native-qrcode-svg package, which will provide `<QRCode/>` components to make QRCode. QR Code is known as Quick Response Code is a trademark for a two-dimensional barcode.

https://aboutreact.com/generation-of-qr-code-in-react-native/#:~:text=Generation%20of%20QR%20Code%20in%20React%20Native%20is%20very%20easy,for%20a%20two%2Ddimensional%20barcode.

**React-native-qrcode-svg (recommended)**

https://www.npmjs.com/package/react-native-qrcode-svg

1. react-native-qrcode-svg : This is the best solution I found and works like charm, so I decided to move ahead with this.

**react-native-qrcode-image worked but with some work around as its using few updated**

internal dependency that’s not updated. (Not recommended
https://medium.com/@mushtaque87/qrcode-generator-for-react-native-391ae401e275

React-native-qrcode (not recommended)
https://www.npmjs.com/package/react-native-qrcode

![IMAGE](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image133.png)

**How to get a versionName in react-native app on Android?**

how to get version name in react native

I've successfully used the React Native Device Info component to get the build details as specified in the Gradle config.
Once installed you can use:
DeviceInfo.getVersion()
To output the version, and:
DeviceInfo.getBuildNumber()
To get the build number.

**React-native-device-info**

Device Information for React Native iOS and Android
https://www.npmjs.com/package/react-native-device-info
https://stackoverflow.com/questions/38240859/how-to-get-a-versionname-in-react-native-app-on-android

**Very usefull package features:**

If you want to check if any specific app is installed on your device or not.

No need for these extra packages when using these packages
React-native-share

```jsx showLineNumbers

Example / Usage of Text (Share)
var SendIntentAndroid = require("react-native-send-intent");


SendIntentAndroid.sendText({
  title: "Please share this text",
  text: "This is the description text of the title",
  type: SendIntentAndroid.TEXT_PLAIN,
});


Example / Usage of Send Mail (text/plain only)
var SendIntentAndroid = require("react-native-send-intent");

SendIntentAndroid.sendMail("your@address.com", "Subject test", "Test body");
Example / Usage of SMS
Thanks to @pedro ;)

var SendIntentAndroid = require("react-native-send-intent");

SendIntentAndroid.sendSms("+55 48 9999-9999", "SMS body text here");
Example / Usage of Phone Calls
It's very important ask for permission in your AndroidManifest.xml file if you need to use Phone Calls directly. You can add an optional second parameter, to fix the default phone app.

Please add this line to your AndroidManifest.xml before using this example:

<uses-permission android:name="android.permission.CALL_PHONE" />
And them you can call in your JavaScript files:

var SendIntentAndroid = require("react-native-send-intent");

SendIntentAndroid.sendPhoneCall("+55 48 9999-9999", true);
Example / Usage of Phone Dial Screen
For this use you doesn't need to ask any permission. You can add an optional second parameter, to fix the default phone app.

var SendIntentAndroid = require("react-native-send-intent");

SendIntentAndroid.sendPhoneDial("+55 48 9999-9999", false);
Example / Create Calendar Event
According to Google using Intents for inserting, updating, and viewing calendar events is the preferred method. At this time only simple recurrence is supported ['daily'|'weekly'|'monthly'|'yearly'].

Create a Calendar Event:

// Create the Calendar Intent.
SendIntentAndroid.addCalendarEvent({
  title: "Go To The Park",
  description: "It's fun to play at the park.",
  startDate: "2016-01-25 10:00",
  endDate: "2016-01-25 11:00",
  recurrence: "weekly",
  location: "The Park",
});
Example / Check if an application is installed
Check if Gmail app is intalled. Returns a promise with a boolean telling if the app is installed or not.

SendIntentAndroid.isAppInstalled("com.google.android.gm").then(isInstalled => {});
Example / Install a remote APK
This can be used to upgrade your APK from a custom source or install other apps. No additional permissions are required.

SendIntentAndroid.installRemoteApp("https://example.com/my-app.apk", "my-saved-app.apk").then(installWasStarted => {});
Example / Open App
Open Gmail app. Returns a promise with a boolean telling if the app was opened or not:

SendIntentAndroid.openApp("com.google.android.gm").then(wasOpened => {});

// You can also specify arbitrary intent extras to be passed to the app
SendIntentAndroid.openApp("com.mycorp.myapp", {
  "com.mycorp.myapp.reason": "just because",
  "com.mycorp.myapp.data": "must be a string",
}).then(wasOpened => {});
Example / Open App with Data
Opens MX Player (Free) app and starts a video at the 1 minute mark. Returns a promise with a boolean telling if the app was opened or not:

SendIntentAndroid.openAppWithData(
  "com.mxtech.videoplayer.ad",
  "http://download.blender.org/peach/bigbuckbunny_movies/big_buck_bunny_480p_surround-fix.avi",
  "video/*",
  {
    position: { type: "int", value: 60 },
  }
).then(wasOpened => {});
Example / Open Chrome Intent
Opens Chrome intent as defined in https://developer.chrome.com/multidevice/android/intents

Returns a promise with a boolean.

True if: the intent was handled by an activity or the browser opened the browser_fallback_url

False if both conditions are not fulfilled

SendIntentAndroid.openChromeIntent("intent://www.spm.com/qrlogin#Intent;scheme=https;package=example.package;S.browser_fallback_url=https://www.spm.com/download;end",
  }
).then((wasOpened) => {});
Example / Open Calendar
SendIntentAndroid.openCalendar();
Example / Open Camera Intent
SendIntentAndroid.openCamera();
Example / Open Email Application
Will open default Email application

SendIntentAndroid.openEmailApp();
Will open all the Email app's that available in device

SendIntentAndroid.openAllEmailApp();
Example / Open Download Manager
SendIntentAndroid.openDownloadManager();
Example / Open Share With dialog
Opens Androids default share tray:

// Create Share With dialog.
SendIntentAndroid.openChooserWithOptions(
  {
    subject: "Story Title",
    text: "Message Body",
  },
  "Share Story"
);

SendIntentAndroid.openChooserWithOptions(
  {
    subject: "Video Title",
    videoUrl: "/path_or_url/to/video.mp4",
  },
  "Share video to"
);
Example / Open Multiple Files Share With dialog
Opens Androids default share tray:

// Create Multiple Files Share With dialog.
SendIntentAndroid.openChooserWithMultipleOptions(
  [
    {
      subject: "Video One Title",
      videoUrl: "/path_or_url/to/video.mp4",
    },
    {
      subject: "Video Two Title",
      videoUrl: "/path_or_url/to/video2.mp4",
    },
  ],
  "Share videos to"
);

SendIntentAndroid.openChooserWithMultipleOptions(
  [
    {
      subject: "Video Title",
      text: "Test shared with video",
    },
    {
      subject: "Video Title",
      videoUrl: "/path_or_url/to/video.mp4",
    },
  ],
  "Share video to"
);
Example / Open Maps
Opens Androids default maps app with location:

// Open Maps App
SendIntentAndroid.openMaps("Piccadilly Circus Station, London, United Kingdom");
Example / Open Maps With Route
Opens Androids default maps app, and route path between your location and address:

mode: d,w,b

d: drive car
w: walking
b: bicycle
SendIntentAndroid.openMapsWithRoute("Piccadilly Circus Station, London, United Kingdom", "w");
Example / Share text to line
SendIntentAndroid.isAppInstalled("jp.naver.line.android").then(function (isInstalled) {
  if (!isInstalled) {
    //LINE has not install, you need to install it!
    return;
  }

  SendIntentAndroid.shareTextToLine({ text: "txt message that you want to share" });
});
When you call SendIntentAndroid.shareTextToLine this method, app will bring txt message to LINE, and you can select one or multiple friends to share.

Example / Share Image to Instagram
import { CameraRoll } from "react-native";

//get frist image from CameraRoll
CameraRoll.getPhotos({ first: 1 }).then(
  function (data) {
    const assets = data.edges;

    SendIntentAndroid.isAppInstalled("com.instagram.android").then(function (isInstalled) {
      if (!isInstalled) {
        //Instagram has not install
        return;
      }

      SendIntentAndroid.shareImageToInstagram("image/*", encodeURI(assets[0].node.image.uri));
    });
  },
  function (err) {
    console.error("An error occurred", err);
  }
);
Share your first image from CameraRoll to Instagram.

Example / Open Settings
Opens a specified settings screen when passed one of the constant values available in android.provider.settings (use the constant value found here to open the Security Settings screen).

SendIntentAndroid.openSettings("android.settings.SECURITY_SETTINGS");
Example / Get voiceMail number
Please add this line to your AndroidManifest.xml file before using next example:

  <uses-permission android:name="android.permission.READ_PHONE_STATE" />
SendIntentAndroid.getVoiceMailNumber().then(voiceMailNumber => {
  if (!voiceMailNumber) {
    return console.error("Can`t get voiceMailNumber");
  }

  //if u want to use next line, u need to add CALL_PHONE permission
  SendIntentAndroid.sendPhoneCall(voiceMailNumber);
});
Example / Open File Chooser
Opens Android chooser so the user can select which app will handle the file.

SendIntentAndroid.openFileChooser(
  {
    subject: "File subject", //optional,
    fileUrl: "/path_or_url/to/file",
    type: "file_mimetype",
  },
  "Open file with:"
);
Example / Open File Picker
Opens Android own file selector to get the selected file and callback path from Uri

SendIntentAndroid.openFilePicker(
  {
    type: "file_mimetype", //default is "*/*"
    title: "selector title", //default is "Choose File"
  },
  filePath => {}
);
Example / Get phone number
Please add these lines to your AndroidManifest.xml file before using next example:

  <uses-permission android:name="android.permission.READ_PHONE_STATE" />
  <uses-permission android:name="android.permission.READ_PHONE_NUMBERS" />
SendIntentAndroid.getPhoneNumber().then(phoneNumber => {
  if (!phoneNumber) {
    return console.error("Can`t get phoneNumber");
  }

  //do something with number
});
Example / Request 'ignore battery optimizations'
Please add this line to your AndroidManifest.xml file before using next example:

  <uses-permission android:name="android.permission.REQUEST_IGNORE_BATTERY_OPTIMIZATIONS"/>
Prompts the user to add your app to the Doze and App Standby optimizations exception white-list. Returns true if running on Android version M and greater, if the app is not on the white-list, and the intent was successfully shown. Will only show on Android version M and greater. For more details look here.

SendIntentAndroid.requestIgnoreBatteryOptimizations().then(intentShown => {});
Example / Show battery optimizations settings
Will only show on Android version M and greater. For more details look here.

SendIntentAndroid.showIgnoreBatteryOptimizationsSettings();

```

**react-native-send-intent**

https://www.npmjs.com/package/react-native-send-intent

```jsx showLineNumbers
import SendIntentAndroid from "react-native-send-intent";

SendIntentAndroid.sendText({
  title: "Please share this text",
  text: "This is the description text of the title",
  type: SendIntentAndroid.TEXT_PLAIN,
});
```

Package.json of Hisaab project at 26 Feb 2022

```jsx showLineNumbers
{
 "name": "hisaab",
 "version": "0.0.1",
 "private": true,
 "scripts": {
   "android": "react-native run-android",
   "ios": "react-native run-ios",
   "start": "react-native start",
   "start-reset-cache": "react-native start --reset-cache",
   "test": "jest",
   "lint": "eslint .",
   "build": "cd android && ./gradlew assembleRelease",
   "postinstall": "patch-package",
   "build:release": "npx react-native run-android --variant=release",
   "bundle:release": "cd android && ./gradlew bundleRelease"
 },
 "dependencies": {
   "@babel/plugin-proposal-decorators": "^7.16.5",
   "@gorhom/bottom-sheet": "^4.1.5",
   "@gorhom/portal": "^1.0.12",
   "@react-native-async-storage/async-storage": "^1.15.14",
   "@react-native-community/clipboard": "^1.5.1",
   "@react-native-community/datetimepicker": "^5.1.0",
   "@react-native-community/netinfo": "^7.1.7",
   "@react-native-firebase/analytics": "^14.4.0",
   "@react-native-firebase/app": "^14.2.2",
   "@react-native-firebase/messaging": "^14.2.2",
   "@react-navigation/bottom-tabs": "^6.0.9",
   "@react-navigation/material-top-tabs": "^6.0.6",
   "@react-navigation/native": "^6.0.6",
   "@react-navigation/native-stack": "^6.2.5",
   "@react-navigation/stack": "^6.0.11",
   "@redux-offline/redux-offline": "^2.6.0-native.1",
   "@sentry/react-native": "^3.2.10",
   "@twotalltotems/react-native-otp-input": "1.3.5",
   "@types/node": "^17.0.2",
   "@types/numeral": "^2.0.2",
   "@types/react-native-vector-icons": "^6.4.10",
   "@types/styled-components": "^5.1.17",
   "appcenter": "4.3.0",
   "appcenter-analytics": "4.3.0",
   "appcenter-crashes": "4.3.0",
   "axios": "^0.24.0",
   "babel-plugin-transform-typescript-metadata": "^0.3.2",
   "big-js": "^3.1.3",
   "fbjs": "^3.0.4",
   "google-libphonenumber": "^3.2.25",
   "i18next": "^21.5.4",
   "immer": "^9.0.12",
   "jslint-configs": "^3.0.0",
   "moment": "^2.29.1",
   "native-base": "^3.2.2",
   "numeral": "^2.0.6",
   "patch-package": "^6.4.7",
   "react": "17.0.2",
   "react-i18next": "^11.14.3",
   "react-native": "0.66.3",
   "react-native-background-timer": "^2.4.1",
   "react-native-blob-util": "^0.14.0",
   "react-native-contacts": "^7.0.2",
   "react-native-country-picker-modal": "^2.0.0",
   "react-native-daterange-picker": "^1.5.1",
   "react-native-dotenv": "^3.3.1",
   "react-native-file-viewer": "^2.1.5",
   "react-native-gesture-handler": "^2.1.0",
   "react-native-image-picker": "^4.6.0",
   "react-native-linear-gradient": "^2.5.6",
   "react-native-network-logger": "^1.12.0",
   "react-native-pager-view": "^5.4.9",
   "react-native-push-notification": "^8.1.1",
   "react-native-reanimated": "2.2.4",
   "react-native-rename": "^2.9.0",
   "react-native-responsive-screen": "^1.4.2",
   "react-native-restart": "0.0.23",
   "react-native-safe-area-context": "^3.3.2",
   "react-native-screens": "^3.9.0",
   "react-native-sqlite-storage": "^6.0.1",
   "react-native-svg": "^12.1.1",
   "react-native-svg-transformer": "^0.14.3",
   "react-native-tab-view": "^3.1.1",
   "react-native-vector-icons": "^9.0.0",
   "react-native-version-check": "^3.4.2",
   "react-redux": "^7.2.6",
   "redux": "^4.1.2",
   "redux-saga": "^1.1.3",
   "rn-fetch-blob": "^0.12.0",
   "styled-components": "^5.3.3",
   "typeorm": "^0.2.41"
 },
 "devDependencies": {
   "@babel/core": "^7.12.9",
   "@babel/runtime": "^7.12.5",
   "@react-native-community/eslint-config": "^2.0.0",
   "@types/google-libphonenumber": "^7.4.23",
   "@types/jest": "^27.0.3",
   "@types/react": "^17.0.37",
   "@types/react-native": "^0.66.6",
   "@types/react-native-dotenv": "^0.2.0",
   "@types/react-native-sqlite-storage": "^5.0.1",
   "@types/react-test-renderer": "^17.0.1",
   "@types/styled-components-react-native": "^5.1.3",
   "@typescript-eslint/eslint-plugin": "^5.5.0",
   "@typescript-eslint/parser": "^5.5.0",
   "babel-jest": "^26.6.3",
   "eslint": "^7.14.0",
   "eslint-config-prettier": "^8.3.0",
   "jest": "^26.6.3",
   "metro-react-native-babel-preset": "^0.66.2",
   "prettier": "2.5.0",
   "react-test-renderer": "17.0.2",
   "redux-logger": "^3.0.6",
   "typescript": "^4.5.2"
 },
 "jest": {
   "preset": "react-native"
 }
}
```

**How To Install Java with Apt on Ubuntu 22.04**

how to install java in ubuntu using terminal

https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-22-04

Colors.xml example in react native

https://stackoverflow.com/questions/39157134/grey-square-as-notification-icon-using-firebase-notifications/40232181#40232181

https://redux-toolkit.js.org/introduction/getting-started
https://www.npmjs.com/package/@reduxjs/toolkit

**Reduce/Optimize React Native App Size**

Reduce React Native App Size !

In this video you will learn how to optimize or reduce react native app size,

You may have noticed that even a simple app in react native reaches more than 30mb in size that is really a pain, so here we go this is the perfect video for you if you are also suffering from big sizes !!!!

In this video i have reduced APPP size from 60MB to 17MB,
The app is even live on playstore you can download try it:
https://play.google.com/store/apps/de...

Seneca Manu
3 years ago
Tldr:

1. Compress assets
2. Enable proguard release build to true (5:56)

https://www.youtube.com/watch?v=W7boJmA7xJA&ab_channel=KashanHaider

**Reduce App Size for RN Android Apps**

Enable Proguard

Solution 1
android/app/build.gradle

```jsx showLineNumbers
/**
* Run Proguard to shrink the Java bytecode in release builds.
*/
def enableProguardInReleaseBuilds = true
```

https://reactnative.dev/docs/signed-apk-android#enabling-proguard-to-reduce-the-size-of-the-apk-optional
Expiring Daemon because JVM heap space is exhausted
//gradle.properties add in last

```jsx showLineNumbers
org.gradle.daemon = true;
org.gradle.jvmargs = -Xmx2560m;
```

https://stackoverflow.com/questions/56075455/expiring-daemon-because-jvm-heap-space-is-exhausted

**Solution 2**

Proguard is used to shrink, optimize, obfuscate, and preverify class files. it detects and eliminates unused classes, methods and attributes and rename the remaining ones using short and meaningless names. It compresses the Java Bytecode and reduces the size of the app a little bit.
To enable it use the following command in android/app/build.gradle:
`def enableProguardInReleaseBuilds = true`

**Enable Separate Builds**

This is the alternative of Android App Bundle (.aab). If we do not want to generate aab and stick with apk then this is the way to reduce sizes. Basically 2 major architectures, armeabi & x86, are supported by Android devices. When APK is generated via React Native, it contains the native libraries of both the architectures. In order to generate 2 different APKs use the following command:
To enable it use the following command in android/app/build.gradle:
`def enableSeparateBuildPerCPUArchitecture = true`

**ERROR WHEN MAKING SIGNED APK**

Issue when enable def enableProguardInReleaseBuilds = true in android/app/build.gradle and create signed apk the app crashes when opening

Errorjava.lang.NoSuchFieldException: fill

Solution:

add this line in proguard-rules.pro

`-keep public class com.horcrux.svg.* {;}`

Reference:

https://github.com/react-native-svg/react-native-svg/issues/1061

**Package for google sign in react native**

`$ npm i @react-native-community/google-signin `

https://www.npmjs.com/package/@react-native-google-signin/google-signin

Bilal haded used this package in hope accelerated projects.

Try new Android apps before their official release
To get user feedback, some developers make new apps or features available before their official release. You can try these apps or features when you join early access or beta programs.
https://support.google.com/googleplay/answer/7003180?hl=en

#### AB testing in react native

![ab testing](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image134.png)

**How to clean Android Build Cache**

Go to root directly of your react native project and run following commands:
cd android &&
./gradlew cleanBuildCache
https://medium.com/@abhisheknalwaya/how-to-clear-react-native-cache-c435c258834e

**How to force update version in react native**

Zubair Mehboob 7:16 PM
Done:
Integrated package react-native-version-check
This package is checking app version by app id (becasue app id is unique and you can see app id in app playsore url) on playstore we don’t have to configure anything by ourself just insall and use this package and worked well in hisaab project

And it will not show correct version update modal in dev build but it will work fine on app that is installed from playstore don’t worked on application installed by installing from apk file on device

Created custom hook useBuildInfo to get the information related to local build and the build on play store
Develop Modal for force update version
Conditional rending in App.tsx

```jsx showLineNumbers
import * as React from "react";
import { Variable } from "../constants";
import { Platform } from "react-native";
import VersionCheck from "react-native-version-check";
const useBuildInfo = () => {
  const [country, setCountry] = React.useState("");
  const [latestVersion, setLatestVersion] = React.useState("");
  const [currentVersion, setCurrentVersion] = React.useState("");
  const [needUpdate, setNeedUpdate] = React.useState(false);
  const [currentBuildNumber, setCurrentBuildNumber] = React.useState("0.0.0");
  const [packageName, setPackageName] = React.useState("");
  const getInfo = async () => {
    try {
      let country = await VersionCheck.getCountry();
      /**
       * UNCOMMENT ONCE APP IS DEPLOYED ON PLAY STORE
       */
      // let latestVersion = await VersionCheck.getLatestVersion({
      //  provider:
      //      Platform.OS === Variable.ANDROID ? Variable.PROVIDER.ANDROID : Variable.PROVIDER.IOS,
      // });
      // let needUpdate = await VersionCheck.needUpdate();
      let currentVersion = await VersionCheck.getCurrentVersion();
      let currentBuildNumber = await VersionCheck.getCurrentBuildNumber();
      let packageName = await VersionCheck.getPackageName();
      setCountry(country);
      /**
       * UNCOMMENT ONCE APP IS DEPLOYED ON PLAY STORE
       */
      // setLatestVersion(latestVersion);
      // setNeedUpdate(needUpdate);
      setCurrentVersion(currentVersion);
      setCurrentBuildNumber(currentBuildNumber);
      setPackageName(packageName);
    } catch (err) {
      console.warn(err);
    }
  };

  React.useEffect(() => {
    getInfo();
  }, []);

  return {
    country,
    latestVersion,
    currentVersion,
    needUpdate,
    currentBuildNumber,
    packageName,
  };
};

export default useBuildInfo;
```

Usage

```jsx showLineNumbers
import { useBuildInfo } from "./hooks";

const {
  country,
  latestVersion,
  currentVersion,
  needUpdate,
  currentBuildNumber,
  packageName,
} = useBuildInfo();
```

Constants:

```jsx showLineNumbers
PROVIDER: {
		ANDROID: 'playStore',
		IOS: 'appStore',
	},
	RETAILO_PLAYSTORE_URL:
		'https://play.google.com/store/apps/details?id=com.app.retailerapp&hl=en&gl=US',


//new key
	"APP_NEW_VERSION_TEXT": "A new version of the app is released, do you want to install the updated version?",
	"APP_NEW_VERSION_TITLE": "Update Hisaab"


Packages
React-native-version-check

"react-native-version-check": "^3.4.2",

```

**Loader in react native**

Style

```jsx showLineNumbers
loader: {
       position: 'absolute',
       left: 0,
       right: 0,
       top: 0,
       bottom: 0,
       alignItems: 'center',
       justifyContent: 'center',
       backgroundColor: Colors.GrayOpacity('0.3'),
   },


   const [isLoading, setIsLoading] = React.useState(false);

return(
{/* loader */}
{isLoading && (
    <View style={LoaderStyles.loader}>
        <ActivityLoader color={Colors.Primary} size={60} />
    </View>
)}
)
```

**Loader component in react native (recommended)**

ModalActivityIndicator component:
#overlay loader styling in react native
#modal style in react native

```jsx showLineNumbers
import React from "react";
import { ActivityIndicator, Modal, StyleSheet, View } from "react-native";
import { themeColors } from "../../theme";

const ModalActivityIndicator = () => {
  return (
    <Modal transparent={true} animationType="none">
      <View style={styles.loading}>
        <ActivityIndicator size="large" />
      </View>
    </Modal>
  );
};

export default ModalActivityIndicator;

const styles = StyleSheet.create({
  loading: {
    position: "absolute",
    left: 0,
    right: 0,
    top: 0,
    bottom: 0,
    alignItems: "center",
    justifyContent: "center",
    backgroundColor: themeColors.primaryModalOverlayColor,
  },
});

const themeColors = {
  primary: "#383838",
  primaryModalOverlayColor: "#38383880",
};
```

Usage:

```jsx showLineNumbers
<View style={styles.container}>
  {auth?.isLoading && <ModalActivityIndicator />}

  <AppHeader />
  <Text style={styles.heading1}>Welcome Back!</Text>
  <Text style={GlobalStyles.heading2}>Fill in your account using</Text>
</View>;

export default StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: themeColors.primary,
  },
});
```

https://stackoverflow.com/questions/44046500/how-do-i-overlay-activityindicator-in-react-native
https://www.npmjs.com/package/react-native-loading-spinner-overlay https://medium.com/@kelleyannerose/react-native-activityindicator-for-a-quick-easy-loading-animation-593c06c044dc
https://github.com/kdastan/react-native-modal-loader

**Unique user id generator in react native for make unique file name in react native etc**

Or unique records creation for front end /client side

**react-native-uuid**
https://www.npmjs.com/package/react-native-uuid

Usage :

1. Install
   npm install react-native-uuid
2. Create a UUID
   import uuid from 'react-native-uuid';
   uuid.v4(); // ⇨ '11edc52b-2918-4d71-9058-f7285e29d894'

**Picker component library in react native**

https://www.npmjs.com/package/@react-native-picker/picker

**Top React Native boilerplates for 2021**

https://blog.logrocket.com/top-react-native-boilerplates-for-2021/
https://github.com/thecodingmachine/react-native-boilerplate

example of stack and drawer navigation in react native ||
Example of stack and drawer navigation in react navigation v5 and v6

https://dev.to/easybuoy/combining-stack-tab-drawer-navigations-in-react-native-with-react-navigation-5-da
https://medium.com/wesionary-team/react-navigation-stack-tab-and-drawer-navigation-in-same-react-native-application-16d03441021

I have implemented react-navigation drawer navigation v6 in ArtishNFT APP of hope accelerated.
**Hide header in stack navigator React navigation**

Solution :

```jsx showLineNumbers
<Stack.Navigator
  screenOptions={{
    headerShown: false,
  }}
>
  <Stack.Screen name="route-name" component={ScreenComponent} />
</Stack.Navigator>
```

https://stackoverflow.com/questions/44701245/hide-header-in-stack-navigator-react-navigation

**how to use navigation drawer navigation inside stack navigation in react native ||
Getting Started with React Navigation v5 - Stack, Tabs, Drawer, Authentication (recomended for react navigation v5 and v6)**

https://www.youtube.com/watch?v=nQVCkqvU1uE&ab_channel=ReactNativeSchool
https://github.com/ReactNativeSchool/getting-started-react-navigation-v5 (drawer navigation with stack and tab navigation)
https://reactnavigation.org/docs/drawer-navigator/#drawercontent
https://reactnavigation.org/docs/drawer-based-navigation/

**how to disable drawer on the drawer navigation screen?**

Solution:
You will pass only those screens in drawer in which you want to open drawer and not passing in auth like screens
For code example see my code of Artist NFT app I have write for hope accelerated

**how to update react native version?**

Solution:
Upgrading to new versions :

Run the following command to start the process of upgrading to the latest version:

npx react-native upgrade
You may specify a React Native version by passing an argument, e.g. to upgrade to 0.61.0-rc.0 run:

npx react-native upgrade 0.61.0-rc.0
https://reactnative.dev/docs/upgrading

**Upgrade Helper**

The Upgrade Helper is a web tool to help you out when upgrading your apps by providing the full set of changes happening between any two versions. It also shows comments on specific files to help understanding why that change is needed.
https://react-native-community.github.io/upgrade-helper/
https://stackoverflow.com/questions/53378354/upgrading-react-native-to-latest-version

**useCallback vs useMemo :**

useCallback don’t call function whenever any value change in second parameter but it recreate that function mean define that function
Where as useMemo takes function calling whenever props change in passed child function or component if value change in child function prop it will again call that function passed in first param of React.useMemo(childFunction)
If prop is not changed then its cached and don’t call child function.
https://www.w3schools.com/react/react_usecallback.asp

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image135.png)

https://youtu.be/nQVCkqvU1uE?t=1288

**React.Memo ()** use to pass functional component in its first param React.Memo(App)
React-useMemo() this function use in that function who is passed in React.Memo() like App component/function in above example
To extract the props and state values in child component.

```jsx showLineNumbers
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
//here a, b are state variables


Kanwal, 3:12 PM
import React, { useMemo } from 'react';


const DemoList = (props) => {
  const { items } = props;

  const sortedList = useMemo(() => {
    console.log('Items sorted');
    return items.sort((a, b) => a - b);
  }, [items]);
//here items is state variableor array comes from state of parent component by passing as prop in child component
It means whenever this only items state update in parent component then re render child component otherwise donot re render child component when any other states change in parent component this reduced the extra re rendering effect of react child component.

 console.log('DemoList RUNNING');

  return (
    <div className={classes.list}>
      <h2>{props.title}</h2>
      <ul>
        {sortedList.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </div>
  );
};

export default React.memo(DemoList);
```

**How do I implement shouldComponentUpdate?**

You can wrap a function component with React.memo to shallowly compare its props:

```jsx showLineNumbers
const Button = React.memo((props) => {
  // your component
});
```

https://reactjs.org/docs/hooks-faq.html#how-do-i-implement-shouldcomponentupdate

**When click on back arrow it should close modal react native modal popup
We can handle by this noRequestClose event provided by react native .**

```jsx showLineNumbers
onRequestClose = { handleModal };
```

```jsx showLineNumbers
import React from "react";
import { Modal, TouchableHighlight } from "react-native";
import { Wrapper, StyledTouchable } from "./style";
export const AppModal = ({ modalVisible, handleModal, children }) => {
  return (
    <Modal
      animationType="fade"
      transparent={true}
      visible={modalVisible}
      onRequestClose={handleModal}
    >
      <StyledTouchable activeOpacity={1} onPress={handleModal}>
        <TouchableHighlight>
          <Wrapper>{children}</Wrapper>
        </TouchableHighlight>
      </StyledTouchable>
    </Modal>
  );
};
```

**how to check if stack is empty in react navigation**
how to check screens in stack navigation
how to get navigation state in BackHandler react batuve

...
//E.g., in a button event listener

```jsx showLineNumbers
if (navigation.canGoBack()) {
  navigation.goBack();
}

useEffect(() => {
  BackHandler.addEventListener("hardwareBackPress", handleBackButtonClick);
  return () =>
    BackHandler.removeEventListener("hardwareBackPress", handleBackButtonClick);
});

const [exitApp, setExitApp] = useState(0);

const handleBackButtonClick = () => {
  const { navigation } = props;
  if (!navigation.canGoBack()) {
    setTimeout(() => {
      setExitApp(0);
    }, 2000); // 2 seconds to tap second-time
    if (exitApp === 0) {
      setExitApp(exitApp + 1);
      showToast(t("PRESS_AGAIN_TO_EXIT"));
    } else if (exitApp === 1) {
      BackHandler.exitApp();
    }
    return true;
  }
};
```

Reset state to homescreen when backpress

```jsx showLineNumbers
React.useEffect(() => {
  BackHandler.addEventListener("hardwareBackPress", handleBackButtonClick);
  return () =>
    BackHandler.removeEventListener("hardwareBackPress", handleBackButtonClick);
}, []);

const handleBackButtonClick = () => {
  NavigationService.reset_0("Tabs");
  return true;
};
```

https://stackoverflow.com/questions/45031085/react-native-device-back-button-handling
https://stackoverflow.com/questions/43090884/resetting-the-navigation-stack-for-the-home-screen-react-navigation-and-react-n

**How to get current route name in react-navigation? || get current route name using Navigation service in react navigation || How to get current route name in react-navigation?|| get current screen react navigation?**

For react-navigation v5:

```jsx showLineNumbers
import { useRoute } from "@react-navigation/native";
const route = useRoute();
console.log(route.name);
```

https://stackoverflow.com/questions/53040094/how-to-get-current-route-name-in-react-navigation#:~:text=You%20can%20import%20the%20function,navigators%20in%20React%20Navigation%205.n text=You%20can%20use%20this%20in%20hooks%20as%20well.

**What is the difference between signed and unsigned APKs?**

Unsigned Apk, as the name suggests it means it is not signed by any Keystore. A Keystore is basically a binary file that contains a set of private keys. ... The signed apk is simply the unsigned apk that has been signed via the JDK jarsigner tool.20-Oct-2021

https://www.geeksforgeeks.org/how-to-generate-unsigned-shareable-apk-in-android-studio/

**React-native-pdf**

A react native PDF view component (cross-platform support)

https://stackoverflow.com/questions/35899438/view-a-pdf-in-react-native

**Download file in react native using rn fetch blob package:**

```js showLineNumbers
Package :  "rn-fetch-blob": "^0.12.0",
```

```jsx showLineNumbers
import RNFetchBlob from "rn-fetch-blob";

const actualDownload = (uri) => {
  let sDate = moment(startDate, "YYYY-MM-DD HH:mm:ss").toISOString();
  let eDate = moment(endDate, "YYYY-MM-DD HH:mm:ss").toISOString();
  const { dirs } = RNFetchBlob.fs;
  RNFetchBlob.config({
    fileCache: true,
    addAndroidDownloads: {
      useDownloadManager: true,
      notification: true,
      mediaScannable: true,
      title: `hisaab_transaction_report.pdf`,
      path: `${dirs.DownloadDir}/hisaab_transaction_report.pdf`,
    },
  })
    .fetch(Variable.METHOD.GET, uri)
    .then((res) => {
      console.log("The file saved to ", res, res.path());
    })
    .catch((e) => {
      console.log("Check this Error", e);
    });
};
```

https://stackoverflow.com/questions/56887851/react-native-download-pdf-file-with-rn-fetch-blob-on-click-a-button
https://www.npmjs.com/package/react-native-blob-util

**How to rename a react native app using just one command**

https://www.npmjs.com/package/react-native-rename (Zubair has renamed the project using this package in Hisaab app project of retailo company and run only one commands and the name is renamed of project at all places in just on command.)

react-native-rename NPM version NPM monthly downloads NPM total downloads Paypal Donate
Rename react-native app with just one command

![rename gif](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image136.gif)

https://cloud.githubusercontent.com/assets/5106887/24444940/cbcb0a58-149a-11e7-9714-2c7bf5254b0d.gif

**How to use `setState` callback on react hooks**

304

You need to use useEffect hook to achieve this.

```jsx showLineNumbers
const [counter, setCounter] = useState(0);

const doSomething = () => {
  setCounter(123);
};

useEffect(() => {
  console.log("Do something after counter has changed", counter);
}, [counter]);
```

https://stackoverflow.com/questions/56247433/how-to-use-setstate-callback-on-react-hooks

**component will unmount in functional component**

```jsx showLineNumbers
React.useEffect(() => {
  return () => {
    // Anything in here is fired on component unmount.
  };
}, []);
```

**handle back press in react native**

https://reactnative.dev/docs/backhandler

#backhandler #handleBackPress # onbackpress #hardwareBackPress #double

https://ayusch.com/double-back-button-press-to-exit-in-react-native/
https://snack.expo.dev/HyhD657d7

**React Native: Double back press to Exit App ** ||
Adding BackHandler.addEventListener ||
how to close on second time back press in react native

```jsx showLineNumbers
useEffect(() => {
  BackHandler.addEventListener("hardwareBackPress", handleBackButtonClick);
  return () =>
    BackHandler.removeEventListener("hardwareBackPress", handleBackButtonClick);
});

const [exitApp, setExitApp] = useState(0);

const handleBackButtonClick = () => {
  setTimeout(() => {
    setExitApp(0);
  }, 2000); // 2 seconds to tap second-time

  if (exitApp === 0) {
    setExitApp(exitApp + 1);
    showToast("message");
  } else if (exitApp === 1) {
    BackHandler.exitApp();
  }

  return true;
};
```

https://www.codegrepper.com/code-examples/typescript/React+Native%3A+Double+back+press+to+Exit+App

OR

```jsx showLineNumbers
import React, { Component } from "react";
import {
  BackHandler,
  View,
  Dimensions,
  Animated,
  TouchableOpacity,
  Text,
} from "react-native";

let { width, height } = Dimensions.get("window");

export default class App extends Component<Props> {
  state = {
    backClickCount: 0,
  };

  constructor(props) {
    super(props);

    this.springValue = new Animated.Value(100);
  }

  componentWillMount() {
    BackHandler.addEventListener(
      "hardwareBackPress",
      this.handleBackButton.bind(this)
    );
  }

  componentWillUnmount() {
    BackHandler.removeEventListener(
      "hardwareBackPress",
      this.handleBackButton.bind(this)
    );
  }

  _spring() {
    this.setState({ backClickCount: 1 }, () => {
      Animated.sequence([
        Animated.spring(this.springValue, {
          toValue: -0.15 * height,
          friction: 5,
          duration: 300,
          useNativeDriver: true,
        }),
        Animated.timing(this.springValue, {
          toValue: 100,
          duration: 300,
          useNativeDriver: true,
        }),
      ]).start(() => {
        this.setState({ backClickCount: 0 });
      });
    });
  }

  handleBackButton = () => {
    this.state.backClickCount == 1 ? BackHandler.exitApp() : this._spring();

    return true;
  };

  render() {
    return (
      <View style={styles.container}>
        <Text>container box</Text>

        <Animated.View
          style={[
            styles.animatedView,
            { transform: [{ translateY: this.springValue }] },
          ]}
        >
          <Text style={styles.exitTitleText}>
            press back again to exit the app
          </Text>

          <TouchableOpacity
            activeOpacity={0.9}
            onPress={() => BackHandler.exitApp()}
          >
            <Text style={styles.exitText}>Exit</Text>
          </TouchableOpacity>
        </Animated.View>
      </View>
    );
  }
}

const styles = {
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  animatedView: {
    width,
    backgroundColor: "#0a5386",
    elevation: 2,
    position: "absolute",
    bottom: 0,
    padding: 10,
    justifyContent: "center",
    alignItems: "center",
    flexDirection: "row",
  },
  exitTitleText: {
    textAlign: "center",
    color: "#ffffff",
    marginRight: 10,
  },
  exitText: {
    color: "#e5933a",
    paddingHorizontal: 10,
    paddingVertical: 3,
  },
};
```

https://stackoverflow.com/questions/52253072/react-native-double-back-press-to-exit-app/52253073

**Recommended I have write this code**

```jsx showLineNumbers
useEffect(() => {
  BackHandler.addEventListener("hardwareBackPress", handleBackButtonClick);
  return () =>
    BackHandler.removeEventListener("hardwareBackPress", handleBackButtonClick);
});

const [exitApp, setExitApp] = useState(0);

const handleBackButtonClick = () => {
  const { navigation } = props;
  if (!navigation.canGoBack()) {
    setTimeout(() => {
      setExitApp(0);
    }, 2000); // 2 seconds to tap second-time
    if (exitApp === 0) {
      setExitApp(exitApp + 1);
      showToast(t("PRESS_AGAIN_TO_EXIT"));
    } else if (exitApp === 1) {
      BackHandler.exitApp();
    }
    return true;
  }
};
```

https://stackoverflow.com/questions/54700512/how-to-check-if-goback-function-is-doable-in-react-navigation

**React Native - Device back button handling**
101

```jsx showLineNumbers
   // This example will show you back navigation which is expected generally in most of the flows. You will have to add following code to every screen depending on expected behavior. There are 2 cases: 1. If there are more than 1 screen on stack, device back button will show previous screen. 2. If there is only 1 screen on stack, device back button will exit app.
   // Case 1: Show previous screen

   import { BackHandler } from 'react-native';

   constructor(props) {
       super(props)
       this.handleBackButtonClick = this.handleBackButtonClick.bind(this);
   }

   componentWillMount() {
       BackHandler.addEventListener('hardwareBackPress', this.handleBackButtonClick);
   }

   componentWillUnmount() {
       BackHandler.removeEventListener('hardwareBackPress', this.handleBackButtonClick);
   }

   handleBackButtonClick() {
       this.props.navigation.goBack(null);
       return true;
   }

```

https://stackoverflow.com/questions/45031085/react-native-device-back-button-handling

**React native send a message to specific whatsapp Number**

Send message to user’s WhatsApp number || send message to whatsapp using rect native

```jsx showLineNumbers

3

You can use this method to send whatsApp message direct to a number.

Example link: https://wa.me/919234567812?text=%7B0%7D+Balaji+CTest

export const sendWhatsAppMessage = link => {
if (!isUndefined(link)) {
 Linking.canOpenURL(link)
  .then(supported => {
    if (!supported) {
     Alert.alert(
       'Please install whats app to send direct message to students via whats
        app'
     );
   } else {
     return Linking.openURL(link);
   }
 })
 .catch(err => console.error('An error occurred', err));
} else {
 console.log('sendWhatsAppMessage -----> ', 'message link is undefined');
}
};

```

The above code have some issues like

Alert message showing on some devices even when whatsapp installed in device issue fixed (on some devices works good but on some alert are showing even when whatsapp installed)

Fix
Alert message showing even when whatsapp installed in device issue fixed

```jsx showLineNumbers
export const sendWhatsAppMessage = (link, errorMessage) => {
  if (Boolean(link)) {
    Linking.openURL(link)
      .then((supported) => {
        console.log("supported", supported);
        return Linking.openURL(link);
      })
      .catch((err) => {
        console.error("An error occurred", err);
        Alert.alert(errorMessage);
      });
  } else {
    console.log("sendWhatsAppMessage -----> ", "message link is undefined");
  }
};
```

https://stackoverflow.com/questions/43518482/react-native-send-a-message-to-specific-whatsapp-number
https://aboutreact.com/send-whatsapp-message/

**SafeAreaView**
https://reactnative.dev/docs/safeareaview

**Send sms to native app**

```jsx showLineNumbers
import { Linking, Platform } from "react-native";

const useSendSMS = async (phoneNumber, message) => {
  try {
    const separator = Platform.OS === "ios" ? "&" : "?";
    const url = `sms:${phoneNumber}${separator}body=${message}`;
    await Linking.openURL(url);
  } catch (error) {
    console.log(error);
  }
};

export default useSendSMS;
```

Usage:

```jsx showLineNumbers
useSendSMS(customerState?.customer?.mobile, getCurrentSMS?.message);
```

**DevSettingsActivity permission for reloading react native javascript app in dev mode”**

If you need to access to the DevSettingsActivity add to your AndroidManifest.xml:

```bash showLineNumbers
<activity android:name="com.facebook.react.devsupport.DevSettingsActivity" />
```

This is only used in dev mode when reloading JavaScript from the development server, so you can strip this in release builds if you need to.

On windows:
Cd android && gradlew app:assembleRelease

On mac and linux:
Cd Android && ./gradlew assembleRelease
This above command will make release build by using debug.keystore file that’s why it don’t require my-upload-key.keystore file to make build.

**carousel in react native**

react native image slider

**react-native-snap-carouse**

https://github.com/meliorence/react-native-snap-carousel

https://www.npmjs.com/package/react-native-snap-carousel
https://stackoverflow.com/questions/44050979/react-native-swiper-multiple-images/52246571
https://snack.expo.dev/@vitkor/carousel-simple-example
https://betterprogramming.pub/build-an-image-carousel-in-react-native-5ce5d6b58e24
https://www.npmjs.com/package/react-native-image-slider-box

Using React Native to implement a carousel

https://blog.logrocket.com/using-react-native-to-implement-a-carousel/

react-native-swiper

https://www.npmjs.com/package/react-native-swiper

Issues

**react native swiper not working on ios**

Wrap your listitem in TouchableOpacity
https://github.com/leecade/react-native-swiper/issues/1089

**react native swiper simple**

https://www.npmjs.com/package/react-native-swiper

**Should You Use TypeScript with React Native? [2021]**

https://www.reactnativeschool.com/should-you-use-typescript-with-react-native

how to create react native typescript project
npx react-native init MyApp --template react-native-template-typescript
https://reactnative.dev/docs/typescript

A failure occurred while executing com.android.build.gradle.internal.tasks
307
Finally found a solution for this by adding this line to gradle.properties.
**org.gradle.jvmargs=-Xmx4608m**

Add this line at last of gradle.properties file
https://stackoverflow.com/questions/57606462/a-failure-occurred-while-executing-com-android-build-gradle-internal-tasks

When user make release build using this command

```json showLineNumbers
  "build:release": "npx react-native run-android --variant=release"
```

It will automatically installed app on connected device

**How to change port of react native app OR
React native change listening port**

**how to server of react native to another port**

> How can I run two react native applications?

how to run 2 react native dev apps
react native start not working on different ports
how to serve of react native to another port

Run these 2 command with same port

```bash showLineNumbers
react-native run-ios or react-native run-android --port 8088
Npx react-native run-ios --port 8088
```

Add this line in your package.json and run npm start on terminal

```json showLineNumbers


   "start": "react-native start --port 9988",
or
   "start": "react-native start --port 8082",

```

E.g

```json showLineNumbers

"scripts": {
   "android": "react-native run-android --port 9988",
   "ios": "react-native run-ios",
   "start": "react-native start --port 8082",
   "test": "jest",
   "lint": "eslint ."
 },
```

https://stackoverflow.com/questions/34431052/react-native-change-listening-port
https://stackoverflow.com/questions/51336123/how-can-i-run-two-react-native-applications
https://stackoverflow.com/questions/34431052/react-native-change-listening-port

**React-native-background-timer Package**

Npm i react-native-background-timer.

**What is this package purpose ?**

basically i'm using background-timer to run counter when application is in the background, otherwise it stops the timer when application is in the background.

https://www.npmjs.com/package/react-native-background-timer
https://www.npmjs.com/package/@react-native-community/clipboard
https://stackoverflow.com/questions/55393271/react-native-how-to-auto-fetched-the-otp-in-the-textfield-from-the-mobile-sms-sh/56223148

Before **Patch package** we were doing is that
Hm node_modules se wo package ka code utha kr apni directory main add krte thy phr useko us directory se access kr k use krte thy jo k bad practice that q k agr koi update ati package main to hm uski avail nhe kr sakte thy hr dafa koi update ane pe hamain code ko update krna parhta or jo changes pehle ki thi wo bhe isme change krni parhti manually thats why i though this approach was working but not recommended

**Patch package: (not recommended better is to do custom work or use another package or library which have support from community) only use this as last priority when you dont found any other package or custom work is not possible**

When any package is not working or have to do some custom changes
Alternative to run patch command

```bash showLineNumbers
npx patch-package <library/package name>
npx patch-package react-native-community_datetimepicker
```

Do make changes in goto node_modules and update code according to your need and then
Use patch package to make patch file for your changes

Some code have es6 code work in node_modules while same have compiled version in es5
So you have change only those package whose code is written in es6 because es5 is very hard to understand for human like element is defined as React.createElement in es5 etc

Zubair had done changes in node_modules for

```json showLineNumbers
"react-native-daterange-picker": "^1.5.1",
```

Package its code was written in es6 that’s why zubair made changes in node_modules and make patch file for that package.

But when I try to change "react-native-country-picker-modal": "^2.0.0",
Components of its code were compiled to es5 that’s why its very long process to change native code and make it usable for custom changes. We don't change it but use it as it is provided to us in Hisaab app.

**Layout with Flexbox**

https://reactnative.dev/docs/flexbox
https://reactnative.dev/docs/layout-props

#### Productivity in react native development.

**Can we run one debug build at a time in multiple android devices**

Yes we can
I have open emulator and connect one android device in parallel and run
React-native run-android
This have created 2 build and when i run npm start
Its starting 2 build in same time.

The benefits of running in 2 devices is that
I was working on RTL (right to left flow in localization for support multi language)
So evey time I change something I have to check in both direction when require start from root screens
But when open english mode in simulator and urdu in another real android device My development time reduce to almost half of the time.

And my laptop was hp ProBook-450-G3 (nextgeni-HP-ProBook-450-G3) with 16gb ddr3 ram and 256GB SSD with code i7 7 Gen (Intel® Core™ i7-6500U CPU @ 2.50GHz × 4 )

Its running both devices (android studio emulator and one real android device with usb debugging option) very fast without lagging.

**How to generate Typescript project in react native OR
generate typescript react native project**

Sol :

Just add template keyword at last in reat native init command

```bash showLineNumbers
npx react-native init AwesomeTSProject --template react-native-template-typescript
```

https://reactnative.dev/docs/environment-setup

**how to use react-native-sqlite-storage**

https://aboutreact.com/example-of-sqlite-database-in-react-native/

**Active queue in redux saga when app in offline mode**

https://medium.com/ideas-at-igenius/how-to-use-a-concurrent-task-queue-in-your-redux-sagas-39e598c4fcae
https://redux-saga.js.org/docs/advanced/Channels/
https://stackoverflow.com/questions/67872004/how-to-queue-requests-using-react-redux
E.g https://codesandbox.io/s/hoh8n

#### R&D later :

**mobile-app-offline-data-synchronization/ **

https://www.mindbowser.com/mobile-app-offline-data-synchronization/

17
**Add Contact permission in Info.plist file :**

Key : Privacy - Contacts Usage Description Value : $(PRODUCT_NAME) contact use
See GIF : http://ge.tt/4HOl7ej2
Share
Follow
edited Aug 27 '18 at 6:12
answered Apr 11 '17 at 9:49

Kirit Modi
21.8k14
14 gold badges
85
85 silver badges
108
108 bronze badges
Hi, can you please share the code which can be copy pasted in Plist'ss source code. thanks– Ritesh.mlk Apr 11 '17 at 9:52
Click on the (+) of plist. in first box enter : Privacy - Contacts Usage Description and in second box enter : $(PRODUCT_NAME) contact use. – Kirit Modi Apr 11 '17 at 9:54

https://stackoverflow.com/questions/43342411/the-apps-info-plist-must-contain-an-nscontactsusagedescription

Malformed calls from JS : field sizes are different [[8,39],[4,0]

Issues fixes in react-native-contact
We are fixing for 0.63
https://stackoverflow.com/questions/65222168/malformed-calls-from-js-field-sizes-are-different-8-39-4-0

NPX (node package ship with node)

If you previously installed a global react-native-cli package, please remove it as it may cause unexpected issues.
React Native has a built-in command line interface, which you can use to generate a new project. You can access it without installing anything globally using npx, which ships with Node.js. Let's create a new React Native project called "AwesomeProject":

Naming convension should be alphanumeric for project name any special characters not allowed you can you can use camelcase or pascal case for name of project

npx react-native init hisaab-app
npx: installed 636 in 68.785s
error "hisaab-app" is not a valid name for a project. Please use a valid identifier name (alphanumeric).
https://reactnative.dev/docs/environment-setup

1. Naming Conventions. A folder and sub folder name should always start with small letters and the files belongs the folders is always in pascal case. The term “PascalCase” comes from software development, it may describe any compound word in which the first letter of each word is capitalized.
   https://gilshaan.medium.com/react-native-coding-standards-and-best-practices-5b4b5c9f4076#:~:text=1.,of%20each%20word%20is%20capitalized.

Is there an official style guide or naming convention for React based projects?
https://stackoverflow.com/questions/55221433/is-there-an-official-style-guide-or-naming-convention-for-react-based-projects

We used this package for bottom sheet in react native in hisaab app project of Retailo
/@gorhom/bottom-sheet (I think because of typescript support and stars)
@gorhom/bottom-sheet
https://www.npmjs.com/package/@gorhom/bottom-sheet

Reanimated-bottom-sheet (not used this)
https://www.npmjs.com/package/reanimated-bottom-sheet

'Pressable' refers to a value, but is being used as a type here. Did you mean 'typeof Pressable'?ts(2749)
Solution :
Make sure you're on a .tsx file and not a .ts file
https://stackoverflow.com/questions/62059408/reactjs-and-typescript-refers-to-a-value-but-is-being-used-as-a-type-here-ts?rq=1

**Modal**

Create custom modal fast by using code of this library not intall this package but to use
src=> Modal.tsx file code.

https://github.com/react-native-modal/react-native-modal

**For responsive fontsize and screen in react native**

Options

Write your custom metric file and write normalize fontsize etc functions in it like Zubair have used in different apps (it works good reviews of Zubair)

Code below

```jsx showLineNumbers
//index.tsx

import { Dimensions, PixelRatio, Platform } from "react-native";
import { isIphoneX } from "./isIPhoneX";
import Colors from "../colors";
let { height, width } = Dimensions.get("window");

height -= Platform.OS == "ios" ? (isIphoneX() ? 70 : 20) : 24;

const scale = height / 812;

const normalize = (size: number) => {
  const newSize = size * scale;
  return Math.round(PixelRatio.roundToNearestPixel(newSize));
};

const VerticalSize = (size = 812) => (size / 812) * height;
const HorizontalSize = (size = 375) => (size / 375) * width;
const createShadow = (
  number = 5,
  opacity = 0.2,
  offset = { height: 5 },
  color = Colors.Shadow,
  backgroundColor = "white"
) => {
  return {
    elevation: number,
    shadowOffset: offset,
    shadowOpacity: opacity,
    shadowColor: color,
    backgroundColor,
  };
};
export default {
  Radius: VerticalSize(10),
  LightRadius: VerticalSize(6),
  ActiveOpacity: 0.5,
  customFontSize: normalize,
  FontRegular: normalize(16),
  FontExtraSmall: normalize(12),
  FontSmallest: normalize(10),
  FontSmall: normalize(14),
  FontMedium: normalize(18),
  FontLarge: normalize(22),
  VerticalSize,
  HorizontalSize,
  createShadow,
};
```

```jsx showLineNumbers
import { Dimensions, Platform } from "react-native";
//isIphoneX.ts
export function isIPhoneXSize(dim: any) {
  return dim.height == 812 || dim.width == 812;
}

export function isIPhoneXrSize(dim: any) {
  return dim.height == 896 || dim.width == 896;
}

export function isIphoneX() {
  const dim = Dimensions.get("window");

  return Platform.OS === "ios" && (isIPhoneXSize(dim) || isIPhoneXrSize(dim));
}
```

Another options is use third party libraries
Like
https://www.npmjs.com/package/react-native-responsive-screen

**Difference between .ts and tsx**

Is that .ts is just a simple typescript file which include typescript code
But tsx is typescript + XML (x is for react component because it is XML sugarcated you know)

Search contacts in react-native-contacts

```jsx showLineNumbers
/**
 *
 * @param str
 * @returns
 * @description
 * this handler will search based on matching string either it is name, phonenumber, email etc
 */

export const useSearchContact = (str: string) => {
  // text can be name and phone
  return new Promise((resove, reject) => {
    try {
      const _contacts = Contacts.getContactsMatchingString(str);
      resove(_contacts);
    } catch (error) {
      console.log("error in Contacts.getAll", error);
      reject(error);
    }
  });
};
```

**React-native-contacts:**

A hook for android right now that uses for requesting contact permission from user
Accept and reject cases verified and tested
It returns list of users from your mobile device contacts list

```jsx showLineNumbers
export const useContactPermission = (props: useContactPermissionProps) => {
  return new Promise(async (resolve, reject) => {
    try {
      if (Platform.OS === Variable.IOS) {
        // resolve(FetchContactsfromPhone());
      } else if (Platform.OS === Variable.ANDROID) {
        const permission = await Contacts.checkPermission();
        Contacts.PERMISSION_AUTHORIZED ||
          Contacts.PERMISSION_UNDEFINED ||
          Contacts.PERMISSION_DENIED;

        if (permission === Variable.AUTHORIZED) {
          resolve(FetchContactsfromPhone());
        }

        if (permission === Variable.DENIED) {
          const _permission = await PermissionsAndroid.request(
            PermissionsAndroid.PERMISSIONS.READ_CONTACTS
          );
          if (permission === Variable.AUTHORIZED) {
            resolve(FetchContactsfromPhone());
          }
        }
      }
    } catch (error) {
      reject(error);
    }
  });
};
```

**Rendering svg in React native**

https://www.npmjs.com/package/react-native-svg

**Svg or assets files naming convention in reactjs**

best practice would be
you can name svg in this convention icon-arrow-down.svg
https://graphicdesign.stackexchange.com/questions/108447/icons-assets-naming-conventions

#### Disadvantages/ Logical reasons to not using inline styles in React js

does react caching outline styles :
Yes it some how memoized object literal styles

#### Disadvantages of Inline CSS

- Duplication of CSS properties
- CSS properties will be limited to a component scope only, so there is zero reusability
- We will not be able to utilize the full power of CSS, for example, no pseudo-classes, pseudo-element, media queries, keyframe animations, etc.
- It is hard to maintain or edit/update, and lot of inline CSS can reduce the code readability
- It hampers the performance, on each re-rendering the style object will be recomputed
  https://www.pluralsight.com/guides/react-inline-styling

**Passing objects as props**

Unintentional re-renders not only happen with functions, but also with object literals.

```jsx showLineNumbers
function App() {
  return <Heading style={{ color: "blue" }}>Hello world</Heading>;
}
```

Every time the App component renders a new style object is created, leading the memoized Heading component to update.
Luckily, in this case the style object is always the same, so we can just create it once outside the App component and then re-use it for every render.

```jsx showLineNumbers
const headingStyle = { color: "blue" };
function App() {
  return <Heading style={headingStyle}>Hello world</Heading>;
}
```

But what if the style is calculated dynamically? In that case you can use the `useMemo` hook to limit when the object is updated.

https://www.debugbear.com/blog/react-rerenders

**Hooks FAQ**

https://reactjs.org/docs/hooks-faq.html#how-do-i-implement-shouldcomponentupdate
https://www.w3schools.com/react/react_memo.asp
https://www.w3schools.com/react/react_usememo.asp

**Q. What should be the file extension (style.js or style.jsx) of style file in react native if it uses stylesheet of react native and styled-component**

A. You can name it whatever you want ( styles. js is typical) but be sure the extension is “. js”; it's JavaScript after all.
ye to js keh raha hy LOL.

https://freecontent.manning.com/applying-and-organizing-styles-in-react-native/

styled-components utilises tagged template literals to style your components. It removes the mapping between components and styles. This means that when you're defining your styles, you're actually creating a normal React component, that has your styles attached to it.

**passing props to stylesheet react native**

passing props to stylesheet react native
19

i'm sending noFooter boolean prop in a style sheet

```jsx showLineNumbers
   <View style={styles.mainFooterCont(noFooter)}>
     <Text> Testing </Text>
    </View>
and receiving it like

  mainFooterCont: noFooter => ({
   flexDirection: 'row',
   justifyContent: 'space-between',
   alignItems: 'flex-end',
   paddingBottom: noFooter ? 0 : 20,
   paddingTop: Metrics.ratio(noFooter ? 0 : 5),
   }),
```

https://stackoverflow.com/questions/42707327/passing-props-into-external-stylesheet-in-react-native

**props in styled components in react ntaive**

Props can be available by using function in styled component like this

```jsx showLineNumbers
Color: ${(props)=> props.disabled?red:black}
```

**Ref or createRef() in react native**

Ref (React.createRef()) cannot be pass as props in react ntaive
We have to use forwardRef for accessing ref in child component

Ref hm isliye use krte
Parent ka ref child main access krne k liye use krte hain forwardRef
E.g child se hamain modal close karna ho (when click on outer area) to hm parent ka ref child main access krke close krte hain

E.g
Library is
https://www.npmjs.com/package/@gorhom/bottom-sheet

```jsx showLineNumbers
// Add customer.js (parent component where we import and using bottomsheet  component we are using ref to close the modal when click outside the bottomsheet component )

// BottomSheet refs
const bottomSheetModalRef = React.createRef();

/**
 * Opens BottomSheet
 */
const openBottomSheetModal = () => {
  bottomSheetModalRef.current?.present();
};

/**
 * Close BottomSheet
 */
const closeBottomSheetModal = () => {
  bottomSheetModalRef.current?.close();
};

<BottomSheetContainer
  snapPoint="35%"
  closeBottomSheet={closeBottomSheetModal}
  ref={bottomSheetModalRef}
>
  <MainWrapper>
    <Title>Customer save karain</Title>
    <ContentWrapper>
      <StyledText style="regular" center>
        Kya aap customer save karna chahte hain?
      </StyledText>
    </ContentWrapper>
  </MainWrapper>
  <Footer>
    <AppButton title={t("HAAN")} onPress={() => alert("Pressed!")} />

    <Buttons type="solid" onPress={() => alert("Pressed!")}>
      <StyledText style="medium">Haan</StyledText>
    </Buttons>
    <Buttons type="underlined" onPress={() => alert("Pressed!")}>
      <StyledText style="medium" size="14" color={Colors.Primary} underline>
        Abhi nahi
      </StyledText>
    </Buttons>
  </Footer>
</BottomSheetContainer>;

// BottomSheetContainer.ts

/* eslint-disable react/no-multi-comp */
import React, { useCallback, useRef, useEffect, useMemo } from "react";
import { View, TouchableHighlight } from "react-native";
import Icon from "react-native-vector-icons/FontAwesome";

// BottomSheet imports
import {
  BottomSheetModal,
  BottomSheetModalProvider,
  BottomSheetBackdrop,
  BottomSheetBackdropProps,
} from "@gorhom/bottom-sheet";

// Style imports
import { Container, CloseButton } from "./style";
import colors from "../../theme/colors";

export const BottomSheetContainer = React.forwardRef((props, ref) => {
  // BottomSheetContainer
  /**
   * Watches trigger in BottomSheet
   */
  const handleSheetChanges = useCallback((index: number) => {
    // Todo: Will be removed in coming commits
    console.log("handleSheetChanges", index);
  }, []);

  /**
   * Closes bottom sheet
   */
  const handleClosePress = () => {
    props.closeBottomSheet?.();
  };

  /**
   * Adds backdrop properties
   * @param props
   */
  const renderBackdrop = (props) => (
    <BottomSheetBackdrop
      {...props}
      opacity={0.8}
      disappearsOnIndex={-1}
      appearsOnIndex={0}
      enableTouchThrough={false}
    />
  );

  return (
    <BottomSheetModalProvider>
      <Container>
        <BottomSheetModal
          dismissOnPanDown
          enablePanDownToClose
          backdropComponent={renderBackdrop}
          ref={ref}
          index={0}
          snapPoints={[props.snapPoint ? props.snapPoint : "40%"]}
          onChange={handleSheetChanges}
        >
          <CloseButton onPress={() => handleClosePress()}>
            <View>
              <Icon name="close" size={12} color={"white"} />
            </View>
          </CloseButton>
          <View>{props.children}</View>
        </BottomSheetModal>
      </Container>
    </BottomSheetModalProvider>
  );
});
```

How to close opened keyboard of input box when click on button
Or how to close open keyboard using ref react native

```jsx showLineNumbers

import { Keyboard } from 'react-native';
and in your code could be something like this:

render() {
    return (
      <TextInput
        onSubmit={Keyboard.dismiss}
      />
    );
  }
```

https://stackoverflow.com/questions/29685421/hide-keyboard-in-react-native

**TextInput**

textinput react native
How to make textinput react native scrollable || how to scroll textinput react native
Just give max height 100 to textinput ant multiline enable to true it will work scrollable after max height reached

scrollEnabled iOS
If false, scrolling of the text view will be disabled. The default value is true. Only works with multiline={true}.

TYPE
bool

https://reactnative.dev/docs/textinput

**how to restrict non numeric value to type in react native text input ||
how to restrict text input to only enter numbers in react native ||
React Native TextInput that only accepts numeric characters**

I need to have a React Native TextInput component that will only allow numeric characters (0 - 9) to be entered. I can set the keyboardType to numeric which almost gets me there for input except for the period (.). However this does nothing to stop pasting non-numeric characters into the field.

Solution :

```jsx showLineNumbers
//  141
// Using a RegExp to replace any non digit is faster than using a for loop with a whitelist, like other answers do.
// Use this for your onTextChange handler:

onChanged (text) {
   this.setState({
       mobile: text.replace(/[^0-9]/g, ''),
   });
}
// Performance test here: https://jsperf.com/removing-non-digit-characters-from-a-string

```

E.g:

```jsx showLineNumbers
const onChangePhoneNo = (number: string) => {
  setValidatePhone({ isValid: true, error: "" });
  setPhoneNumber(number);
  const parsedVal = number.replace(/[^0-9]/g, "");
  setPhoneNumber(parsedVal);
};

<PhoneInputTextInputSC
  keyboardType="phone-pad"
  placeholder="3012345678"
  value={phoneNumber}
  onChangeText={onChangePhoneNo}
  maxLength={10}
  isRTL={I18nManager.isRTL}
/>;
```

https://stackoverflow.com/questions/32946793/react-native-textinput-that-only-accepts-numeric-characters
https://gist.github.com/AlexisLeon/80b5641eb30b43bc598288e41052ac39
https://www.codegrepper.com/code-examples/javascript/react+native+text+input+allow+only+numbers

**how to check keyboard is open in react native**

How to detect when keyboard is opened or closed in React Native

Thank you guys for your answers. Here is the hooks version if someone is interested:

```jsx showLineNumbers
const [isKeyboardVisible, setKeyboardVisible] = useState(false);

useEffect(() => {
  const keyboardDidShowListener = Keyboard.addListener(
    "keyboardDidShow",
    () => {
      setKeyboardVisible(true); // or some other action
    }
  );
  const keyboardDidHideListener = Keyboard.addListener(
    "keyboardDidHide",
    () => {
      setKeyboardVisible(false); // or some other action
    }
  );

  return () => {
    keyboardDidHideListener.remove();
    keyboardDidShowListener.remove();
  };
}, []);
```

https://stackoverflow.com/questions/51606099/how-to-detect-when-keyboard-is-opened-or-closed-in-react-native
https://stackoverflow.com/questions/51606099/how-to-detect-when-keyboard-is-opened-or-closed-in-react-native/51606247

**Do this when app ui is adjusting on keyboard open or you have used flex (flex needs to be change with static height) keyboard issues in React Native : **

app UI is jerking when calculator keyboard and custom keyboard switching issue fixed
Or
13 on open native keyboard ui is breaking (UI is breaking when native keyboard opening issue fixed by integrating native keyboard event listener and hide calculation panel work done on active state)
Change this from

```json showLineNumbers
       android:windowSoftInputMode="adjustResize"
```

To

```json showLineNumbers
       android:windowSoftInputMode="adjustPan"
```

https://stackoverflow.com/questions/39344140/react-native-how-to-control-what-keyboard-pushes-up

All countries Phone number validation with country picker implementation in hisaab app

```jsx showLineNumbers
import { Colors, Fonts } from "../../theme";

import {
  ButtonWSC,
  Container,
  DisabledText,
  ErrorText,
  FormField,
  PhoneInputSC,
  PhoneInputTextInputSC,
  Row,
  TextInputSC,
  TitleText,
} from "./style";
import {
  Buttons,
  ContentWrapper,
  Footer,
  MainWrapper,
  Title,
  StyledText,
} from "../../components/FilterCustomers/style";
import { Content } from "../CreateBusiness/style";
import PNF, { PhoneNumberUtil } from "google-libphonenumber";
import CountryPicker from "react-native-country-picker-modal";

//handler
function handleSubmit() {
  closeBottomSheetModal();
  const number = phoneUtil.parseAndKeepRawInput(phoneNumber, countryCode);

  const isValidNumberForRegion = phoneUtil.isValidNumberForRegion(
    phoneUtil.parse(phoneNumber, countryCode),
    countryCode
  );
  if (isValidNumberForRegion) {
    setValidatePhone({ isValid: true, error: "" });
    const internationalNumber = phoneUtil
      .formatOutOfCountryCallingNumber(number)
      .replaceAll(/[^\w\s]/gi, "");
    console.log("internationalNumber", internationalNumber);
    Alert.alert(`internationalNumber ${internationalNumber}`);
  } else {
    setValidatePhone({ isValid: false, error: "Invalid phone number" });
  }
  resetState();
}

//in render
<FormField>
  <Row>
    <TitleText>{t("CUSTOMER_KA_NUMBER")}</TitleText>
    <DisabledText>({t("OPTIONAL")})</DisabledText>
  </Row>
  <PhoneInputSC>
    <CountryPicker
      theme={{
        fontFamily: Fonts["Inter-Medium"],
        fontSize: 16,
        color: "red",
      }}
      countryCode={countryCode}
      onSelect={onChangeCountryCode}
      withFilter
      withFlag
      withCallingCode
      withCallingCodeButton
      withAlphaFilter
      withEmoji
    />
    <PhoneInputTextInputSC
      keyboardType="number-pad"
      placeholder="3012345678"
      value={phoneNumber}
      onChangeText={onChangePhoneNo}
    />
  </PhoneInputSC>
  {!validatePhone.isValid && <ErrorText>{validatePhone?.error}</ErrorText>}
</FormField>;
```

**How can i change the header modal placeholder value "Enter country name"? #306
OR Cant find the filter textinput placeholder #237**

Solution :

```jsx showLineNumbers
filterProps={{
   placeholder: 'place holder text'
}}
```

https://github.com/xcarpentier/react-native-country-picker-modal/issues/237
https://github.com/xcarpentier/react-native-country-picker-modal/issues/306

**R&D for country code and phone number validation in react native**

add selectedCountries and excludeCountries?? #281

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image137.png)

https://github.com/xcarpentier/react-native-country-picker-modal/issues?q=is%3Aissue+list
https://github.com/xcarpentier/react-native-country-picker-modal/issues/281
https://github.com/xcarpentier/react-native-country-picker-modal#props

**phone validation in RN**

https://stackoverflow.com/questions/50441460/react-native-mobile-number-validation-accept-numeric-value-only

https://www.npmjs.com/package/react-native-country-picker-modal
REPO: https://github.com/xcarpentier/react-native-country-picker-modal
usage : https://gist.github.com/haydenbleasel/ff4b8eb40543364d937301a588284c34
Demo: https://reactnative.gallery/xcarpentier/country-picker
https://github.com/google/libphonenumber
https://www.npmjs.com/package/google-libphonenumber

not using
https://www.npmjs.com/package/react-native-phone-input
https://github.com/thegamenicorus/react-native-phone-input

https://www.npmjs.com/package/react-phone-number-input
https://catamphetamine.gitlab.io/react-phone-number-input/
https://www.npmjs.com/package/react-native-phone-number-input
https://www.npmjs.com/package/phone

multi country phone number validation in react native
React Native: mobile number validation accept numeric value only

Error fixes
https://github.com/xcarpentier/react-native-country-picker-modal/issues/334

![IMAGE](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image138.png)
![IMAGE](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image139.png)

**Q.can we share async storage across different apps (Is AsyncStorage shared across apps? - Stack Overflow)**

1 Answer. AsyncStorage is not shared between multiple apps. Every app runs it it's own sandbox environment and has no access to other apps.14-Feb-2018

**Could not find a declaration file for module 'module-name'. '/path/to/module-name.js' implicitly has an 'any' type**

https://stackoverflow.com/questions/41292559/could-not-find-a-declaration-file-for-module-module-name-path-to-module-nam

**RTL right to left in React native based on selected language**

2 approaches to achieve this

1. flex-direction row-reverse (based on language change we will be maintaining a key RTL :true/false in redux which tells which style to apply. (its very long process)
2. Right-to-Left Layout Support For React Native Apps (short approach first do a small POC and its recommended because it is time saving)

https://reactnative.dev/blog/2016/08/19/right-to-left-support-for-react-native-apps

#### REACT native bugs fixes

**Could not resolve all files for configuration ':app:debugRuntimeClasspath' react native**

OR
**Received status code 502 from server: Bad Gateway #24082**

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image140.png)

https://status.bintray.com/ 502 Bad Gateway
https://github.com/facebook/react-native/issues/24082

**jcenter is having issues at the moment, please check http://status.bintray.com/**
https://stackoverflow.com/questions/49510176/android-studio-gradle-sync-failed-could-not-head-received-status-code-5

**PDF downloading from url work in react native**

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image141.png)

#### React navigation:

Stack with tab navigation in react native zubair have done in hisaab app
navigation between stack and tab navigation in react native
For moving between stack to tab navigation we use jump to not navigation.navigate. In tab navigation

```jsx showLineNumbers
import React from "react";
import { createStackNavigator } from "@react-navigation/stack";
import { InitialStack, AuthStack, HomeStack, AccountStack } from "./stack";
import { TabNavigator } from "./tab";

export const MainStack = () => {
  const MainStack = createStackNavigator();
  const AppStacks = [
    ...InitialStack,
    ...AuthStack,
    ...HomeStack,
    ...AccountStack,
  ];
  return (
    <MainStack.Navigator
      initialRouteName={"Splash"}
      screenOptions={{
        headerShown: false,
      }}
    >
      {AppStacks.map((stack) => (
        <MainStack.Screen {...stack} />
      ))}
      <MainStack.Screen component={TabNavigator} name="Tabs" />
    </MainStack.Navigator>
  );
};
```

```jsx showLineNumbers
import React from "react";
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
import { Home, Account, CashBook } from "../../screens";
import { Colors, Metrix } from "../../theme";
import { HomeSvg, ProfileSvg, CahsSvg, CreditSvg } from "../../assets/svg";

import { style } from "./style";
import { useTranslation } from "react-i18next";
import { Variable } from "../../constants";
const Tab = createBottomTabNavigator();

type Screen = {
  Home: React.FC,
  CashBook: React.FC,
  Account: React.FC,
};
const Screens: Screen = { Home, CashBook, Account };

export const TabNavigator = () => {
  const { t } = useTranslation();
  return (
    <Tab.Navigator
      initialRouteName={Variable.SCREENS.HOME}
      screenOptions={{
        tabBarActiveTintColor: Colors.Primary,
        tabBarInactiveTintColor: Colors.Disabled,
        headerShown: false,
        tabBarStyle: style.tabBarStyle,
        tabBarLabelStyle: style.tabBarLabelStyle,
        tabBarHideOnKeyboard: true,
      }}
    >
      {Object.keys(Screens).map((screen) => (
        <Tab.Screen
          key={screen}
          name={screen}
          component={Screens[screen]}
          options={{
            tabBarLabel: t(
              `${
                screen === Variable.SCREENS.HOME
                  ? "CREDIT_BOOK"
                  : screen === Variable.SCREENS.CASH_BOOK
                  ? "CASH_BOOK"
                  : `${screen}Screen`
              }`
            ),
            tabBarIcon:
              screen == Variable.SCREENS.HOME
                ? ({ focused, color }) => (
                    <CreditSvg
                      fill={color}
                      width={Metrix.VerticalSize(25)}
                      height={Metrix.VerticalSize(25)}
                    />
                  )
                : screen == Variable.SCREENS.CASH_BOOK
                ? ({ focused, color }) => (
                    <CahsSvg
                      fill={color}
                      width={Metrix.VerticalSize(25)}
                      height={Metrix.VerticalSize(25)}
                    />
                  )
                : ({ focused, color }) => (
                    <ProfileSvg
                      fill={color}
                      width={Metrix.VerticalSize(40)}
                      height={Metrix.VerticalSize(40)}
                    />
                  ),
          }}
        />
      ))}
    </Tab.Navigator>
  );
};
```

**How to use props.state.params in react navigation v6?**

TypeError : props.navigation.getParam is not a function. In(props.navigation.getParam('name')

```jsx showLineNumbers
console.log(" props.route.params", props.route.params);
```

https://stackoverflow.com/questions/60769220/typeerror-props-navigation-getparam-is-not-a-function-inprops-navigation-get

### Sentry react native

**Which parameter need to pass in sentry and firebase for analytics ?**

**React Native | Sentry Documentation**

https://docs.sentry.io › platforms › react-native
Sentry's React Native SDK enables automatic reporting of errors and exceptions, and identifies performance issues in your application. The React Native SDK ...

**react native network inspector :**

If you are looking to debug network requests on a release version of your app you can use the library react-native-network-logger. It lets you monitor and view network requests within the app from a custom debug screen.
https://stackoverflow.com/questions/33997443/how-can-i-view-network-requests-for-debugging-in-react-native

**Network logger in react native :**

@channel We are using this network logger in retailo, if u have any recommendation tou now is the time:
https://www.npmjs.com/package/react-native-network-logger

We have integrated react-native-dotenv in hisaab app
But .env var are not accessing from file but after run this command this works

```jsx showLineNumbers
       "start-reset-cache": "react-native start --reset-cache",

```

**Reset cache command in react native**

try this first:

This command was not working

`npm start --reset-cache`
Add below command in package.json and npm
`$ npm run start-reset-cache from terminal`
On terminal you should receive this warning
warning: the transform cache was reset.
Wait for making bundle it will take and time and then boom it works

```jsx showLineNumbers
  "start-reset-cache": "react-native start --reset-cache",
```

```jsx showLineNumbers
H.A.  11:14 PM
Standup in 15 min

H.A.  11:45 PM
@Bilal Hadid please answer @Salman Khan pm about QR code front end please.

Bilal Hadid  11:45 PM
ok
11:45
standup end?

Salman Khan  11:46 PM
No come on


3 replies
Last reply today at 11:50 PMView thread
New

Bilal Hadid  11:54 PM
react native qr code
11:55
it is library name
11:55
you just install it then import it
11:56
import QRCode2 from "react-native-qrcode-svg";

```

**Data validation library \ form validation react and react native**
Yup and joi

https://www.npmjs.com/package/yup
https://www.npmjs.com/package/joi

**Formik Form in react native**
https://www.npmjs.com/package/formik

### AXIOS

**Get notified after axios timeout**

Intercept timeout errors? #1174
timeout in axios interceptors

https://stackoverflow.com/questions/50619928/get-notified-after-axios-timeout
https://github.com/axios/axios/issues/1174
https://www.codegrepper.com/code-examples/javascript/axios+timeout

---

## sidebar_position: 1

# Intro

## mixed Copy of Mixed research private

**In which computer memory stack store temp variable**

A stack is a special area of a computer's memory which stores temporary variables created by a function. In stack, variables are declared, stored and initialized during runtime. It is a temporary storage memory.07-Oct-2021

Where are stack variables stored?
Where is stack stored in memory?

RAM
Stack is used for static memory allocation and Heap for dynamic memory allocation, both stored in the computer's RAM . Variables allocated on the stack are stored directly to the memory and access to this memory is very fast, and it's allocation is dealt with when the program is compiled.
http://net-informations.com/faq/net/stack-heap.htm

**Queue data structure memory**

Queue is an abstract data structure, somewhat similar to Stacks. Unlike stacks, a queue is open at both its ends. One end is always used to insert data (enqueue) and the other is used to remove data (dequeue). Queue follows First-In-First-Out methodology, i.e., the data item stored first will be accessed first.
OR
Queue is linear data structure based on “First In First Out” (FIFO) principle. The elements that are inserted earlier will be deleted before those elements which are added later. It is used to maintain sequence of events occurring.04-Sept-2020

Queues- Introduction and Memory Representation:
https://csveda.com/queue-applications-introduction-and-memory-representation/

the stack has size limits
https://gribblelab.org/teaching/CBootCamp/7_Memory_Stack_vs_Heap.html

**the stack has size limits?**

It depends on your operating system. On Windows, the typical maximum size for a stack is 1MB, whereas it is 8MB on a typical modern Linux, although those values are adjustable in various ways.

https://softwareengineering.stackexchange.com/questions/310658/how-much-stack-usage-is-too-much#:~:text=It%20depends%20on%20your%20operating,are%20adjustable%20in%20various%20ways.

**what is the limit of queue in redux saga**

We can increase queue limit to as much as we want even we can dynamically increase queue limit
But as queue stored in RAM (temporary memory) it will wanish when user clear app cache or (may be when user kill app from background as well)

How to install git in ubuntu linux
sudo apt update
sudo apt install git
https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-20-04

**Conflicting peer dependency: react@18.0.0 #3517**

Conflicts in React dependency tree
Solution:

```bash showLineNumbers
npm i --legacy-peer-deps
```

**Updating the snapshot file**

```bash showLineNumbers
$ Yarn test file-path -u
```

https://javascript.plainenglish.io/jest-updating-snapshot-tests-ef6c731cb68b

**Progress bar in react native**

https://www.npmjs.com/package/react-native-progress

**Custom fonts in react native**

https://mehrankhandev.medium.com/ultimate-guide-to-use-custom-fonts-in-react-native-77fcdf859cf4

**Offline support in react native**

If you dont know how to build anything in react native
Just try to search how to make this in Android (JAVA or kotlin) and replicate that thing in react native like what is the alternative or JAVA this thing in react native etc.

Chaman Lal 4:14 PM

@Zubair Mehboob, can you please share the list of packages that we are using for offline approach

Zubair Mehboob 4:14 PM

Sure

```bash showLineNumbers
typeorm
react-native-sqlite-storage
@redux-offline/redux-offline
```

https://www.npmjs.com/package/@redux-offline/redux-offline

Koi package of only queue system isliye use nhe kia q k us ke downloads both km thy or support bhe km thi or usme edge cases bhe ziada ate. By zubair mehboob NGI

**UML diagram :**

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image130.png)

https://www.linkedin.com/pulse/offline-first-approach-understanding-various-architecture-/?trk=organization-update-content_share-article

**react native offline**

https://medium.com/@InspireNL/redux-offline-queue-open-source-413b20a29e2b

**buffer limit**

Implemented new type of buffer - infinity, which will expand itself a… #530

https://github.com/redux-saga/redux-saga/pull/530

**Offline first react native**

https://www.netguru.com/blog/how-to-design-offline-first-approach-in-mobile-app

WatermelonDB provide both sqlite DB support and synchronization feature support since why we are not going with watermelonDB is it has very low/short community (if we face any problem in watermelonDB feature then we would have to wait so long so that any developer will fix that issue and merge PR as well)

@channel please read this so that we can have idea how companies are implementing offline-first.
https://www.linkedin.com/pulse/offline-first-approach-understanding-various-architecture-?trk=organization-update-content_share-article

**Programmatically Restart a React Native App:**

React-native-restart package

https://www.npmjs.com/package/react-native-restart
https://stackoverflow.com/questions/37489946/programmatically-restart-a-react-native-app

### R&D

We can add if check of env variables if provided or not based on that we can show proper error in console in sheel scripts

```bash showLineNumbers
if [ -z "$ADJUST_APP_TOKEN" ]
then
    echo "You need to define the ADJUST_APP_TOKEN variable in AppCenter Console"
    exit
fi
```

**Secure enviornment apps in react native like HBL app**

https://javascript.plainenglish.io/building-a-secure-mobile-app-with-react-native-9602e3c37302

**how to close html dom from iframe in html**

Close child window in a IFrame RRS feed
How do I close an iframe window?
how to acces window.close in iframe

https://social.msdn.microsoft.com/Forums/en-US/e8ae6b61-64b4-4d13-a8cb-051f9b65a81f/close-child-window-in-a-iframe?forum=asphtmlcssjavascript

**Adjust in react native for marketing stats (need more research on this zohaib had integrated this on hisaab project by retailo)**

https://help.adjust.com/en/developer/android-sdk-documentation
https://github.com/adjust/android_sdk

**Offline-first in React Native: How to build great offline apps - Josh Warwick**

https://www.youtube.com/watch?v=b7TtH57Nlic

**Single sign on R&D and implementation :**

https://docs.google.com/document/d/1n57qq0tdcFJ_DGT9YpeLdSMjq_quwmn2xKD6gkqm0AA/edit

### JWT

Online tool to decode encoded JWT and get information from it for testing.
https://jwt.io/

**Draw Diagram : (Uml and flowchart diagram):**

https://app.diagrams.net/#G1EU5CxNb6aXCKqKKIFi8_EWsrGEvnILgs

Enforce or disallow spaces inside of curly braces in JSX attributes and expressions. (react/jsx-curly-spacing)

How to fix eslint formatting issues

```bash showLineNumbers

"lint-fix": "eslint --fix src --ext .ts,.tsx",
https://github.com/eslint/eslint/issues/7456

```

https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-curly-spacing.md

no-unused-vars in vscode how ot remove all

https://eslint.org/docs/rules/no-unused-vars
https://github.com/microsoft/vscode/issues/105234

React-native-snackbar for toast in react native (less recommended) Zaman has used in dApps in hope accelerated projects.
https://www.npmjs.com/package/react-native-snackbar

**Open downloaded pdf file in react native from mobile storage download directory in hisaab app of retailo**

**how to open pdf from file path in react native**

react-native-file-viewer
https://www.npmjs.com/package/react-native-file-viewer

Issues fixes

https://github.com/vinzscam/react-native-file-viewer/issues/94
https://github.com/vinzscam/react-native-file-viewer/issues/103
https://stackoverflow.com/questions/59876571/react-native-how-to-open-local-file-url-using-linking

Weekly Downloads
27,398

```jsx showLineNumbers
npm install react-native-file-viewer --save
```

react-native-view-pdf
https://www.npmjs.com/package/react-native-view-pdf
Weekly Downloads
11,991

rn-fetch-blob .fetch not working in android 9
android:requestLegacyExternalStorage="true"
https://github.com/joltup/rn-fetch-blob/issues/478

File viewer in react native | file opener in react native
react native file system open pdf file
3

I could not make it work with Linking for local pdf files. Then i searched more and found react-native-file-viewer. With this, you can open a pdf as simply as:

```jsx showLineNumbers
 import FileViewer from "react-native-file-viewer";
 ...

 try {
     await FileViewer.open(url, { showOpenWithDialog: true, showAppsSuggestions: true });
 } catch (e) {
     console.warn(TAG, "An error occurred", JSON.stringify(e));
 }

```

To open multple files one by one

```jsx showLineNumbers
// Danish Khalid  4:30 PM
const showFiles =
  file &&
  file.map(async (item: string) => await downloadFileOnAndroidAndiOS(item));

let i = 0;
const funSync = async () => {
  FileViewer.open(await showFiles[i], {
    onDismiss: () => {
      if (i !== showFiles.length - 1) {
        console.log("dismiss");
        i++;
        funSync();
      }
    },
  });
};
funSync();
```

**how to programmatically open pdf from local directory in react native**

https://stackoverflow.com/questions/53776607/how-to-open-pdf-files-in-3rd-party-app-via-react-native
https://www.npmjs.com/package/react-native-view-pdf

RNFetchBlob.fetch not working using rn-fetch-blob

https://github.com/joltup/rn-fetch-blob
https://stackoverflow.com/questions/44546199/how-to-download-a-file-with-react-native

react-native-pdf

https://www.npmjs.com/package/react-native-pdf

Document picker file picker in react native

https://www.npmjs.com/package/react-native-document-picker

Salam, 130pm meeting today is on the idea discussed on Friday (mini app / app bundling) so please do brushing up of your R&D work on this

**Possible solutions:**

https://github.com/smallnew/react-native-multibundler

React Native mini-app / microapp structure

https://stackoverflow.com/questions/66252829/react-native-mini-app-microapp-structure

Test text

**How to make release build for App store
.ipa file generation command or we have to make using xcode where is .ipa file located after generated from xcode ?**

**package to remove all unused imports and variable in react or
How can I remove unused imports/declarations from the entire project of React Typescript?**

https://stackoverflow.com/questions/64365300/how-can-i-remove-unused-imports-declarations-from-the-entire-project-of-react-ty

**Toggle-switch-react-native npm package**

Toggle in react native like IOS in react native android phone tested working like IOS toggle (Y)

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image141.png)

https://www.npmjs.com/package/toggle-switch-react-native

**Login with instagram in react native**

React-native-instagram-login (hamza has used this package in Artist NFT app for hope accelarated)
https://www.npmjs.com/package/react-native-instagram-login
https://www.youtube.com/watch?v=Xw-mCiyUMgE&ab_channel=HungVu

### Deep linking #deeplinking

**how to do deep linking using react navigation**

https://reactnavigation.org/docs/deep-linking/ (isme android ios both k liye hy recommended)
https://blog.jscrambler.com/how-to-handle-deep-linking-in-a-react-native-app
https://stackoverflow.com/questions/55086526/how-to-open-app-with-an-url-specific-react-native
https://www.youtube.com/watch?v=_fVNt1KjkEk&ab_channel=UnsureProgrammer tutorial
https://blog.logrocket.com/understanding-deep-linking-in-react-native/
https://github.com/dabit3/react-native-deep-linking
https://medium.com/react-native-training/deep-linking-your-react-native-app-d87c39a1ad5e
https://www.youtube.com/watch?v=rvDq2WMU4mw&t=13s
https://github.com/saadibrahim/react-native-deep-links

how to check if another specific app is installed in react native android
Use firebase dynamic url

https://rnfirebase.io/dynamic-links/usage
https://medium.com/@c.nwaugha/how-to-implement-firebase-dynamic-links-in-react-native-888a554bd7fa
https://www.youtube.com/watch?v=YT841IVQvSc
https://www.youtube.com/watch?v=rvDq2WMU4mw&t=13s (deep linking be another way around)

how to integrate firebase dynamic url in react native

https://www.youtube.com/watch?v=zra2DCd0DnY

```jsx showLineNumbers
 Linking.openURL('twitter://timeline')
   onPress={() => {
         const playStoreUrl =
           'https://play.google.com/store/apps/details?id=com.app.retailerapp&hl=en&gl=US';
         const SchemaUrl = 'https://retailo.co/hisaab-app';
         // console.log('SchemaUrl', SchemaUrl);
         Linking.openURL(SchemaUrl)
           .then(opened => {
             if (!opened) {
               Linking.openURL(playStoreUrl);
             }
           })
           .catch(err => {
             Linking.openURL(playStoreUrl);
           });
       }}>


```

**how to check if user has installed specific app in react native**

OR
How can i check app installed in react native code

You can use firebase dynamic linking to achieve this

https://stackoverflow.com/questions/44005242/how-can-i-check-app-installed-in-react-native-code
https://www.npmjs.com/package/react-native-check-app-install

**how to convert es5 to es6 javascript**

https://parthpadhiar.medium.com/convert-es5-to-es6-node-js-a061d7b2403a

https://stackoverflow.com/questions/44005242/how-can-i-check-app-installed-in-react-native-code
https://stackoverflow.com/questions/41655898/react-native-rtl-on-android

**Firebase also provide dynamic deep linking #deeplinking for react native (hammad ali khan android developer at ngi recommended this he has implemented this)**

Inka Use Case ye tha unka :
K agr koi deeplnk pe click krta hy or agr mobile me app install nhe hy to wo mobile app to open nhe kr satka wo/firebase google play store pe redirect kr k open kr dyta hy app in goolge play store.

Watch video in below link for details.
https://firebase.google.com/products/dynamic-links?gclid=Cj0KCQiA_8OPBhDtARIsAKQu0gbHiXYIrSpLFvUY4I-X0DpJK77QD08ThSjxiFu-L7LGp7mALUTG5KUaAidJEALw_wcB&gclsrc=aw.ds

**Localization, internationalization, locale, multilingual, RTL left to right right to le**

urdu transation k liye wo link diyega jo usama ne diya tha

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image143.png)

https://www.ijunoon.com/transliteration/?type=162202216738

#how to pass dynamic values in i18n
#react-i18next and replacing placeholder keys with components
#react-i18next dynamic key
#“react i18n dynamic text” Code Answer
#Internationalize dynamic messages

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image144.png)

https://stackoverflow.com/questions/55000798/react-i18next-and-replacing-placeholder-keys-with-components

**Add internationalization and RTL layout support to your React Native app using react-i18next**

https://github.com/saadibrahim/react-native-rtl-tutorial
https://www.youtube.com/watch?v=-x9sHrkzRyw&ab_channel=SaadIbrahim (Recommended video one video for all work)

**Localization in tab navigation in **

Just pass translated name in `tabBarLabel` in `options` object
https://reactnavigation.org/docs/material-top-tab-navigator/

```jsx showLineNumbers
<Tab.Screen
  name={Variable.LATE}
  component={RenderReminders}
  options={{ tabBarLabel: t(`${Variable.LATE}`) }}
/>
```

### NPM vs YARN

Use yarn rather then npm because npm have lots of issues that yarn has fixed

Below issues has fixed by yarn
Error when trying to install react-redux dependency
OR

```jsx showLineNumbers
npm install fails with react 17.0.1 and react-native 0.64.0 #2603
```

**Error: spawn ./gradlew EACCES react native**

Sol:

```jsx showLineNumbers
run
$ chmod 755 android/gradlew

20
Run the following command
chmod 755 android/gradlew
inside your app root folder then run
react-native run-android

```

https://stackoverflow.com/questions/54413443/react-native-error-while-creating-app-could-not-create-service-of-type-scriptp
https://stackoverflow.com/questions/43667745/react-native-run-android-command-failed-but-gradlew-installdebug-work

**what is called that notification which is showing when song is playing in android**

This called foreground service or background notification service something like that
You cannot clear foreground service notification untill service is running or component is not unmounted

In React Native

how to create foreground notification service in react native
https://notifee.app/react-native/docs/android/foreground-service

**Issues :**

**When app is in background or in killed state the push notification popup is arrived and when app is in foreground**

For simplicity or quick fix We can show popup when app is on foreground or
We have to make/design custom in App push notification popup.
Or
We have to make custom push notification that will only show when push notification arrived when app is in foreground but in kill and background state the default push notification will show.

**In Native Android: **

**How to Start a Foreground Service in Android (With Notification Channels)**

https://www.youtube.com/watch?v=FbpD5RZtbCc&ab_channel=CodinginFlow

**How To Make Music Player Notification In Android Studio | Show Notification In Sliding Panel Part 4**

https://www.youtube.com/watch?v=8B0sOpPtnIU&ab_channel=Programmity

**What is the difference between cloud messaging and in-app messaging?**

Firebase Cloud Messaging (FCM) is a cross-platform messaging solution that lets you reliably send messages at no cost. Firebase In-App Messaging: Engage active app users with contextual messages. They both send messages to the app.15-Oct-2020

https://stackoverflow.com/questions/64369489/what-is-the-difference-between-firebase-cloud-messaging-and-firebase-in-app-mess

Deep linking can be named as pending intent in android native
pending intent in android notification

https://developer.android.com/training/notify-user/navigation

**rn fetch blob for download file in react native (for access mobile storage)**

https://www.npmjs.com/package/rn-fetch-blob

**how to use navigation without passing in props**
OR
how to navigate from any component in react navigation

Solution:
5
You can't access navigation because it's not ready yet. you can create Ref for your navigation then export it and use it where you want.

```jsx showLineNumbers
// App.js

import { NavigationContainer } from "@react-navigation/native";
import { navigationRef } from "./RootNavigation";

export default function App() {
  return (
    <NavigationContainer ref={navigationRef}>{/* ... */}</NavigationContainer>
  );
}
```

https://stackoverflow.com/questions/65562835/couldnt-find-a-navigation-object-is-your-component-inside-a-screen-in-a-naviga (recommended)
https://stackoverflow.com/questions/61170112/how-to-use-navigation-navigate-from-a-component-outside-the-stack-navigation

### R&D topics of React native to do later in training period

**Exchange data between React Native Apps**

https://stackoverflow.com/questions/52398411/exchange-data-between-react-native-apps

**Postman public api collection**

testing postman rest for download file

https://www.postman.com/search?q=file%20download&scope=all&type=all

https://stackoverflow.com/questions/52398411/exchange-data-between-react-native-apps

**Implement deep linking in React Native apps using Universal links and URL schema**

https://www.youtube.com/watch?v=rvDq2WMU4mw&ab_channel=SaadIbrahim
https://stackoverflow.com/questions/52795246/linking-in-react-native-can-open-just-one-app
https://medium.com/wolox/ios-deep-linking-url-scheme-vs-universal-links-50abd3802f97

**Patch package** : (zubair have used in hisaab app for fixing changes in range picker calender that was not giving any functionality to close or select only one date)

This will create a patches folder in root dir that contains patch files

E.g
React-native-daterange-picker+1.5.1.patch

```jsx showLineNumbers
diff --git a/node_modules/react-native-daterange-picker/src/index.js b/node_modules/react-native-daterange-picker/src/index.js
index 38517d4..a879734 100644
--- a/node_modules/react-native-daterange-picker/src/index.js
+++ b/node_modules/react-native-daterange-picker/src/index.js
@@ -47,8 +47,10 @@ const DateRangePicker = ({
  buttonTextStyle,
  presetButtons,
  open,
+  isOpen,
+  onOpen
}) => {
-  const [isOpen, setIsOpen] = useState(false);
+  //const [isOpen, setIsOpen] = useState(false);
  const [weeks, setWeeks] = useState([]);
  const [selecting, setSelecting] = useState(false);
  const [dayHeaders, setDayHeaders] = useState([]);
@@ -85,19 +87,20 @@ const DateRangePicker = ({
  };
  const _onOpen = () => {
-    if (typeof open !== "boolean") onOpen();
+    if (typeof open !== "boolean") onOpen(true);
  };
  const _onClose = () => {
    if (typeof open !== "boolean") onClose();
  };
-  const onOpen = () => {
-    setIsOpen(true);
-  };
+  // const onOpen = () => {
+  //   setIsOpen(true);
+  // };
  const onClose = () => {
-    setIsOpen(false);
+   // setIsOpen(false);
+   onOpen(false)
    setSelecting(false);
    if (!endDate) {
      onChange({
@@ -210,7 +213,7 @@ const DateRangePicker = ({
  useEffect(() => {
    if (typeof open === "boolean") {
-      if (open && !isOpen) onOpen();
+      if (open && !isOpen) onOpen(true);
      else if (!open && isOpen) onClose();
    }
  }, [open]);


```

**Patch npm package for making patch file when you fix issue in your dependencies**

When you make changes in node_modules this will trace the changes and make a patch script that will run through package post script (that will run when you run npm i after deleting node modules)

https://www.npmjs.com/package/patch-package

**Emulator blocking in react native for save from hackers and attacks
In production mode**

Automation testing while debugging in react native
selenium alternative for react native for automated testing

Problem
Hm script or command likain or ap automatically screens pe navigate kre click kr k

React Native testing using Appium
is an open-source test-automation framework for native, hybrid and mobile web apps. It uses Selenium WebDriver internally. Because of this, Appium can work extremely well for the mobile web as well, and the use cases are similar if Selenium is used for web-based testing.

https://blog.codemagic.io/react-native-apps-testing-end-to-end/#:~:text=React%20Native%20testing%20using%20Appium,used%20for%20web%2Dbased%20testing.

### TESTING IN REACT NATIVE

**​​React native testing**

https://reactnative.dev/docs/testing-overview#static-analysis

**validate phone number country wise in javascript**

https://www.codegrepper.com/code-examples/javascript/phone+number+validatio
n+with+country+code+in+javascript

**react-native-phone-number-input (bilal hadid have integrated in block ride for hope accelarated)**

https://www.npmjs.com/package/react-native-phone-number-input

NPM

how to install old version of npm package in react native
`Use npm install [package-name]@[version-number]` to install an older version of a package. Prefix a version number with a caret (^) or a tilde (~) to specify to install the latest minor or patch version, respectively.17-Feb-2021
Using NPM To Install A Specific Version Of A Node.js Packagehttps://www.whitesourcesoftware.com › blog › npm-instal…

```jsx showLineNumbers
E.g
npm i react-native-contacts@6.0.5
Version no your can get from repo release section
```

**How to copy file using terminal in ubuntu**
OR command to copy file using terminal in ubuntu

```bash showLineNumbers
mkdir ~/bashrcbackup
cp -b ~/.bashrc ~/bashrcbackup/

```

https://askubuntu.com/questions/195983/how-to-copy-files-via-terminal

**How to set ANDROID_HOME path in ubuntu?**

BUILD FAILED in 13s

error Failed to install the app. Make sure you have the Android development environment set up: https://reactnative.dev/docs/environment-setup.
**Error: Command failed: ./gradlew app:installDebug -PreactNativeDevServerPort=8081**

FAILURE: Build failed with an exception.

- What went wrong:
  **Could not determine the dependencies of task ':app:compileDebugJavaWithJavac'.**
  > SDK location not found. Define location with an ANDROID_SDK_ROOT environment variable or by setting the sdk.dir path in your project's local properties file at '/home/muhammadmoiz/Documents/office/hisaab-app/android/local.properties'.

OR
**how to set android home path in ubuntu for react native in ubuntu**
OR
sdk location not found react native
OR
Could not determine the dependencies of task ':app:compileDebugJavaWithJavac' react native

Solution

The problem is that our OS in this case linux/ubuntu cannot got ANDROID_HOME path from .bash_profile

I have paste this code in .bash_profile at home directory

**3. Configure the ANDROID_HOME environment variable**

The React Native tools require some environment variables to be set up in order to build apps with native code.
Add the following lines to your $HOME/.bash_profile or $HOME/.bashrc (if you are using zsh then ~/.zprofile or ~/.zshrc) config file:

```jsx showLineNumbers
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

As defined in official docs but to solve this problem we have to paste these path line of code at bottom in .bashrc file at home directory

Note : please make copy of .bashrc file to another directory so that if you want to revert to previous file you can do so

34
first open the .bashrc file by gedit ~/.bashrc

```jsx showLineNumbers
# Added ANDROID_HOME variable.
  export ANDROID_HOME=$HOME/Android/Sdk
  export PATH=$PATH:$ANDROID_HOME/tools
  export PATH=$PATH:$ANDROID_HOME/platform-tools
save the file and reopen the terminal
```

**How to log ANDROID_HOME directory in terminal
Or how to verify if ANDROID_HOME is set or not in linux**

```bash showLineNumbers
echo $ANDROID_HOME
it will show the path like /home/pathTo/Android/Sdk

```

**React Native android build failed. SDK location not found**

Although this works but we have to repeat this process for all the projects when ever we try to run any project.
One solution is to delete local.properties file if exist in your project.

https://stackoverflow.com/questions/32634352/react-native-android-build-failed-sdk-location-not-found

The SDK directory '/Users/office/Library/Android/sdk' does not exist react native
configuring project ':app' failed to find Build Tools revision
The SDK directory '/Users/username/Library/Android/sdk' does not exist
AndroidStudio SDK directory does not exist
44

Right click your project and select 'Open Module Settings' under SDK Location put your location for your SDK.

paste in /Users/AhmadMusa/Library/Android/sdk

Clean and rebuild your project

Update

Try to delete your local.properties file and create a new one, but do not check it into version control.

Right click top level of project and Create new file 'local.properties' then add: sdk.dir=/Users/AhmadMusa/Library/Android/sdk

Clean and build

https://stackoverflow.com/questions/32149220/androidstudio-sdk-directory-does-not-exist/32149274#32149274
https://stackoverflow.com/questions/34917661/configuring-project-app-failed-to-find-build-tools-revision

It worked after change in local.properties file from:
sdk.dir=/Users/username/Library/Android/sdk
to:
sdk.dir=/Users/runner/Library/Android/sdk

Error fixed in setup of React navigation 6 in react native 0.66.3

**error Failed to install the app. Make sure you have the Android development environment set up: https://reactnative.dev/docs/environment-setup.
Error: Command failed: ./gradlew app:installDebug -PreactNativeDevServerPort=8081
/home/muhammadmoiz/Documents/office/assets/rn_boilerplate/android/app/src/main/java/com/rn_boilerplate/MainActivity.java:2: error: class, interface, or enum expected
package com.rn_boilerplate;**

```jsx showLineNumbers

Add the following code to the body of MainActivity class:
@Override
protected void onCreate(Bundle savedInstanceState) {
 super.onCreate(null);
}
Copy
and make sure to add an import statement at the top of this file:
import android.os.Bundle;
```

Output file look like this
The position of line are important make sure to add

```jsx showLineNumbers

import android.os.Bundle;
This line after
import com.facebook.react.ReactActivity;

And add this code
 @Override
 protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(null);
 }

after

  */
 @Override
 protected String getMainComponentName() {
   return "rn_boilerplate";
 }

Result:
package com.rn_boilerplate;

import com.facebook.react.ReactActivity;
import android.os.Bundle;

public class MainActivity extends ReactActivity {

 /**
  * Returns the name of the main component registered from JavaScript. This is used to schedule
  * rendering of the component.
  */
 @Override
 protected String getMainComponentName() {
   return "rn_boilerplate";
 }

 @Override
 protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(null);
 }
}

```

**Routes naming convention in react-native :**

The casing of the route name doesn't matter -- you can use lowercase home or capitalized Home, it's up to you. We prefer capitalizing our route names.

Home (recommended)
https://reactnavigation.org/docs/native-stack-navigator/

Note: The component prop accepts component, not a render function. Don't pass an inline function (e.g. component={() => <HomeScreen />}), or your component will unmount and remount losing all state when the parent component re-renders. See Passing additional props for alternatives.
https://reactnavigation.org/docs/hello-react-navigation

Passing additional props​
Sometimes we might want to pass additional props to a screen. We can do that with 2 approaches:

Use React context and wrap the navigator with a context provider to pass data to the screens (recommended).
Use a render callback for the screen instead of specifying a component prop:
https://reactnavigation.org/docs/hello-react-navigation#passing-additional-props

Context in react native same as it is in reactjs
https://wix.github.io/react-native-navigation/docs/third-party-react-context/

Note: By default, React Navigation applies optimizations to screen components to prevent unnecessary renders. Using a render callback removes those optimizations. So if you use a render callback, you'll need to ensure that you use `React.memo` or `React.PureComponent`for your screen components to avoid performance issues.

Another common requirement is to be able to go back multiple screens -- for example, if you are several screens deep in a stack and want to dismiss all of them to go back to the first screen. In this case, we know that we want to go back to Home so we can use navigate('Home') (not push! try that out and see the difference). Another alternative would be navigation.popToTop(), which goes back to the first screen in the stack.

**How to force checkout to branch in git**

`git checkout -f master`

https://stackoverflow.com/questions/17223527/how-do-i-force-git-to-checkout-the-master-branch-and-remove-carriage-returns-aft

`200 status code` (GET request)
Successful fetch records from server.

`201 status code` (for post request when record created on database)
The HTTP 201 Created success status response code indicates that the request has succeeded and has led to the creation of a resource.13-Aug-2021

`204 status code`
For a PUT request: HTTP 200 or HTTP 204 should imply "resource updated successfully". For a DELETE request: HTTP 200 or HTTP 204 should imply "resource deleted successfully". HTTP 202 can also be returned which would imply that the instruction was accepted by the server and the "resource was marked for deletion".26-Feb-2010
https://stackoverflow.com/questions/2342579/http-status-code-for-update-and-delete#:~:text=For%20a%20PUT%20request%3A%20HTTP,resource%20was%20marked%20for%20deletion%22.

`400 status code` bad request error(request to wrong api route or invalid path)
A 400 Bad Request error means that the request the client made is incorrect or corrupt, and the server can't understand it. The main thing to understand is that the 400 error is a client-side error. It indicates that the request the client submitted can't be processed by the server.

`401 status code` (for example when passing expired token)
The HyperText Transfer Protocol (HTTP) 401 Unauthorized response status code indicates that the client request has not been completed because it lacks valid authentication credentials for the requested resource.25-Nov-2021

`403 forbidden` (Its for ACL :when you dont have access/authorization to access a particular resource we normal user cannot access admin panel only admin can access)
The HTTP 403 Forbidden response status code indicates that the server understands the request but refuses to authorize it.

`500 status code` (internal server error)
When the server is down.

https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

**How to install slack and skype in Huawei y6p because it is not available in AppGallery of huawei in Android**

Simply download the apk manually from browser and then enable usb debugging in phone
Connect mobile with PC through USB and then goto download directory and open terminal and run this below command

`$ adb install <apk-name>`
I had install slack and skype through this approach in huawei phone
If not work then try to install the older versions of apk it will work.

`adb install by device id`

`adb – Install APK on Specific Device`

Now when you know how to list all attached devices, we can install our APK on one of these devices using same adb command.

```jsx showLineNumbers
adb -s <DEVICE ID> install <PATH TO APK>
where <DEVICE ID> should be replaced with the value of attached device id. The device id from the output of adb devices command.

List devices with adb devices command:
List of devices attached
06157df6aaf6c740    device
emulator-5554    device
2. Use adb -s <device id> install <path to apk> to install on selected device:

adb -s 06157df6aaf6c740 install my-android-app.apk

adb -s 805KPQJ1888444 install app-release.apk
https://www.appsdeveloperblog.com/install-apk-on-device-adb/

```

We can use play store for app testing
App distributor of firebase
App center
Direct build share
Testflight (IOS only)

### Styled components : (In typescript)

[v4.0.0] Types: Could not find a declaration file for module 'styled-components/native'. #2099

Just add:
❯yarn add @types/styled-components-react-native -D
Or npm install @types/styled-components-react-native -D

Passing props using styled-components :

```jsx showLineNumbers
// Define our button, but with the use of props.theme this time
const Button = styled.button`
  color: ${(props) => props.theme.fg};
  border: 2px solid ${(props) => props.theme.fg};
  background: ${(props) => props.theme.bg};

  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border-radius: 3px;
`;
```

**Microsoft app center for publishing react native build
CI/CD to make build and send invite to testers when code push on branch (like develop) like heroku make build**

2 things app center get

pre script file (which will get .env var)
pre-build file

It have force minor update feature for tester devices

**vsc-rename-files**

orer%20view,from%20that%20file's%20context%20menu.
https://marketplace.visualstudio.com/items?itemName=alfnielsen.vsc-rename-files

**How to disable yellow warnings to appear on app but log in console**

how to hide warning in react native android

```jsx showLineNumbers
// disable yellow warning
import { LogBox } from "react-native";
LogBox.ignoreAllLogs(true);
```

For me below lines worked currently I am using react native 0.64

```jsx showLineNumbers
import { LogBox } from "react-native";

LogBox.ignoreLogs(["Warning: ..."]); //Hide warnings

LogBox.ignoreAllLogs(); //Hide all warning notifications on front-end
```

https://stackoverflow.com/questions/35309385/how-do-you-hide-the-warnings-in-react-native-ios-simulator

### Lodash like useful methods

How to print a number with commas as thousands separators in JavaScript
OR
how to number amount into comma separated string in javascript

Solution :

```jsx showLineNumbers
export function numberWithCommas(x) {
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}

Input: 1000;
Output: 1, 000;
```

https://stackoverflow.com/questions/2901102/how-to-print-a-number-with-commas-as-thousands-separators-in-javascript

scrollview inside bottom sheet react native

```jsx showLineNumbers

Import scrollview from react-native-gesture-handler:

E.g

<ScrollView>
  <ContainerBS>
  <ContainerBS>
<ScrollView>
```

https://github.com/osdnk/react-native-reanimated-bottom-sheet/issues/228

#224 (comment)
Just import ScrollView/FlatList from `react-native-gesture-handler`
That works on android without any other workarounds

https://stackoverflow.com/questions/62951696/react-native-reanimated-bottom-sheet-content-in-snapable-container-only-scrol

E.g of usage of scrollview in react native

```jsx showLineNumbers
 const backgroundStyle = {
   backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
 };

<ScrollView
       contentInsetAdjustmentBehavior="automatic"
       style={backgroundStyle}
     >
```

**Dynamically adding key in object **

We can not add key by using ternery operator in object

```jsx showLineNumbers
{
				...(type && { transactionType: type }),
				...(text && { search: text }),
}
```

**Google password manually adding**

First export .csv file from this link

https://passwords.google.com/options?ep=1

And open .csv file in excel and manually add new username password with url and name
And save in unformatted text csv format

And then again import same csv file from same url by import option.
https://passwords.google.com/options?ep=1

And that’s it you are now relax and enjoy the comfort.
https://support.google.com/accounts/answer/10500247?p=import-pws&hl=en&visit_id=637779925466265780-3687999032&rd=1

### STYLE GUIDE:

**how to render style based on condition in react native stylesheet?
React Native styling with conditional**

```jsx showLineNumbers
<CountryPicker
  containerButtonStyle={
    I18nManager.isRTL
      ? styles.containerButtonStyleRTL
      : styles.containerButtonStyle
  }
/>;

//style.js

const styles = StyleSheet.create({
  containerButtonStyle: {
    paddingRight: 5,
  },
  containerButtonStyleRTL: {
    paddingLeft: 5,
  },
});
```

https://stackoverflow.com/questions/45478621/react-native-styling-with-conditional

How to slide <View/> in and out from the bottom in React Native? how to show a view with bottom to top transition in react native android
https://stackoverflow.com/questions/39117599/how-to-slide-view-in-and-out-from-the-bottom-in-react-native

**on IOS device dropdown is underlying the logos in react native**

I had given zindex 1 to dropdown list and issue fixed

**Passing functions in react native stylesheet**

You can use functions when dynamic styling like passing margin dynamic to use it in multiple places (recommended)

```jsx showLineNumbers
export default StyleSheet.create({
  MT: (val = 35) => {
    return {
      marginTop: Metrix.VerticalSize(val),
    };
  },
});

Or;
MT: (val = 35) => ({
  marginTop: Metrix.VerticalSize(val),
}),
  (
    //usage
    <AppPhoneInput
      value={phone}
      onChangeText={setPhone}
      style={styles.MT(10)}
      setMyCountryCode={setCountryCode}
      title={`Performing Right\nOrganization No.`}
    />
  );
```

Rather than this below hard coded not recommended waste time to maintain variables
​​

```jsx showLineNumbers
 MT35: {
   marginTop: Metrix.VerticalSize(35),
 },
```

**React Native: Inherit styles global styles**

1
You can create a global style, and use it without importing it, you only import it in your main screen.

```jsx showLineNumbers
// global styles Global.js import { StyleSheet } from 'react-native'; import { Constants } from 'expo'; module.GlobalStyles = StyleSheet.create({ container: { padding: 20, textAlign: 'center', backgroundColor: 'blue', paddingTop: Constants.statusBarHeight, flex: 1, }, }); if (global) { global.GlobalStyles = module.GlobalStyles; }
Then in your main screen / entry point
import './Global';
Use it like
<View style={GlobalStyles.container}>

```

```jsx showLineNumbers
// global styles Global.js
import {StyleSheet} from 'react-native';
import {Metrix} from '..';

module.GlobalStyles = StyleSheet.create({
 MTAuto: {
   marginTop: 'auto',
 },
 // handlers
 MT: (val = 35) => ({
   marginTop: Metrix.VerticalSize(val),
 }),
 PB: val => ({
   paddingbottom: Metrix.VerticalSize(val),
 }),
});

if (global) {
 global.GlobalStyles = module.GlobalStyles;
}


Usage
 <View
         style={[
           GlobalStyles.MT(20),
           GlobalStyles.PB(15),
           styles.footerTxtBtnWrapper,
         ]}>
         <AppButton
           title="NEXT"
           onPress={() => dispatch({type: 'AUTHENTICATE_APP'})}
           style={styles.appButton}
         />
       </View>
```

https://stackoverflow.com/questions/56652729/react-native-inherit-styles/56654194
Demo https://snack.expo.dev/@lekgwaraj/global-variable-in-react-native

```jsx showLineNumbers
export class AppHeading extends Component {
  render() {
    return (
      <AppText {...this.props} style={[styles.myAppHeading, this.props.style]}>
        {this.props.children}
      </AppText>
    );
  }
}
```

https://medium.com/@fullsour/style-inheritance-of-react-native-eca1c974f02b

**How to align content at the bottom of the screen without using flexbox in react native ?**

Solution :

marginTop: 'auto’

```jsx showLineNumbers
<View style={{ marginTop: "auto", width: "100%", paddingBottom: 15 }}>
  <Button
    style={{ marginTop: 50, marginLeft: "auto", marginRight: "auto" }}
    title="CREATE ACCOUNT"
    // onPress={() => NavigationService.navigate('')}
  />

  <OutlinedButton
    title="SIGN IN"
    style={{ marginTop: 15, marginLeft: "auto", marginRight: "auto" }}
    // onPress={() => NavigationService.navigate('')}
  />
</View>
```

To make center from left and right

```css showLineNumbers
Margin-left :’auto’'
Margin-right: ‘auto’
```

```jsx showLineNumbers
<Button
  style={{ marginTop: 50, marginLeft: "auto", marginRight: "auto" }}
  title="CREATE ACCOUNT"
  // onPress={() => NavigationService.navigate('')}
/>
```

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image194.png)

### React Native R&D

**Enviornment setup on linux**

installation of android studio https://www.itzgeek.com/post/
how-to-install-android-studio-on-ubuntu-20-04/

install node version manager nvm https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04

to install jdk from cmd line

sudo apt install vim

```bash showLineNumbers
$ cat $HOME/.bash_profile
$ touch $HOME/.bash_profile
$ vim $HOME/.bash_profile
$ source $HOME/.bash_profile
npx react-native init AwesomeProject
```

no need to install KVM and watchman because they create overhead and not making any blocker in our development

I have tried to install watchman but somehow my sudo permissiosn are reset and sudo was not working and that issue have no perfect solution so I had to reinstall OS in my laptop.

**OTP auto read on ios in react native**

https://stackoverflow.com/questions/39631168/automatic-otp-verification-in-ios POC required : need to test first I am not sure if its work on all iphone devices

**localization in react native**

layout left to right based on language in react native

https://reactnative.dev/blog/2016/08/19/right-to-left-support-for-react-native-apps

e.g https://github.com/facebook/react-native/blob/main/packages/rn-tester/js/examples/RTL/RTLExample.js

**does ios simulator support push notifications**
**YES**

Testing push notifications using the Xcode 11.4 iOS Simulator

As of Xcode 11.4, it is now possible to simulate push notifications by dragging and dropping an .apns file onto the iOS simulator. The Xcode 11.4 release notes have the following to say about the new feature:"

https://stackoverflow.com/questions/1080556/how-can-i-test-apple-push-notification-service-without-an-iphone

**does Android simulator/emulator support push notifications**
**YES**
( 31 ) Which target have your emulator? For Google Services like GCM, use a "Google APIs" (any version) target to receive push notifications

https://stackoverflow.com/questions/20521600/android-emulator-not-receiving-push-notifications

#### React native fabric

https://www.google.com/search?q=what+is+react+native+fabric&oq=what+is+react+native+fabric&aqs=chrome..69i57.10266j0j1&sourceid=chrome&ie=UTF-8

https://github.com/react-native-community/discussions-and-proposals/issues

#### React native fiber

Created by Lin Clark, Fiber is the reimplementation of React’s reconciliation algorithm which enables the incremental rendering of the virtual DOM.
https://medium.com/habilelabs/what-do-you-know-about-the-new-fiber-structure-of-react-js-d3f955deb4fd

multipart means form data to send media file like pictures in request

react-native: not found npm install -g react-native-cli

for making react native release build "android-release": "react-native run-android --variant=release",

react native debugger https://github.com/jhen0409/react-native-debugger/releases/tag/v0.12.1

"How can I determine if my React Native app is a
debug or release build from JavaScript code?" "**DEV**

https://stackoverflow.com/questions/34498970/how-can-i-determine-if-my-react-native-app-is-a-debug-or-release-build-from-java"

What does adb reverse do?

Android's “adb reverse” command is available in Lollipop and higher versions of Android (Platform 21+) and it allows you to access a server running on your computer from your Android device over USB without any network (WiFi or Cellular). This is done through a technique called a reverse proxy.01-Feb-2016
"dev-menu":"adb shell input keyevent 82"

https://stackoverflow.com/questions/44170991/reload-a-react-native-app-on-an-android-device-manually-via-command-line

debug react native code

https://tunvir.medium.com/react-native-debug-with-vscode-in-simple-steps-bf39b6331e67

TestFlight - How to Upload and Distribute Your App | App Store 2021 testflight

https://www.youtube.com/watch?v=DLvdZtTAJrE&ab_channel=SeanAllen

Drop app bundles here to upload

Android Package (APK) (wiki) is the package file format used by the Android operating system for distribution and installation of mobile apps.

Android App Bundle(AAB) is a new upload format that includes all your app’s compiled code and resources, but defers APK generation and signing to Google Play using Google’s app serving model called Dynamic Delivery.

**How to check certificate name and alias in keystore files?**

"You can run the following command to list the content of your keystore file (and alias name):

keytool -v -list -keystore .keystore
If you are looking for a specific alias, you can also specify it in the command:

```bash showLineNumbers
keytool -list -keystore .keystore -alias foo" OR keytool -v -list -keystore <FileName>.keystore
```

https://stackoverflow.com/questions/12893995/how-to-check-certificate-name-and-alias-in-keystore-files

### Chat system

**React native gifted chat**

This is an awesom library for UI for custom chat app I have used in post league project literey full customized Components are available https://github.com/FaridSafi/react-native-gifted-chat

**What is Hermes engine React Native?**

Hermes is an open-source JavaScript engine optimized for React Native. For many apps, enabling Hermes will result in improved start-up time, decreased memory usage, and smaller app size. At this time Hermes is an opt-in React Native feature, and this guide explains how to enable it.17-Aug-2021

**For dropdown if not available in your library like its not available in react native elements**

```js showLineNumbers
"react-native-dropdown-picker": "^3.7.6",
"to align list item text we have <DropDownPicker
  itemStyle propert" "
```

```jsx showLineNumbers
<DropDownPicker
  itemStyle={props?.itemStyle}
  items={items}
  onChangeItem={onChangeItem}
  defaultValue={selectedItem?.value}
  containerStyle={styles(props).container}
  style={styles(props).main}
  activeLabelStyle={[styles(props).inactiveLabel, styles(props).activeLabel]}
  labelStyle={styles(props).inactiveLabel}
  selectedLabelStyle={[styles(props).inactiveLabel, styles(props).activeLabel]}
  dropDownStyle={[
    styles(props).dropDown,
    {
      minHeight: AppScaler.scale(items.length * 35),
    },
  ]}
  arrowColor={props.textColor || appTheme.colors.primary}
  {...props}
/>
```

https://www.npmjs.com/package/react-native-dropdown-picker

https://stackoverflow.com/questions/42707327/

**passing-props-into-external-stylesheet-in-react-native**

```js showLineNumbers
const styles = (props) =>
AppScaledSheet.create({
main: {
borderColor: props.borderColor || '#FFFFFF',
},"
```

https://stackoverflow.com/questions/42707327/passing-props-into-external-stylesheet-in-react-native

**What's the difference between a Modal, Popup, Popover and Lightbox?**

https://ux.stackexchange.com/questions/90336/
whats-the-difference-between-a-modal-popup-popover-and-lightbox

**for responsive font size acros diff res on devices use this library**

```jsx showLineNumbers
import {AppScaler} from '../third-party/react-native-size-matters-extension'; As Andrei have used in post league react naitve project
" labelStyle: {
fontSize: AppScaler.scale(11),
fontFamily: 'Gotham-Bold',
},"


```

**📐 react-native-size-matters**

https://github.com/nirsky/react-native-size-matters

https://www.npmjs.com/package/react-native-size-matters

**App onboarding react native**

https://www.google.com/search?q=App+onboarding+examples

**Enviornment setup in react native - on mac**

first time in VD with Osama at 5 oct 2021

https://reactnative.dev/docs/environment-setup

```bash showLineNumbers

/bin/bash -c ""$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)""

brew install node

brew install watchman

Images issue fix
https://github.com/facebook/react-native/issues/29279
Patch on 0.63

Run in project dir
npm i -g patch-package

product> clean build folder

Run project from Xcode play bin

sudo gem install cocoapods

To install IOS dependencies in IOS
Goto iOS dir in project and run below command
Cd iOS && pod install

Cmd to change Xcode dir path
sudo xcode-select --switch /Applications/Xcode.app

Print: Entry, "":CFBundleIdentifier"", Does Not Exist
```

**ENVIORNMENT SETUP IN REACT NATIVE**

Andriod setup in mac

steps

reference

https://reactnative.dev/docs/environment-setup

```bash showLineNumbers

brew install --cask adoptopenjdk/openjdk/adoptopenjdk8

setting android home sdk path
nano ~/.bash_profile

to verify
cat ~/.bash_profile

run below command to refresh changes
source $HOME/.bash_profile

Run this command

sdkmanager ""platforms;android-29"" ""system-images;android-29;default;x86_64"" ""system-images;android-29;google_apis;x86""
sdkmanager ""cmdline-tools;latest"" ""build-tools;29.0.2”

[misc]

for adb devices setup
brew install android-platform-tools
https://stackoverflow.com/questions/31374085/installing-adb-on-macos

References :

Set ANDROID_HOME environment variable in mac
https://stackoverflow.com/questions/28296237/set-android-home-environment-variable-in-mac

“sdkmanager: command not found” after installing Android SDK
solution
run below command to refresh changes
source $HOME/.bash_profile"

```

**advance react native**

https://www.youtube.com/watch?v=ZwX3i3e1Vfs&ab_channel=WixEngineeringTechTalks

**React native internal**

https://www.reactnative.guide/3-react-native-internals/3.1-react-native-internals.html?source=post_page---------------------------

https://www.youtube.com/watch?v=0MlT74erp60&ab_channel=FacebookDevelopers

**integration of native module (code ) in react native**

https://reactnative.dev/docs/native-modules-android

https://reactnative.dev/docs/native-modules-ios

**cashing image from url in react native**

first its downloading image using file system and then its storing in cache storage

https://blog.logrocket.com/caching-images-react-native-tutorial-with-examples/

**can we send push notification when app offline**

No app should be online to receive PN

**Receive all the push notifications when devices are offline**

https://stackoverflow.com/questions/52522362/receive-all-the-push-notifications-when-devices-are-offline

## release and update app android ios

Welcome to App Center.

Continuously build, test, release, and monitor apps for every platform."

https://appcenter.ms/

app distributor by firebase

testflight for IOS

**React Native Error: ENOSPC: System limit for number of file watchers reached**

https://stackoverflow.com/questions/55763428/react-native-error-enospc-system-limit-for-number-of-file-watchers-reached

## React Native env setup and dev guide

https://stackoverflow.com/questions/28314139/how-to-install-android-studio-on-ubuntu

**KVM**

Reference : https://help.ubuntu.com/community/KVM/Installation

**how to uninstall node on mac**

How do I completely uninstall Node.js, and reinstall from beginning (Mac OS X)

```bash showLineNumbers

sudo rm -rf ~/.npm ~/.nvm ~/node_modules ~/.node-gyp ~/.npmrc ~/.node_repl_history
sudo rm -rf /usr/local/bin/npm /usr/local/bin/node-debug /usr/local/bin/node /usr/local/bin/node-gyp
sudo rm -rf /usr/local/share/man/man1/node* /usr/local/share/man/man1/npm*
sudo rm -rf /usr/local/include/node /usr/local/include/node_modules
sudo rm -rf /usr/local/lib/node /usr/local/lib/node_modules /usr/local/lib/dtrace/node.d
sudo rm -rf /opt/local/include/node /opt/local/bin/node /opt/local/lib/node
sudo rm -rf /usr/local/share/doc/node
sudo rm -rf /usr/local/share/systemtap/tapset/node.stp

brew uninstall node
brew doctor
brew cleanup --prune-prefix

```

https://stackoverflow.com/questions/11177954/how-do-i-completely-uninstall-node-js-and-reinstall-from-beginning-mac-os-x

https://stackoverflow.com/questions/28225045/no-such-keg-usr-local-cellar-git

**Step 1 – Remove existing Node Versions**

If your system already has a node installed, uninstall it first. My system already has installed node via Homebrew. So uninstalling it first. Skip if not already installed.

```bash showLineNumbers
brew uninstall --ignore-dependencies node
brew uninstall --force node
```

https://tecadmin.net/install-nvm-macos-with-homebrew/
https://www.freecodecamp.org/news/node-version-manager-nvm-install-guide/

**How to install npm through NVM(Node version manager)?**

how to install npm using nvm

use this zshrc

```bash showLineNumbers
$ vim ~/.zshrc
```

https://dev.to/ms314006/how-to-install-npm-through-nvm-node-version-manager-5gif

**how to change node version using nvm**

```bash showLineNumbers
nvm install <node-version that you want to use>
e.g nvm use 16

now uninstall the version that you dont want to use
e.g nvm uninstall <node-version>  (just to make sure you are using different version which you want to uninstall while running uninstall command)

node -v (you are good to go)


or extra step

nvm ls
nvm use default 16  or nvm alias default 16

```

## Bookmarks

### Nextgeni - muhammad.moiz@nextgeni.net

### NextGenI React Native

### Android Official

- [Release Notes Google APIs for Android Google Developers](https://developers.google.com/android/guides/releases)

### Animation

- [LottieFiles - Free animation files built for Lottie, Bodymovin](https://lottiefiles.com/)

- [javascript - React Native center Animated Icon](https://stackoverflow.com/questions/54948040/react-native-center-animated-icon)

- [Remove Background from Image – remove.bg](https://www.remove.bg/upload)

### Audio Recording @i

- [GitHub - prscX/react-native-voice-recorder: ReactNative: Native Audio Recorder View](https://github.com/prscX/react-native-voice-recorder)

- [android - Record audio while is touching a button like messenger, wpp or even](https://stackoverflow.com/questions/40109444/record-audio-while-is-touching-a-button-like-messenger-wpp-or-even-allo-react-n)

- [react-native-record-sound](https://github.com/MisterAlex95/react-native-record-sound)

- [GitHub - dooboolab/react-native-audio-recorder-player: react-native native module for audio recorder and player.](https://github.com/dooboolab/react-native-audio-recorder-player)

- [GitHub - 3llomi/RecordView: A Simple Audio Recorder View with "hold to Record Button" and "Swipe to Cancel " Like WhatsApp](https://github.com/3llomi/RecordView)

- [GitHub - varunjohn/Audio-Recording-Animation: WhatsApp like audio recording animations and views sample for Android.](https://github.com/varunjohn/Audio-Recording-Animation)

- [GitHub - zmxv/react-native-sound: React Native module for playing sound clips](https://github.com/zmxv/react-native-sound)

- [GitHub - jsierles/react-native-audio: Audio recorder library for React Native](https://github.com/jsierles/react-native-audio)

- [react-native-audio-recorder-player npm](https://www.npmjs.com/package/react-native-audio-recorder-player)

- [react-native-voice-recorder](https://www.npmjs.com/package/react-native-voice-recorder)

- [React Native Audio Recorder and Player - dooboolab - Medium](https://medium.com/dooboolab/react-native-audio-recorder-and-player-4aa5f26a666)

- [A React Native Sound Recorder and Player NPM Package](https://medium.com/react-native-training/a-react-native-sound-recorder-and-player-npm-package-a5f9b3fc7eed)

- [react-native-audio-toolkit/ExampleApp at master ·](https://github.com/react-native-community/react-native-audio-toolkit/tree/master/ExampleApp)

- [library for React Native](https://github.com/react-native-community/react-native-audio-toolkit)

- [GitHub - qiuxiang/react-native-recording: React Native audio recording module used for DSP with Android + iOS](https://github.com/qiuxiang/react-native-recording)

- [react-native-audio-record](https://www.npmjs.com/package/react-native-audio-record)

- [react-native-sound-recorder](https://www.npmjs.com/package/react-native-sound-recorder)

- [How To Create An Audio/Video Recording App With React Native: An In-Depth Tutorial — Smashing Magazine](https://www.smashingmagazine.com/2018/04/audio-video-recording-react-native-expo/)

- [jsierles/react-native-audio: Audio recorder library for React Native](https://github.com/jsierles/react-native-audio)

- [prscX/react-native-voice-recorder: ReactNative: Native Audio Recorder View](https://github.com/prscX/react-native-voice-recorder)

- [react-native-audio-recorder-player](https://www.npmjs.com/package/react-native-audio-recorder-player)

- [react-native-audio-record](https://www.npmjs.com/package/react-native-audio-record)

- [react-native-sound-player](https://www.npmjs.com/package/react-native-sound-player)

- [3llomi/iRecordView: A Simple Audio Recorder View with "hold to Record Button" and "Swipe to Cancel " Like WhatsApp](https://github.com/3llomi/iRecordView)

- [android - How to create a whatsapp like recording button with slide to cancel](https://stackoverflow.com/questions/28711549/how-to-create-a-whatsapp-like-recording-button-with-slide-to-cancel)

- [Stack kevinresol/react-native-sound-recorder: Simplest Sound Recorder for React Native](https://github.com/kevinresol/react-native-sound-recorder)

- [goodatlas/react-native-audio-record: Audio record buffers for React Native iOS and Android](https://github.com/goodatlas/react-native-audio-record)

- [react-native-voice-record-app/App.js at master ·](https://github.com/soutot/react-native-voice-record-app/blob/master/src/App.js)

- [jsierles/react-native-audio](https://github.com/jsierles/react-native-audio/issues/234)

- [soutot/react-native-voice-record-app](https://github.com/soutot/react-native-voice-record-app)

### calender

- [wix/react-native-calendars: React Native Calendar Components 🗓️ 📆](https://github.com/wix/react-native-calendars)

### Card Scanner

- [Kerumen/react-native-awesome-card-io: A complete and cross-platform card.io component for React Native.](https://github.com/Kerumen/react-native-awesome-card-io)

- [OCR scanner Card2Contact | Codementor](https://www.codementor.io/@uokesita/ocr-scanner-card2contact-rfdr8nljg)

- [How to Add Credit Card Scanner in React Native | A Programming Blog](https://aprogrammingblog.com/react%20native/2019/05/14/react-native-credit-card-scan.html)

- [react-native-scanner-credit-card](https://www.npmjs.com/package/react-native-scanner-credit-card)

- [Text Recognition App Using React Native - The NativeBase.io Blog](https://blog.nativebase.io/text-recognition-app-using-react-native-3537ccecda6)

### chat

- [react-native-gifted-chat](https://www.npmjs.com/package/react-native-gifted-chat)

- [React native snippet Chat ui example](https://www.bootdey.com/react-native-snippet/33/Chat-ui-example#)

- [Browsing Featured Sounds category - page 3 of 9 | Notification Sounds](https://notificationsounds.com/featured-sounds?page=3)

### Document picker

- [Elyx0/react-native-document-picker: Document Picker for React Native using Document Providers](https://github.com/Elyx0/react-native-document-picker)

- [Best file picker for react native](https://stackoverflow.com/questions/49548589/best-file-picker-for-react-native)

- [itinance/react-native-fs: Native filesystem access for react-native](https://github.com/itinance/react-native-fs)

- [vinzscam/react-native-file-viewer: Native file viewer for React Native. Preview any type of file supported by the mobile device.](https://github.com/vinzscam/react-native-file-viewer)

- [react-native-doc-viewer vs react-native-file-viewer | npm trends](https://www.npmtrends.com/react-native-doc-viewer-vs-react-native-file-viewer)

- [How to Send the document from react native DocumentPicker response to a web](https://stackoverflow.com/questions/52690047/how-to-send-the-document-from-react-native-documentpicker-response-to-a-web-api)

- [How to get Absolute path of a file in react-native?](https://stackoverflow.com/questions/52423067/how-to-get-absolute-path-of-a-file-in-react-native)

- [wkh237/react-native-fetch-blob: A project committed to making file access and data transfer easier, efficient for React Native developers.](https://github.com/wkh237/react-native-fetch-blob)

### Eslint

- [Setting up ESLint in React - Ross Whitehouse - Medium](https://medium.com/@RossWhitehouse/setting-up-eslint-in-react-c20015ef35f7)

- [Getting Started with ESLint - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/user-guide/getting-started)

- [List of available rules - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/rules/)

- [dustinspecker/awesome-eslint: A list of awesome ESLint plugins, configs, etc.](https://github.com/dustinspecker/awesome-eslint#configs)

- [Intellicode/eslint-plugin-react-native: React Native plugin for ESLint](https://github.com/Intellicode/eslint-plugin-react-native)

- [Configuring ESLint - ESLint - Pluggable JavaScript linter](https://eslint.org/docs/user-guide/configuring#specifying-parser-options)

### firebase Push notification

- [Firebase Notification Integration in React Native 0.60+](https://medium.com/@katharinep/firebase-notification-integration-in-react-native-0-60-3a8d6c8d56ff)

- [React Native: Integrating Push Notifications using FCM](https://medium.com/@anum.amin/react-native-integrating-push-notifications-using-fcm-349fff071591)

- [Receiving notifications - Notifications | React Native Firebase](https://rnfirebase.io/docs/v4.3.x/notifications/receiving-notifications)

- [react-native-firebase-docs/docs/messaging at master ·](https://github.com/invertase/react-native-firebase-docs/tree/master/docs/messaging)

- [firebasePushnotificaiton/FirebaseNotifiction/android/app/src/main at master ·](https://github.com/rohitmodi12/firebasePushnotificaiton/tree/master/FirebaseNotifiction/android/app/src/main)

- [firebasePushnotificaiton/FirebaseNotifiction at master ·](https://github.com/rohitmodi12/firebasePushnotificaiton/tree/master/FirebaseNotifiction)

- [styled-components: Basics](https://styled-components.com/docs/basics)

- [APNS, GCM & FCM Tester](https://pushtry.com/)

- [firebase project – Database – Firebase console](https://console.firebase.google.com/u/1/project/fir-project-c2cdf/database/firestore/data~2Ffcm-tokens~2F4l4gqHOGXEAIpuXmLxWY)

- [Get started with Cloud Firestore Firebase](https://firebase.google.com/docs/firestore/quickstart)

- https://www.youtube.com/watch?v=nHvw1mcaOs0

- [Firebase Notification Integration in React Native 0.60+](https://medium.com/@katharinep/firebase-notification-integration-in-react-native-0-60-3a8d6c8d56ff)

- https://rnfirebase.io/docs/v5.x.x/notifications/introduction

- [Firebase Cloud Messaging | React Native Firebase | Invertase](https://invertase.io/oss/react-native-firebase/v6/messaging)

- [react native - How to get all of device tokens from Firebase?](https://stackoverflow.com/questions/43060846/how-to-get-all-of-device-tokens-from-firebase)

- [android - Firebase Cloud Messaging function sendToDevice not working](https://stackoverflow.com/questions/45423966/firebase-cloud-messaging-function-sendtodevice-not-working)

- [Messaging | Admin Node.js SDK Firebase](https://firebase.google.com/docs/reference/admin/node/admin.messaging.Messaging#sendtodevice)

- [Your server environment and FCM Firebase](https://firebase.google.com/docs/cloud-messaging/server)

- [Sending Firebase Cloud Messages from a Node.js Server](https://www.youtube.com/watch?v=6uZ7Fw8AVlk)

- [Firebase Push notifications in React NativeApps](https://enappd.com/blog/firebase-push-notifications-in-react-native/81/)

### graphs

- [indiespirit/react-native-chart-kit: 📊React Native Chart Kit: Line Chart, Bezier Line Chart, Progress Ring, Bar chart, Pie chart, Contribution graph](https://github.com/indiespirit/react-native-chart-kit)

### Icons

- [react-native-vector-icons/FONTAWESOME5.md at master ·](https://github.com/oblador/react-native-vector-icons/blob/master/FONTAWESOME5.md)

### Learning Goals

- [Upgrade React Native applications](https://react-nativecommunity.github.io/upgrade-helper/)

- [Upgrading to new React Native versions · React Native](https://facebook.github.io/react-native/docs/upgrading)

- [Announcing React Native 0.60 · React Native](https://facebook.github.io/react-native/blog/2019/07/03/version-60)

- [Learning Goals saved at NextGenI ](https://docs.google.com/document/d/1o9D9ZdCAk0PuQdq9eTbWDgknO8IiT8ybZEMvbiWeQEc/edit)

### native base

- [NativeBase-Customizer](https://nativebase.io/customizer/)

### Pending RND's

- [Linting and Formatting with ESLint in VS Code ― Scotch.io](https://scotch.io/tutorials/linting-and-formatting-with-eslint-in-vs-code)

- [Supporting safe areas · React Navigation](https://redux-saga.js.org/)
- [Read Me · Redux-Saga](https://reactnavigation.org/docs/en/handling-iphonex.html)

### React native image picker

- [ivpusic/react-native-image-crop-picker: iOS/Android image picker with support for camera, video, configurable compression, multiple images and cropping](https://github.com/ivpusic/react-native-image-crop-picker)

- [How to avoid keyboard pushing layout up on Android react-native](https://stackoverflow.com/questions/42840555/how-to-avoid-keyboard-pushing-layout-up-on-android-react-native)

- [How to add multiple image using react native image picker](https://stackoverflow.com/questions/45543706/how-to-add-multiple-image-using-react-native-image-picker)

### react-native-share-element

- [IjzerenHein/react-native-shared-element: Native shared element transition "primitives" for react-native 💫](https://github.com/IjzerenHein/react-native-shared-element)

### Responsive font size

- [ios - React Native Responsive Font Size](https://stackoverflow.com/questions/33628677/react-native-responsive-font-size)

- [PixelRatio · React Native](https://facebook.github.io/react-native/docs/pixelratio.html)

### Social SignIn

### Facebook Login

- [facebook/facebook-android-sdk: Used to integrate Android apps with Facebook Platform.](https://github.com/facebook/facebook-android-sdk)

- [Getting Started - Android SDK](https://developers.facebook.com/docs/android)
- [Android SDK](https://developers.facebook.com/docs/android/getting-started/)

- [Android - Facebook Login](https://developers.facebook.com/docs/facebook-login/android/v2.2)

- [Android - Facebook Login](https://developers.facebook.com/docs/facebook-login/android)

- [Login - React Native SDK](https://developers.facebook.com/docs/react-native/login/)

- [facebook/react-native-fbsdk: A React Native wrapper around the Facebook SDKs for Android and iOS. Provides access to Facebook login, sharing, graph](https://github.com/facebook/react-native-fbsdk)

- [Getting Key Hash for Facebook Console - About React](https://aboutreact.com/getting-key-hash-for-facebook-console/)

- [Quick Starts - Facebook for Developers](https://developers.facebook.com/quickstarts/477714742908204/?platform=android)

- [Android - Facebook Login](https://developers.facebook.com/docs/facebook-login/android/)

- [Facebook login in React native - Mehran Khan - Medium](https://medium.com/@mehran.khan/integrating-fbsdk-facebook-login-in-react-native-7b7600ce74a7)

- [Android Facebook integration with invalid key hash](https://stackoverflow.com/questions/23674131/android-facebook-integration-with-invalid-key-hash)

### Google SignIn

- [Example of Google Sign In in React Native Android and iOS App](https://aboutreact.com/example-of-google-sign-in-in-react-native/)

- [react-native-community/react-native-google-signin: Google Signin for your React Native applications](https://github.com/react-native-community/react-native-google-signin)

- [react-native-google-signin/android-guide.md at master ·](https://github.com/react-native-community/react-native-google-signin/blob/master/docs/android-guide.md)

- [Getting SHA1 Fingerprint for Google API Console - About React](https://aboutreact.com/getting-sha1-fingerprint-for-google-api-console/)

- [How to Integrate Firebase in React Native Android and iOS App](https://aboutreact.com/integrate-firebase-in-android-and-ios-app/)

- [react-native-google-signin/android-guide.md at master ·](https://github.com/react-native-community/react-native-google-signin/blob/master/docs/android-guide.md)

- [Authenticating Your Client Google APIs for Android](https://developers.google.com/android/guides/client-auth)

- [Get an API Key Maps SDK for Android Google](https://developers.google.com/maps/documentation/android-sdk/get-api-key#fingerprint)

- [react-native-community/google-signin DEVELOPER_ERROR on real device · Issue #451 ·](https://github.com/react-native-community/google-signin/issues/451)

- [React-Native: Facebook and Google Login](https://stackoverflow.com/questions/44577495/react-native-facebook-and-google-login)

- [Social login with React Native - Bene Studio](https://blog.benestudio.co/social-login-with-react-native-6157ba3cff1c)

- [Keystore file '/Project-Folder/android/app/debug.keystore' not found for signing config 'debug' in react-native 0.60 · Issue #25629 ·](https://github.com/facebook/react-native/issues/25629)

- [fullstackreact/react-native-oauth: A react-native wrapper for social authentication login for both Android and iOS](https://github.com/fullstackreact/react-native-oauth)

### Splash Screen

- [How to Add a Splash Screen to a React Native App](https://medium.com/handlebar-labs/how-to-add-a-splash-screen-to-a-react-native-app-ios-and-android-30a3cec835ae)

- [Remove Background from Image – remove.bg](https://www.remove.bg/upload)

### Swiper

- [Create a Snapping Image Swiper like Instagram with React](https://codedaily.io/tutorials/67/Create-a-Snapping-Image-Swiper-like-Instagram-with-React)

- [react-native-image-slider-show](https://www.npmjs.com/package/react-native-image-slider-show)

### Upload App platforms

- [Upload your App - Diawi - Development and In-house Apps- [Wireless Installation](https://www.diawi.com/)

- [Installr - Easy iOS and Android beta app distribution](https://www.installrapp.com/)

- [TestFairy - Mobile beta testing done right](https://wetransfer.com/)
- [WeTransfer](https://www.testfairy.com/pricing)

### Video

- [Issues · itsnubix/react-native-video-controls](https://github.com/itsnubix/react-native-video-controls/issues)

- [Issues · react-native-community/react-native-video](https://github.com/react-native-community/react-native-video/issues?q=is%3Aopen+is%3Aissue)

- [controls](https://github.com/itsnubix/react-native-video-controls)

### React Native Bookmarks

- [React Native Crash Course](https://www.youtube.com/watch?v=mkualZPRZCs)

- [Android SDK & AVD Setup For React Native](https://www.youtube.com/watch?v=KRLLjlpy0r4)

- [Getting Started · React Native](https://facebook.github.io/react-native/docs/getting-started.html)

- [react-community/react-native-image-picker: A React Native module that allows you to use native UI to select media from the device library or directly from](https://github.com/react-community/react-native-image-picker)

- [react-native-community/react-native-camera: A Camera component for React Native. Also supports barcode scanning!](https://github.com/react-native-community/react-native-camera)

- [ES6 - JavaScript Improved | Udacity](https://www.udacity.com/course/es6-javascript-improved--ud356)

- [Simple login system using React Native, Firebase and Nativebase - Hashnode](https://hashnode.com/post/simple-login-system-using-react-native-firebase-and-nativebase-civwpo89u0lwyqe539bm66g0j)

### Deep link in react native

- [Create Deep Links to App Content Android Developers](https://developer.android.com/training/app-links/deep-linking)

- [Add Android App Links Android Developers](https://developer.android.com/studio/write/app-link-indexing)

- [Deep Linking Your React Native App | by Nader Dabit | React Native Training](https://medium.com/react-native-training/deep-linking-your-react-native-app-d87c39a1ad5e)

- [create deep link to app content in react native - Google Search](https://www.google.com/search?ei=459kX46vHpXQgwe6lq2gCg&q=create+deep+link+to+app+content+in+react+native&oq=create+deep+links+to+app+content+in+react+nat&gs_lcp=CgZwc3ktYWIQAxgAMggIIRAWEB0QHjIICCEQFhAdEB46BAgAEEc6AggAOgYIABAWEB46BQghEKABOgcIIRAKEKABUKcIWPEpYOc3aAFwAngAgAHLAogBoxySAQYyLTEzLjGYAQCgAQGqAQdnd3Mtd2l6yAEIwAEB&sclient=psy-ab)

- [Enable other businesses to accept payments directly](https://stripe.com/docs/connect/enable-payment-acceptance-guide#setup)

- [Creating direct charges](https://stripe.com/pricing)
- [Pricing & fees | Stripe](https://stripe.com/docs/connect/direct-charges)

- [default_cover.png](https://static.askwho.com/ask_who/profile_image/default_cover.png)

- [Using WebSockets on Heroku with Node.js | Heroku Dev Center](https://devcenter.heroku.com/articles/node-websockets)

- [Logging | Heroku Dev Center](https://devcenter.heroku.com/articles/logging)

### wheel Picker

- [AigeStudio/WheelPicker: Simple and fantastic wheel view in realistic effect for android.](https://github.com/AigeStudio/WheelPicker)

- [GregFrench/react-native-wheel-picker](https://github.com/GregFrench/react-native-wheel-picker)

- [react-native-wheel-picker / JS.coach](https://js.coach/react-native-wheel-picker?search=picker&collection=React+Native)

- [Fixed issue #75 · GregFrench/react-native-wheel-picker@aa4df1a](https://github.com/GregFrench/react-native-wheel-picker/commit/aa4df1a4f1ff9dc91f07198d47b92a19d1d69c25)

- [I got "Build failed" when i go genarate de apk file "./gradlew assembleRelease" · Issue #54 · lesliesam/react-native-wheel-picker](https://github.com/lesliesam/react-native-wheel-picker/issues/54)

- [kalontech/ReactNativeWheelPicker](https://github.com/kalontech/ReactNativeWheelPicker)

- [Issues · DelightfulStudio/react-native-wheel-picker-android](https://github.com/DelightfulStudio/react-native-wheel-picker-android/issues)

- [JS.coach](https://js.coach/?search=picker&collection=React+Native)

### react-navigation

- [Navigation options resolution · React Navigation](https://reactnavigation.org/docs/en/navigation-options-resolution.html#a-drawer-has-a-stack-inside-of-it-and-you-want-to-lock-the-drawer-on-certain-screens)

### React-Native-build

### Srink apk size

- [Shrink your React Native application size dramatically!](https://medium.com/@rishii.kumar.chawda/reduce-your-react-native-app-size-dramatically-5430d773c92f)

- [Using Hermes · React Native](https://facebook.github.io/react-native/docs/hermes)

### Payment gateways in react native

- [Accept Payments Online with Checkout.com - Global Payment Processing](https://www.checkout.com/)

### stripe

- [Set up Stripe in React Native + NodeJS](https://blog.bam.tech/developer-news/setup-stripe-react-native-nodejs)

- [Online payment processing for internet businesses - Stripe](https://stripe.com/)

- [Installation · tipsi-stripe](https://tipsi.github.io/tipsi-stripe/docs/installation.html)

- [javascript - How to implement Stripe with React Native?](https://stackoverflow.com/questions/40092731/how-to-implement-stripe-with-react-native/41395930#41395930)

- [tipsi/tipsi-stripe: React Native Stripe binding for iOS/Android platforms](https://github.com/tipsi/tipsi-stripe)

- [Testing | Stripe Payments](https://stripe.com/docs/testing)

- [Stripe payment integration in React Native apps usingFirebase](https://enappd.com/blog/stripe-integration-in-react-native-apps-using-firebase/108/)

- [Accepting payments in React Native](https://pusher.com/tutorials/react-native-payments)

- [stripe/stripe-android: Stripe Android SDK](https://github.com/stripe/stripe-android)

- [Using Stripe API in React Native with fetch | BigBinary Blog](https://blog.bigbinary.com/2015/11/03/using-stripe-api-in-react-native-with-fetch.html)

- [.paymentRequestWithCardForm(options) -&gt; Promise · tipsi-stripe](https://tipsi.github.io/tipsi-stripe/docs/paymentrequestwithcardform.html)

- [.createTokenWithCard(params) -&gt; Promise · tipsi-stripe](https://tipsi.github.io/tipsi-stripe/docs/createtokenwithcard.html)

### Nextgeni recommed Plugins

### Wheel picker

- [react-native-wheel-picker-android](https://www.npmjs.com/package/react-native-wheel-picker-android)

- [Issues in plugins ](https://docs.google.com/document/d/19ANuM4-M-mMI9uZ-a4y590DrNgzyXu2hvDu8cQKscxE/edit)

- [Linux commands ](https://docs.google.com/document/d/1vtTleU-kMb1cUBR8crbXLiebwxl5fi7IiA16N4lmdkE/edit?ts=5e2ae301)

- [react-native-vector-icons directory](https://oblador.github.io/react-native-vector-icons/)

- [React native fixes ](https://docs.google.com/document/d/12kEdfs9J-xmT4l4VMx4-BnZ3iYGe1vYG4M2dd1RYy64/edit)

### React Native

### Native Base

- [GitHub - GeekyAnts/NativeBase-KitchenSink: An example app with all the UI components of NativeBase](https://github.com/GeekyAnts/NativeBase-KitchenSink)

- [Getting Started · NativeBase](https://snack.expo.io/)
- [amused strawberries](https://docs.nativebase.io/docs/GetStarted.html)

- [React Native Express](http://www.reactnativeexpress.com/)
- [Getting started · React Navigation](https://reactnavigation.org/docs/en/getting-started.html)

- [React Native School](https://www.youtube.com/playlist?list=PLjVnDc2oPyOGBOb75V8CpeSr9Gww8pZdL&fbclid=IwAR2Rbaay7p42AG7ATLoXBLkj159EnJ5kmA5bVlJMjshKly9Dzuyoq703vWs)

- [Course | CS50M | edX](https://courses.edx.org/courses/course-v1:HarvardX+CS50M+Mobile/course/)

- [Introduction to the Back End | The Odin Project](https://www.theodinproject.com/courses/web-development-101/lessons/introduction-to-the-back-end)

- [Kickresume | Souq web developer](https://www.kickresume.com/dashboard/2/677409/)

- [Flexbox Froggy - A game for learning CSS flexbox](http://flexboxfroggy.com/)

- [Grid Garden - A game for learning CSS grid](http://cssgridgarden.com/)

### react native

- [PermissionsAndroid · React Native](https://facebook.github.io/react-native/docs/permissionsandroid)

- [yonahforst/react-native-permissions: Check and request user permissions in ReactNative](https://github.com/yonahforst/react-native-permissions)

- [Simple React Native Map Example to integrate the Map into RN App](https://aboutreact.com/react-native-map-example/)

- [Why Android developers should pay attention to React Native in 2021 | by Joel](https://medium.com/codex/why-android-developers-should-pay-attention-to-react-native-in-2021-ae4a3c737167?fbclid=IwAR0XymeqDptGBh-6G5JE_9sLZ0gZ8S39oPA9Jinb3j7GAx8lg19W99OTl0Q)

- [Why Android developers should pay attention to React Native in 2021 | by Joel](https://medium.com/codex/why-android-developers-should-pay-attention-to-react-native-in-2021-ae4a3c737167)

- [Awesome React Native components, news, tools, and learning material! | Awesome React Native](https://www.awesome-react-native.com/#conferences)

- [GitHub - facebook/react-native-website: The site and docs for React Native](https://dev.to/notifications)
- [Notifications - DEV Community 👩‍💻👨‍💻 ](https://github.com/facebook/react-native-website)

- [GitHub - jondot/awesome-react-native: Awesome React Native components, news, tools, and learning material!](https://github.com/jondot/awesome-react-native)

- [flexbox - flex vs flexGrow vs flexShrink vs flexBasis in React Native?](https://stackoverflow.com/questions/43143258/flex-vs-flexgrow-vs-flexshrink-vs-flexbasis-in-react-native)

- [How to Run macOS on Windows 10 in a Virtual Machine](https://www.makeuseof.com/tag/macos-windows-10-virtual-machine/)

- [Android Asset Studio](https://romannurik.github.io/AndroidAssetStudio/index.html)

- [Random Car Generator](https://randomlistgenerator.com/car)
- [Random User Generator | Photos](https://randomuser.me/photos)
- [Different Types Of Cars List - NDTV CarAndBike](https://auto.ndtv.com/news/types-of-cars-1450327)

- [Types of Cars with Pictures | Car Brand Names.com](http://www.car-brand-names.com/types-of-cars/)

- [Jobs in Pakistan, Search Latest Government Jobs, Careers](https://jobsalert.pk/)

- [sudheerj/angular-interview-questions: List of 300 Angular Interview Questions](https://www.indeed.com.pk/)

- [Job Search | Indeed](https://github.com/sudheerj/angular-interview-questions)

- [Learn Angular - Full Tutorial Course](https://www.youtube.com/watch?v=2OHbjep_WjQ&vl=en)

- [Top Angular Interview Questions You Must Prepare For 2019 | Edureka](https://www.edureka.co/blog/interview-questions/top-angularjs-interview-questions-2016/)

- [Free Download - Learn Photoshop, Web Design & Profitable Freelancing](http://technozune.com/index.php/2019/08/23/learn-photoshop-web-design-profitable-freelancing/)

- [Simple Programming Problems](https://adriann.github.io/programming_problems.html)

### Mobile App Templates in React Native

- [Mobile App Templates in React Native - Free Download Instamobile](https://www.instamobile.io/templates/)

- [6+ React Native Mobile App Templates @ Creative Tim](https://www.creative-tim.com/templates/react-native)

- [15 React Native Component Libraries You Should Know in 2020/2021](https://www.codeinwp.com/blog/react-native-component-libraries/)

### car wash app

- [Mobile Car Wash Equipment](https://www.youtube.com/watch?v=LDtbGZCqeBE)

- [Start-up, app aim to revamp the car wash YouTube](https://www.youtube.com/watch?v=c9SBpC-hCM4)

- [EVOCLEAN WATER LESS CAR WASH !](https://www.youtube.com/watch?v=EJHfARFgAFM)

- [Build a Login/Auth App with the MERN Stack — Part 1](https://blog.bitsrc.io/build-a-login-auth-app-with-mern-stack-part-1-c405048e3669)

- [with Passport.js and JWT GitHub - rishipr/mern-auth: MERN + Redux user authentication boilerplate](https://github.com/rishipr/mern-auth/)

- [Building a Log In System for a MERN Stack – Keith Weaver – Medium](https://medium.com/@Keithweaver_/building-a-log-in-system-for-a-mern-stack-39411e9513bd)

- [GitHub - andycandomore/mern-stack: 🌐 MERN stack 2.0 I have built 12 MERN app in production based on this setup](https://github.com/andycandomore/mern-stack)

- [GitHub - djizco/boilerplate-mern: A Full MERN Stack Boilerplate for Web Apps including a local authentication system. Uses React 16, Express.js, MongoDB,](https://github.com/djizco/boilerplate-mern)

- [Redux, Passport.js, Webpack 4, Testing, and more M.E.R.N stack application using Passport for authentication.](https://hackernoon.com/m-e-r-n-stack-application-using-passport-for-authentication-920b1140a134)

- [MERN v2.0 - Build production ready universal apps easily](http://mern.io/)

- [Starting with Authentication A tutorial with Node.js and MongoDB](https://medium.com/createdd-notes/starting-with-authentication-a-tutorial-with-node-js-and-mongodb-25d524ca0359)

- [Android Asset Studio - Launcher icon generator](<https://romannurik.github.io/AndroidAssetStudio/icons-launcher.html#foreground.type=image&foreground.space.trim=1&foreground.space.pad=0&foreColor=rgba(96%2C%20125%2C%20139%2C%200)&backColor=rgb(68%2C%20138%2C%20255)&crop=1&backgroundShape=square&effects=shadow&name=launch_screen>)
