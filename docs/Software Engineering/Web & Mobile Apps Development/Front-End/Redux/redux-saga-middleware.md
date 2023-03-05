# Redux Saga

buffer limit
https://github.com/redux-saga/redux-saga/pull/530

### Redux saga

**Fixes redundant action against same call**

From
takeEvery(AuthTypes.SIGN_UP, signUpUser),
to
takeLatest(AuthTypes.SIGN_UP, signUpUser),

![image](https://s3-bucket-for-image-hosting.github.io/research-website-images-repo/assets/images/image168.png)

Action jaise hi call hoga to saga ka subscribed event call hojaega jo k success or failed ka action call krke redux ko update krega

**Where to show bottom tab navigator in UI design**

Best practice to show bottom tab navigation
Jis screen main back arrow ata hy wahan pe hm bottom tab navigation nhe dikhate

Yield 2 chezain return krta hy
1- data returned from generator function
2-next to continue processing generator function from that point where its returns last

**How to disable night /dark mode in my application even if night mode is enable in android 9.0 (pie)?
Or
force disable dark mode work done in order to fix color inversion issues in different places of UI in dark mode
Or
how to disable app color changing on dark mode in react native **

disable dark mode react native
On IOS:
Go to ios > _name_app_ > Info.plist and add inside <dict></dict>:
<key>UIUserInterfaceStyle</key>
<string>Light</string>
On Android:
Go to android > app > src > main > values > styles.xml and add inside <style></style>
<item name="android:forceDarkAllowed">false</item>

Working example for Android

```jsx showLineNumbers
Change this line  DayNight => Light (will work then)

   <style name="AppTheme" parent="Theme.AppCompat.DayNight.NoActionBar">

to this as well

   <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">



<resources>

   <!-- Base application theme. -->
   <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
       <!-- Customize your theme here. -->
       <item name="android:forceDarkAllowed">false</item>
   </style>

</resources>

```

https://github.com/facebook/react-native/issues/27876
https://stackoverflow.com/questions/57175226/how-to-disable-night-mode-in-my-application-even-if-night-mode-is-enable-in-andr/64339016#64339016
https://www.codegrepper.com/code-examples/whatever/disable+dark+mode+react+native

**How to disable keyboard in input react native**

```jsx showLineNumbers
  editable={false}
```

https://stackoverflow.com/questions/51135278/how-to-disable-keyboard-in-react-native

Todo app using redux saga

https://codesandbox.io/s/todo-app-redux-saga-zc0to?file=/src/task/components/taskList.js

redux saga is completely based upon **generator functions**

"Saga works like a separate thread or a background process that is solely

responsible for making your side effects or API calls unlike redux-thunk,
which uses callbacks which may lead to situations like 'callback hell' in some cases.
However, with the async/await system, this problem can be minimized in redux-thunk.21-Dec-2020"

https://www.eternussolutions.com/2020/12/21/redux-thunk-redux-saga/#:~:text=Saga%20works%20like%20a%20separate,be%20minimized%20in%20redux%2Dthunk.

https://github.com/gilbarbara/react-redux-saga-boilerplate

https://betterprogramming.pub/react-redux-saga-boilerplate-d2ca0c891ccd

https://betterprogramming.pub/react-redux-saga-boilerplate-d2ca0c891ccd

**git@github.com:Marinashafiq/react-redux-boilerplate.git**

https://github.com/Marinashafiq/react-redux-boilerplate
