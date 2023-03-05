# Proguard React Native

**proguard rule for react native svg**

we need to add proguard rules for each libary if its providing support for proguard for react native explicitly

https://github.com/invertase/react-native-firebase/blob/main/tests/android/app/proguard-rules.pro

https://github.com/JesperLekland/react-native-svg-charts-examples/blob/master/android/app/proguard-rules.pro

**Enabling Proguard to reduce the size of the APK (optional)**

Proguard is a tool that can slightly reduce the size of the APK. It does this by stripping parts of the React Native Java bytecode (and its dependencies) that your app is not using.
IMPORTANT: Make sure to thoroughly test your app if you've enabled Proguard. Proguard often requires configuration specific to each native library you're using. See app/proguard-rules.pro.
To enable Proguard, edit android/app/build.gradle:

/\*\*

- Run Proguard to shrink the Java bytecode in release builds.
  \*/

```bash showLineNumbers
def enableProguardInReleaseBuilds = true
```

https://facebook.github.io/react-native/docs/signed-apk-android
