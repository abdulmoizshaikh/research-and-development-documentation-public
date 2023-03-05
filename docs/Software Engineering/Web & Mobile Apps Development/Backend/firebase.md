# Firebase

**OTP service in react native**

twilio otp react native (recommended) and easy approach
twilio otp sms send and verification in any mobile app using twilio api (to need to configure and android or IOS sdk)

https://www.twilio.com/blog/phone-verification-react-native
twilio otp react native android and ios

**firebase otp service for react native**

Phone Authentication (need to configure sdk for both android and ios and its complicated
firebase auth service for signin with user phone number by send otp to verify phone number

https://rnfirebase.io/auth/phone-auth

**twilio verify push replaces OTP verification**

https://drive.google.com/file/d/1Mu_l7VQG08vckZ9E0a-OpSKp1jZVDuJk/view

https://github.com/twilio/twilio-verify-for-react-native

**snapshop foreach is sync or async**

It’s sync operation

Unsubscribe events in firebase

// Or you can save a line of code by using an inline function
// and on()'s return value.
var onValueChange = ref.on('value', function(dataSnapshot) { ... });
// Sometime later...
ref.off('value', onValueChange);

https://firebase.google.com/docs/reference/node/firebase.database.Reference#off

**Pagination in firebase:**

Paginate data with query cursors

![plot](../../../../assets/images/image75.png)
![plot](../../../../assets/images/image6.png)

https://firebase.google.com/docs/firestore/query-data/query-cursors

**Upload image to firebase storage**

bucket for store image in firebase
The Firebase storage bucket can store the data using a file or folder. A reference instance can also take a string path value to upload an image to Firebase storage. This guide explains the steps to upload a selected image from a device to Firebase storage using the image picker helper functions.17-Oct-2020

```js showLineNumbers

  uploadImageToStorage(path, name) {
       this.setState({ isLoading: true });
       let reference = storage().ref(name); //here this path is firebase directory path where you want you upload this image and with image name as well like this firebaseurl/assets/image/image_name.jpg  (PS: filename coming from date picker object in react native)
       let task = reference.putFile(path); //and this path is your mobile directory path coming from image picker library object this tells firebase that you could update this image with same name from this path
       task.then(() => {
           console.log('Image uploaded to the bucket!');
           this.setState({ isLoading: false, status: 'Image uploaded successfully' });
       }).catch((e) => {
           status = 'Something went wrong';
           console.log('uploading image error => ', e);
           this.setState({ isLoading: false, status: 'Something went wrong' });
       });
   }

```

https://www.pluralsight.com/guides/upload-images-to-firebase-storage-in-react-native

**How to check if another specific app is installed in react native android**

> Use Firebase dynamic url

https://rnfirebase.io/dynamic-links/usage

https://medium.com/@c.nwaugha/how-to-implement-firebase-dynamic-links-in-react-native-888a554bd7fa

https://www.youtube.com/watch?v=YT841IVQvSc

https://www.youtube.com/watch?v=rvDq2WMU4mw&t=13s (deep linking be another way around)

how to integrate firebase dynamic url in react native

https://www.youtube.com/watch?v=zra2DCd0DnY

```js showLineNumbers

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

**How to check if user has installed specific app in react native**

OR

How can i check app installed in react native code

You can use firebase dynamic linking to achieve this

https://stackoverflow.com/questions/44005242/how-can-i-check-app-installed-in-react-native-code

https://www.npmjs.com/package/react-native-check-app-install

**What is the difference between cloud messaging and in-app messaging?**

Firebase Cloud Messaging (FCM) is a cross-platform messaging solution that lets you reliably send messages at no cost. Firebase In-App Messaging: Engage active app users with contextual messages. They both send messages to the app.15-Oct-2020

https://stackoverflow.com/questions/64369489/what-is-the-difference-between-firebase-cloud-messaging-and-firebase-in-app-mess

### Firebase :

**Firebase push notifications:**
https://stackoverflow.com/questions/51088909/how-to-stop-google-from-revoking-my-refresh-token

**how to generate authentication for firebase auth token for push notification**

https://stackoverflow.com/questions/50399170/what-bearer-token-should-i-be-using-for-firebase-cloud-messaging-testing

Create Custom Tokens
https://firebase.google.com/docs/auth/admin/create-custom-tokens#:~:text=Firebase%20gives%20you%20complete%20control,via%20the%20signInWithCustomToken()%20method.

**[Via REST](https://rnfirebase.io/messaging/notifications#via-rest)**

If you are unable to use a Firebase Admin SDK, Firebase also provides support for sending messages to devices via a POST request:

![image](./../../../../assets/images/image178.png)

https://rnfirebase.io/messaging/notifications#via-rest

**Firebase push notification: (android)**

https://firebase.google.com/docs/cloud-messaging/android/first-message

Go beyond notification messages
To go beyond notification messages and add other, more advanced behavior to your app, see:

**Receive messages in an Android app**

https://firebase.google.com/docs/cloud-messaging/android/receive

![image](./../../../../assets/images/image179.png)
https://firebase.google.com/docs/cloud-messaging/android/receive#edit-the-app-manifest

**Firebase short url\_**

![image](./../../../../assets/images/image180.png)
**Migrate from URL Shortener to Firebase Dynamic Links**

https://firebase.google.com/support/guides/url-shortener

**expiry time of bitly url**

Bitly links never expire. If you use a custom domain to shorten your links they will continue to work as long as your DNS is still pointing at Bitly and the custom domain is attached to a Bitly account. While you can hide links and their analytics from the analytics view, the data will remain in Bitly.20-Apr-2021
https://support.bitly.com/hc/en-us/articles/360002288272--Will-the-links-I-create-on-Bitly-ever-expire-#:~:text=Bitly%20links%20never%20expire.,data%20will%20remain%20in%20Bitly.

**Firebase dynamic URLS:**

https://firebase.google.com/docs/hosting/custom-domain

domain and path prefix are being released. please retry in one month

![image](./../../../../assets/images/image181.png)
https://stackoverflow.com/questions/57503507/dynamic-links-domain-and-path-prefix-are-being-released-please-retry-in-one-m

### Facebook:

Facebook also providing dynamic url support like firebase do
We need to configure facebook sdk react-native-fbsdk-next in our app and
When user click on any banner of our mobile app on facebook it will redirect user from facebook to our application if installed and if not installed on our mobile device (android & ios) then it will redirect to play store and app store based on its platform (Android OR IOS).

**Firebase Analytics:**
Analytics Error Codes

https://firebase.google.com/docs/analytics/errors
https://rnfirebase.io/analytics/usage

```jsx showLineNumbers
import analytics from '@react-native-firebase/analytics';

onPress={async () =>
  await analytics().logEvent('login', {
      id: 3745092,
      item: 'mens grey t-shirt',
      description: ['round neck', 'long sleeved'],
      size: 'L',
  })
}

Or

export const logEvent = async (eventName, payload) =>
   await analytics().logEvent(eventName, payload);

```

**Are firebase notifications free?**

Firebase Notifications is a free service that enables user notifications for Android and iOS devices. Through the Firebase console, you can send notifications quickly and easily across platforms with no server coding required.14-Jun-2016

Cloud Messaging (FCM) Free
Crashlytics Free
Dynamic Links Free
https://firebase.google.com/pricing/

react native app not working on http ur
react native app not working on http url
how to run react native app on http serverl
How to run react native app on http url (not secured ip address)
https://github.com/facebook/react-native/issues/24408

Try using this one. It worked for me.
Add the codes in your main AndroidManifest.xml :

```jsx showLineNumbers
<manifest xmlns:tools="http://schemas.android.com/tools">
  <uses-permission android:name="android.permission.INTERNET" />

  <application android:usesCleartextTraffic="true" tools:targetApi="28">
    ...
  </application>
</manifest>
```

@Zohaib Akhtar @Zubair Mehboob @Muhammad Moiz Just FYI, we will be using Sentry for app crashes
https://stackshare.io/stackups/crashlytics-vs-sentry

### FIREBASE:

**OTP service in react native**

twilio otp react native (recommended) and easy approach
twilio otp sms send and verification in any mobile app using twilio api (to need to configure and android or IOS sdk)
https://www.twilio.com/blog/phone-verification-react-native
twilio otp react native android and ios

**firebase otp service for react native**

**Phone Authentication (need to configure sdk for both android and ios and its complicated**

firebase auth service for signin with user phone number by send otp to verify phone number
https://rnfirebase.io/auth/phone-auth

**twilio verify push replaces OTP verification**

https://drive.google.com/file/d/1Mu_l7VQG08vckZ9E0a-OpSKp1jZVDuJk/view

https://github.com/twilio/twilio-verify-for-react-native

snapshot foreach is sync or async

It’s sync operation

Unsubscribe events in firebase

// Or you can save a line of code by using an inline function
// and on()'s return value.
var onValueChange = ref.on('value', function(dataSnapshot) { ... });
// Sometime later...
ref.off('value', onValueChange);
https://firebase.google.com/docs/reference/node/firebase.database.Reference#off

**Pagination in firebase:**

Paginate data with query cursors

https://firebase.google.com/docs/firestore/query-data/query-cursors

**Upload image to firebase storage**

bucket for store image in firebase
The Firebase storage bucket can store the data using a file or folder. A reference instance can also take a string path value to upload an image to Firebase storage. This guide explains the steps to upload a selected image from a device to Firebase storage using the image picker helper functions.17-Oct-2020

https://www.pluralsight.com/guides/upload-images-to-firebase-storage-in-react-native

```jsx showLineNumbers
  uploadImageToStorage(path, name) {
       this.setState({ isLoading: true });
       let reference = storage().ref(name); //here this path is firebase directory path where you want you upload this image and with image name as well like this firebaseurl/assets/image/image_name.jpg  (PS: filename coming from date picker object in react native)
       let task = reference.putFile(path); //and this path is your mobile directory path coming from image picker library object this tells firebase that you could update this image with same name from this path
       task.then(() => {
           console.log('Image uploaded to the bucket!');
           this.setState({ isLoading: false, status: 'Image uploaded successfully' });
       }).catch((e) => {
           status = 'Something went wrong';
           console.log('uploading image error => ', e);
           this.setState({ isLoading: false, status: 'Something went wrong' });
       });
   }
```

## firebase-android

**Do we restore firebase project after delete ?**

yes we can because when we delete a project it goes to firebase pending delete and after some time it become perminently delete we can restore before its perminently delete by firbase

"To recover your shut-down project:

Visit the [Resources pending deletion](https://console.developers.google.com/project?pendingDeletion=true&organizationId=416774220862) page.
Select the project you want to recover, and click Restore.
In the confirmation dialog, click Restore."

Enter your app's package name in the Android package name field.

**What's a package name, and where do you find it?**

**if select type wrong package name in firebase app you cant upload in the playstore but you can distribute the app through firebase app distribution**

`Make sure to enter the package name that your app is actually using. The package name value is case-sensitive, and it cannot be changed for this Firebase Android app after it's registered with your Firebase project.`

A package name uniquely identifies your app on the device and in the Google Play Store.

A package name is often referred to as an application ID.

Find your app's package name in your module (app-level) Gradle file, usually app/build.gradle (example package name: com.yourcompany.yourproject).

Be aware that the package name value is case-sensitive, and it cannot be changed for this Firebase Android app after it's registered with your Firebase project."

App nickname: An internal, convenience identifier that is only visible to you in the Firebase console

Debug signing certificate SHA-1: A SHA-1 hash is required by Firebase Authentication (when using Google Sign In or phone number sign in) and Firebase Dynamic Links.

**Firebase App distribution**

https://youtu.be/SiPOaV-5j9o
https://firebase.google.com/docs/app-distribution/android/distribute-console
https://www.youtube.com/watch?v=a9MCPDsr6W4&ab_channel=ProgrammingMakeSense

**download app from invited email**

https://firebase.google.com/docs/app-distribution/android/set-up-for-testing

**Firebase testlab**

for test accros multiple devices of difference resolution and models like multiple models of android you dont need to buy multiple devices to test on it

https://youtu.be/4_ZEEX1x17k
https://www.youtube.com/watch?v=o0aUuKztO4A&ab_channel=Firebase

**There was an error provisioning your app. Please try again. firebase OR Firebase: There was an unknown error while processing the request. Try again. [closed]**

The problem occurred because maybe the Firebase console was unable to sync or refresh, but signing out and back in worked for me. Try that.

https://stackoverflow.com/questions/43115090/firebase-there-was-an-unknown-error-while-processing-the-request-try-again
