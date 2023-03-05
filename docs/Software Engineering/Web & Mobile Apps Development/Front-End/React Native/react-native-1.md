# React Native

**Creating a new application**

> If you previously installed a global react-native-cli package, please remove it as it may cause unexpected issues.

React Native has a built-in command line interface, which you can use to generate a new project. You can access it without installing anything globally using npx, which ships with Node.js. Let's create a new React Native project called "AwesomeProject":

https://reactnative.dev/docs/environment-setup

**Images from Device storage custom path In React Native**

I have an Image that I've downloaded and saved to the path /data/user/0/com.project/files/assets/image.png and I want to use this in my Image component in React-Native. Is there a way to use images stored in this path?

If it's a file on your device, I think the way of displaying it is somewhat like this:

```js showLineNumbers
<Image
  source={{ uri: "file:///data/user/0/com.project/files/assets/image.png" }}
  style={{ width: 100, height: 100 }}
/>
```

Just make sure the file path is from the root. Hope it works for you.

https://stackoverflow.com/questions/51209891/images-from-device-storage-custom-path-in-react-native

**How do you hide the warnings in React Native iOS simulator?**

According to React Native Documentation, you can hide warning messages by setting disableYellowBox to true like this:

```js showLineNumbers

console.disableYellowBox = true;
Update: React Native 0.63+
console.disableYellowBox is removed and now you can use:

import { LogBox } from 'react-native';
LogBox.ignoreLogs(['Warning: ...']); // Ignore log notification by message
LogBox.ignoreAllLogs();//Ignore all log notifications
```

https://stackoverflow.com/questions/35309385/how-do-you-hide-the-warnings-in-react-native-ios-simulator

**React Native OTP Input (used by other developers in sweet connect app not ideal approach I guess)**

@twotalltotems/react-native-otp-input is a tiny Javascript library which provides an elegant UI for the end user to input one time passcode (OTP). It handles the input suggestion on iOS when the OTP SMS is received. For Android, it will autofill when the user presses the copy button on the SMS notification bar. It also features a carefully crafted flow to handle edge cases for volatile user gestures. We provide default UI, but you can always customize the appearance as you like.

https://www.npmjs.com/package/@twotalltotems/react-native-otp-input

## OTP input in react native

OTP picker react native
OTPInputView react native

Solution:

react-native-confirmation-code-field

https://www.npmjs.com/package/react-native-confirmation-code-field

https://www.npmjs.com/package/react-native-confirmation-code-field

Demo:

https://camo.githubusercontent.com/543de61a3529d1cdd39111c945acc4b24434ebb1a69a6b69d6122ab8e6d92919/68747470733a2f2f6d656469612e67697068792e636f6d2f6d656469612f68754a727146305952724e4a425477556d7a2f67697068792e676966

https://github.com/retyui/react-native-confirmation-code-field/tree/4f9637acb4d26c9c9a95b5acf901d140825a7c5e/examples/DemoCodeField/src/AnimatedExample

Code: https://github.dev/retyui/react-native-confirmation-code-field/blob/4f9637acb4d26c9c9a95b5acf901d140825a7c5e/examples/DemoCodeField/src/AnimatedExample/index.js

![image](../../../../../assets/images/image129.png)

https://github.com/retyui/react-native-confirmation-code-field/blob/4f9637acb4d26c9c9a95b5acf901d140825a7c5e/examples/DemoCodeField/src/MaskExample/index.js

**What Is a Blob?**

According to Wikipedia: "**A binary large object (BLOB or blob)** is a collection of binary data stored as a single entity. **Blobs are typically images, audio, or other multimedia objects**, though sometimes binary executable code is stored as a blob."

What this means is that a blob is essentially a container for data, so it's more easily handled by protocols that fetch and manipulate large media files. So, if you're planning on working in an application with limited resources handling media files like photos or music, you'll be handling blobs.

**Toast in react native (used in sweetconnect project)**

https://www.npmjs.com/package/react-native-flash-message

**Make Use of requestAnimationFrame**

Sometimes, if we do an action in the same frame that we are adjusting the opacity or highlight of a component that is responding to a touch, we won't see that effect until after the onPress function has returned. If onPress does a setState that results in a lot of work and a few frames dropped, this may occur. A solution to this is to wrap any action inside of your onPress handler in requestAnimationFrame :

```js showLineNumbers

handleOnPress() {
    requestAnimationFrame(() => {
        this.doExpensiveAction();
    });
}
```

https://www.pluralsight.com/guides/how-to-use-requestanimationframe-with-react

**React-native-background-timer **

used this package in hisaab package by zohaib after QA report an issue of timer not working when app isint background state and it was working fine using this package.
for run timer in background as well

> "react-native-background-timer": "^2.4.1”,

**generate random phone number method javascript**

```js showLineNumbers

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

```js showLineNumbers

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

**React native geolocation**

**how to get user location using react-native-maps**

@react-native-community/geolocation seems to be deprecated, upvote for @ggDeGreat.

https://www.npmjs.com/package/react-native-geolocation-service

https://stackoverflow.com/questions/47558468/how-to-get-current-location-using-react-native-maps

How to get current location using react-native-maps

**Location permission in react native**

how to check has Location Permission in react native

https://stackoverflow.com/questions/38371987/determining-if-geolocation-enabled-with-react-native

https://stackoverflow.com/questions/45822318/how-do-i-request-permission-for-android-device-location-in-react-native-at-run-t

**react native masked text**

https://www.npmjs.com/package/react-native-masked-text

**what is Watchman for react native**

React Native uses watchman **to detect when you've made code changes and then automatically build and push the update to your device without you needing to manually refresh it.** 14-Feb-2017

https://stackoverflow.com/questions/42235799/what-is-the-use-of-watchman-for-react-native#:~:text=React%20Native%20uses%20watchman%20to,needing%20to%20manually%20refresh%20it.

### Packages:

**react-native-calendars**

https://www.npmjs.com/package/react-native-calendars

**react-native-app-settings**

https://www.npmjs.com/package/react-native-app-settings

### Deep Linking

**Deep linking can be named as pending intent in android native**

pending intent in android notification

https://developer.android.com/training/notify-user/navigation

**How to do deep linking using react navigation?**

https://reactnavigation.org/docs/deep-linking/ (isme android ios both k liye hy recommended)
https://blog.jscrambler.com/how-to-handle-deep-linking-in-a-react-native-app
https://stackoverflow.com/questions/55086526/how-to-open-app-with-an-url-specific-react-native
https://www.youtube.com/watch?v=_fVNt1KjkEk&ab_channel=UnsureProgrammer tutorial
https://blog.logrocket.com/understanding-deep-linking-in-react-native/
https://github.com/dabit3/react-native-deep-linking
https://medium.com/react-native-training/deep-linking-your-react-native-app-d87c39a1ad5e
https://www.youtube.com/watch?v=rvDq2WMU4mw&t=13s
https://github.com/saadibrahim/react-native-deep-links

Firebase also provide dynamic deep linking #deeplinking for react native (hammad ali khan android developer at ngi recommended this he has implemented this)

Inka Use Case ye tha unka :
K agr koi deeplnk pe click krta hy or agr mobile me app install nhe hy to wo mobile app to open nhe kr satka wo/firebase google play store pe redirect kr k open kr dyta hy app in goolge play store.

**Watch video in below link for details.**

https://firebase.google.com/products/dynamic-links?gclid=Cj0KCQiA_8OPBhDtARIsAKQu0gbHiXYIrSpLFvUY4I-X0DpJK77QD08ThSjxiFu-L7LGp7mALUTG5KUaAidJEALw_wcB&gclsrc=aw.ds

**Implement deep linking in React Native apps using Universal links and URL schema**

https://www.youtube.com/watch?v=rvDq2WMU4mw&ab_channel=SaadIbrahim
https://stackoverflow.com/questions/52795246/linking-in-react-native-can-open-just-one-app
https://medium.com/wolox/ios-deep-linking-url-scheme-vs-universal-links-50abd3802f97

### Animation in react native :

**Animation in react native:**

https://docs.google.com/document/d/1ATI-NfzgOQjMUpek-yOtH-GxuGAQsXgYxfj3zqKKBpw/edit

**Flatlist animation in react native**

https://www.youtube.com/watch?v=V2FEEgeEk_o&ab_channel=BrunoOliveira

https://start-react-native.dev/

**Animation in react native from one point to another**

How to change Text in Animation in react-native?

```js showLineNumbers
//ConnectingActivityLoader.tsx

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
```

Usage:

```js showLineNumbers
return <ConnectingActivityLoader />;
```

**How to animate a Single View one by one in react native?**

move from one point to another in x or y axis animation in react native?
sol:

https://snack.expo.dev/rJjzdKC04
https://stackoverflow.com/questions/56561761/how-to-animate-a-single-view-one-by-one-in-react-native

> #### QRCode in react native

**How to generate QR code in react native ?**

Generation of QR Code in React Native is very easy as we just have to install react-native-svg and react-native-qrcode-svg package, which will provide `<QRCode/>` components to make QRCode. QR Code is known as Quick Response Code is a trademark for a two-dimensional barcode.

https://aboutreact.com/generation-of-qr-code-in-react-native/#:~:text=Generation%20of%20QR%20Code%20in%20React%20Native%20is%20very%20easy,for%20a%20two%2Ddimensional%20barcode.

**React-native-qrcode-svg (recommended)**

https://www.npmjs.com/package/react-native-qrcode-svg

**react-native-qrcode-svg** : This is the best solution I found and works like charm, so I decided to move ahead with this.

**react-native-qrcode-image** worked but with some work around as its using few updated internal dependency that’s not updated. (Not recommended )

https://medium.com/@mushtaque87/qrcode-generator-for-react-native-391ae401e275

**React-native-qrcode (not recommended)**

https://www.npmjs.com/package/react-native-qrcode

Environment Variables in React native: (.env)

Tools like react-native-dotenv and react-native-config are great for adding environment-specific variables like API endpoints, but they should not be confused with server-side environment variables, which can often contain secrets and API keys.

https://reactnative.dev/docs/security#storing-sensitive-info

What is Flipper React Native?

What is Flipper? Flipper is **a highly extensible mobile app debugger used to debug iOS, Android and React Native applications**. It lets you inspect, control, and visualize your application from its desktop application.04-Mar-2022

Does react native use native components?

React Native is like React, but **it uses native components** instead of web components as building blocks. So to understand the basic structure of a React Native app, you need to understand some of the basic React concepts, like JSX, components, state , and props .

what is Codegen in react native

Using the Codegen is not mandatory: all the code that is generated by it can also be written manually. However, it **generates scaffolding code that could save you a lot of time**. The Codegen is invoked automatically by React Native every time an iOS or an Android app is built.19-Aug-2022

How do you use Reactotron?

First, install the correct desktop app for your platform from the releases page. We'll then add the project as a development dependency to our React Native project. Finally, we configure it. First create a config file for Reactotron.11-Jun-2019

what is hermes in react native

Hermes is **a small and lightweight JavaScript engine optimized for running React Native on Android** (you can read more about using it with React Native here. Hermes helps improve app performance and also exposes ways to analyze the performance of the JavaScript that it runs.

"Hermes is a Javascript Engine designed for mobile environments focused on startup performance..."

https://www.youtube.com/watch?v=JsppO1HUYx4&ab_channel=MetaOpenSource

metro in react native

Metro is a JavaScript bundler. It takes in an entry file and various options, **and gives you back a single JavaScript file that includes al**l **your code** and its dependencies.

### Text and cursor are misaligned when using big font sizes #64

Solution:

You can use lineHeight to fix differences between platforms

```css showLineNumbers
    height: 60,
    lineHeight: 60,
    width: 50,
```

https://github.com/retyui/react-native-confirmation-code-field/issues/64
