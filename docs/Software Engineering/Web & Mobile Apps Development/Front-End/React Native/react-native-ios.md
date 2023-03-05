# React Native IOS

## Publishing to Apple App Store

https://reactnative.dev/docs/publishing-to-app-store

## Making IOS Release in react native

React Native: How to generate iPA file/iOS build || How to upload iOS build on testFlight || Gulsher

https://www.youtube.com/watch?v=d0k20lCZYfI&ab_channel=IntellectDeveloper

---

## Will apple approve an app for beta testing without app icons?

Is app icon is mandatory to publish ios app in testflight

Without app icon you are not able to upload the build. Application Loader will show you the error to add icons in the build.

https://stackoverflow.com/questions/30054643/will-apple-approve-an-app-for-beta-testing-without-app-icons

---

## How to install .ipa downloaded file to IOS simulator or Iphone?

How can I install a .ipa file to my iPhone simulator
how to install .ipa in ios simulator

Solution:

`Just drag and drop .app file to simulator it will install app automatically.`

However, you can extract an app installed in a local simulator, send it to someone else, and have them copy it to the simulator on their machine.

You cannot run an ipa file in the simulator because the ipa file is compiled for a phone's ARM architecture, not the simulator's x86 architecture.

I have checked in iPhone simulator 13(iOS 15.4)

or

10

For Xcode 10, here's an easy way that worked for me for a debug IPA (development profiles)

Unzip the IPA to get the Payload folder.
Within the Payload folder is the app executable.
Drag and drop the app to an open simulator. (You might see a green add button when you drag it over the simulator)
It should install that app on that simulator.

OR

I found an .ipa file that I wanted using iTunes and copied it over to my desktop.

After that I changed the extension to .zip and extracted it.

Next I found the Payload folder and moved the application inside to my desktop.

Finally I moved that application to my iPhone simulators applications folder found at:

HD

- Applications
- Xcode.app (right click - Show Package Contents)
- Contents
- Developer
- Platforms
- iPhoneSimulator.platform
- SDKs
- iPhoneSimulator6.0.sdk
- Applications
- Hope this helps! (Note: Some apps crash more often than others.)

https://stackoverflow.com/questions/517463/how-can-i-install-a-ipa-file-to-my-iphone-simulator

## How to convert an archive (.app) to .ipa in iTunes 12.7.0 onwards?

Got a solution.

XCode -> Archive -> Select project in Organizer -> Show in Finder -> Show Package contents -> Products -> Applications -> "Product.app".

Create a folder named "Payload" -> Put "Product.app" with in "Payload" -> Compress "Payload" -> Get "Payload.zip" -> Change name to "Product.ipa".

https://stackoverflow.com/questions/46671832/how-to-convert-an-archive-app-to-ipa-in-itunes-12-7-0-onwards

https://gist.github.com/bananita/8039021

Create an IPA and APK From a React Native Project

https://betterprogramming.pub/create-ipa-and-apk-from-react-native-72fe53c6a8db

---

How to build .ipa application for react-native-ios? [closed]

```bash showLineNumbers
Get the .app file:

 react-native run-ios --configuration=release
.app file path Build/Products/Release/"<Your_Filename>.app".

Convert .app to .ipa :

Create folder Payload.
paste .app file into Payload folder.
compress the Payload folder.
change the name you want and put extension as .ipa.
```

https://stackoverflow.com/questions/42110496/how-to-build-ipa-application-for-react-native-ios
