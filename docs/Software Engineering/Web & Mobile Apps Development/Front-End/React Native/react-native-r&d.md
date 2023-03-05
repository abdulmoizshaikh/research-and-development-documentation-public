# react native R&D

### Share data between to Apps

react-native-send-intent

```bash showLineNumbers
npm i react-native-send-intent
```

```jsx showLineNumbers
SendIntentAndroid.isAppInstalled("com.facturationandroid").then(
  (isInstalled) => {
    SendIntentAndroid.openApp("com.facturationandroid", {
      data1: "hello",
      data2: "test",
    }).then((wasOpened) => {});
  }
);
```

this article tell share data between 2 activities in same application using either file component or intent this is not usefull for our usecase:

https://www.npmjs.com/package/react-native-send-intent

https://stackoverflow.com/questions/49550963/sending-simple-data-to-other-apps-using-react-native-in-android

## React.js Conf 2016 - Tadeu Zagallo - Optimising React Native: Tools and Tips

https://www.youtube.com/watch?v=0MlT74erp60&ab_channel=MetaDevelopers

### R&D tasks

**Typescript export type and babel throw Error #11809**
babel parser export type {
Unexpected token in src/index.ts on Expo 42 #1663 in react-native-gesture-handler
node_modules/react-native-gesture-handler/src/index.ts: Unexpected token (5:12)

Solution

Update the version of @babel/core and @babel/runtime from 7.5.0 to 7.9.0 issue fixed

I found the reason.
This is a problem caused by different babel versions, one of which is less than 7.9.0.
thank you very much for your help
https://github.com/babel/babel/discussions/11809
https://github.com/software-mansion/react-native-gesture-handler/issues/1663

**The missing guide to React Native app variants — Part 1**

https://medium.com/supercharges-mobile-product-guide/the-missing-guide-to-react-native-app-variants-part-1-c036fb99ebcc
https://medium.com/@ywongcode/building-multiple-versions-of-a-react-native-app-4361252ddde5
how to define variant in react native
https://stackoverflow.com/questions/39119301/installdebug-not-found-in-root-project-android-react-native

**The number of method references in a .dex file cannot exceed 64k API 17**

Solution:
In android/app/build.gradle
android { compileSdkVersion 23 buildToolsVersion '23.0.0' defaultConfig { applicationId "com.dkm.example" minSdkVersion 15 targetSdkVersion 23 versionCode 1 versionName "1.0" multiDexEnabled true }
Put this inside your defaultConfig:

`multiDexEnabled true`

https://stackoverflow.com/questions/36785014/the-number-of-method-references-in-a-dex-file-cannot-exceed-64k-api-17

**bundling failed: Error: Unable to resolve module `@react-native-community/toolbar-android`from**

Solution:
Error: Unable to resolve module `@react-native-community/toolbar-android`
npm install --save @react-native-community/toolbar-android
https://stackoverflow.com/questions/62769564/error-unable-to-resolve-module-react-native-community-toolbar-android

**RNCAndroidDropdownPicker was not found in the UIManager #3435**

requirenativecomponent was not found in the uimanager native base Picker
Execution failed for task ':@react-native-picker_picker:compileDebugJavaWithJavac’.

solution
Hello, just installing @react-native-picker/picker@^1.9.7 fixes the issue for me.
yarn add @react-native-picker/picker@1.9.7

https://github.com/GeekyAnts/NativeBase/issues/3435

release build creation bugs

> Task :app:bundleConsumerReleaseJsAndAssets FAILED

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.

open project using android studio
android studio will download gradle dependencies inn android folder automatically

## React-native components

1. A library for ready made react native components<br/>
   https://bit.dev/

2. 11 Top React Native Developer Tools for 2020<br/>
   https://blog.bitsrc.io/11-top-react-native-developer-tools-1e019462dd01

3. react native cli to generate boileplate project<br/>
   https://github.com/infinitered/ignite

4. collaps in react native || custom accordion in react native<br/>
   https://stackoverflow.com/questions/67060475/react-native-animated-accordion-drawer-drop-down-collapsible-card
   https://snack.expo.dev/@vipulchandra04/a85348"

5. icons in react native react native vector icons<br/>
   https://oblador.github.io/react-native-vector-icons/

## React Native learning and New Features

learn feature flag in git

https://docs.gitlab.com/ee/operations/feature_flags.html

code push (hm release nhe kr chah rahe to direct code push hojaega release nikalne bagair) (good for minor release not good for larger code)

https://microsoft.github.io/code-push/

publishing private npm packages

https://docs.npmjs.com/creating-and-publishing-private-packages

**How To Structure Firebase Push Notifications In Your React Native App**

https://medium.com/@zainmanji/how-to-structure-firebase-push-notifications-in-your-react-native-app-6847712d1c31

**Hooks in React Native :**

Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

https://reactjs.org/docs/hooks-intro.html

We can use hooks in react native also as same as we use hooks in reactjs.

Example :

```jsx showLineNumbers
import React, { useState } from "react";
import { StyleSheet, Text, View, Button } from "react-native";

export default function App() {
  const [count, setCount] = useState(0);

  return (
    <View style={styles.container}>
      <Text>You clicked {count} times.</Text>
      <Button
        onPress={() => setCount(count + 1)}
        title="Click me"
        color="red"
        accessibilityLabel="Click this button to increase count"
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  instructions: {
    textAlign: "center",
    color: "#333333",
    marginBottom: 5,
  },
});
```

Reference :
https://medium.com/crowdbotics/build-a-react-native-app-with-react-hooks-5498e1d5fdf6

How can you

**React native environment setup on macOS**

It's pretty simple and way more easy than android

https://www.youtube.com/watch?v=_oCQDtDW3j4&ab_channel=DavidGrice

React-native run-ios

Or to select individual simulator you can use below command

React-native run-ios --simulator=”iPhone X”

**How to build multiple apps from one project with different app name, icon, settings,**

5
+50

This is a problem I have been solving in my projects last days. And I think I have some good (not perfect) solution so far.

`Idea.` We don't have any built-in functions to help us handle this case, so we can use some external manipulation that can do the job. What we need is just multiple Android and iOS projects and single JS code base.

`Implementation.` I`ve come to this project structure:

- ios
- android
- manager
- src
  `ios` and `android` folders is well known to you, they are native project folders.
  `src` is a folder with JS code, you can organize it whatever you want
  `manager` is most interesting one. Here we can store multiple native project files. We can have multiple native project folders in it, for example app1-android app1-ios app2-android app2-ios. And when we want to work on app1 we just copy app1-ios and app1-android to our root ios and android folders, so the actual project is app1. When we are done with app1 we can save android and ios folders to our manager and then just copy app2-ios and app2-android to root ios and android. And we are all good to develop our app2.<br/>
  We can do it manually. But we are developers and we can make it much easier. I`ve written a PHP script that makes it as easy as php save.php -a app1 and php set.php -a app1 to copy from manager to root and backwards. Moreover, it takes care of not copying some unimportant staff (pods folder in ios, build in android etc.) and running pod install to ensure we have all pod in actual project.
I stick to one package.json file to have all npm modules installed once, so I don`t have to run npm install after each project switch.<br/>
  Afterall, we can have as much projects as we wish in one repo, we can customize each one independently.<br/>
  PS If you want me to share my scripts I`ll do it as fast as I can (need some time to prepare it for github and to write some more detailed instructions), just let me know.

https://stackoverflow.com/questions/47266053/how-to-build-multiple-apps-from-one-project-with-different-app-name-icon-setti

## Research & development tasks

**Typescript export type and babel throw Error #11809**
babel parser export type {
Unexpected token in src/index.ts on Expo 42 #1663 in react-native-gesture-handler
node_modules/react-native-gesture-handler/src/index.ts: Unexpected token (5:12)

Solution

**Update the version of @babel/core and @babel/runtime from 7.5.0 to 7.9.0 issue fixed**

I found the reason.
This is a problem caused by different babel versions, one of which is less than 7.9.0.
thank you very much for your help

https://github.com/babel/babel/discussions/11809

https://github.com/software-mansion/react-native-gesture-handler/issues/1663

**The missing guide to React Native app variants — Part 1**

https://medium.com/supercharges-mobile-product-guide/the-missing-guide-to-react-native-app-variants-part-1-c036fb99ebcc

https://medium.com/@ywongcode/building-multiple-versions-of-a-react-native-app-4361252ddde5

how to define variant in react native

https://stackoverflow.com/questions/39119301/installdebug-not-found-in-root-project-android-react-native

**The number of method references in a .dex file cannot exceed 64k API 17**
The number of method references in a .dex file cannot exceed 64K

Solution:
In android/app/build.gradle
android { compileSdkVersion 23 buildToolsVersion '23.0.0' defaultConfig { applicationId "com.dkm.example" minSdkVersion 15 targetSdkVersion 23 versionCode 1 versionName "1.0" multiDexEnabled true }
Put this inside your defaultConfig:

```js showLineNumbers

multiDexEnabled true
```

https://stackoverflow.com/questions/36785014/the-number-of-method-references-in-a-dex-file-cannot-exceed-64k-api-17

**bundling failed: Error: Unable to resolve module `@react-native-community/toolbar-android` from**
Solution:
Error: Unable to resolve module `@react-native-community/toolbar-android`
npm install --save @react-native-community/toolbar-android

https://stackoverflow.com/questions/62769564/error-unable-to-resolve-module-react-native-community-toolbar-android

**RNCAndroidDropdownPicker was not found in the UIManager #3435**

requirenativecomponent was not found in the uimanager native base Picker
Execution failed for task ':@react-native-picker_picker:compileDebugJavaWithJavac’.

solution
Hello, just installing @react-native-picker/picker@^1.9.7 fixes the issue for me.
yarn add @react-native-picker/picker@1.9.7

https://github.com/GeekyAnts/NativeBase/issues/3435

release build creation bugs

> Task : app:bundleConsumerReleaseJsAndAssets FAILED

Deprecated Gradle features were used in this build, making it incompatible with Gradle 7.0.
Use '--warning-mode all' to show the individual deprecation warnings.

open project using android studio
android studio will download gradle dependencies inn android folder automatically

same issue on v1 branch making debug build
