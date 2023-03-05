# Deeplinking in React Native

---

## Retailo Deep Linking Mechanism

---

Reference file made by Khalil developer of retailo
https://docs.google.com/document/d/1UuUeGOWe57zvOEW0Kiz9WWMEdD4iyCvv/edit

### POC

JSON file for configure at server for redirection work when hit to this https://retailo.co/ url scheme :

// assetlinks.json (backend or devOps guys will add hisaab app namespace and package name for redirection work

```jsx showLineNumbers
[
  {
    relation: ["delegate_permission/common.handle_all_urls"],
    target: {
      namespace: "android_app",
      package_name: "com.app.retailerapp",
      sha256_cert_fingerprints: [
        "D4:82:0E:8F:C9:7E:DF:47:F3:6D:1C:09:3B:C3:AE:17:71:19:3C:6D:A9:D9:CD:52:CE:6F:12:94:D9:FC:62:0D",
      ],
    },
  },
];
```

https://retailo.co/.well-known/assetlinks.json

Package_name will be applicationId of android>app>build.gradle

### Declare website associations

A Digital Asset Links JSON file must be published on your website to indicate the Android apps that are associated with the website and verify the app's URL intents. The JSON file uses the following fields to identify associated apps:

- package_name: The application ID declared in the app's build.gradle file.
- sha256_cert_fingerprints: The SHA256 fingerprints of your app’s signing certificate. You can use the following command to generate the fingerprint via the Java keytool:
- keytool -list -v -keystore my-release-key.keystore
- This field supports multiple fingerprints, which can be used to support different versions of your app, such as debug and production builds.

The following example assetlinks.json file grants link-opening rights to a com.example Android app:

```jsx showLineNumbers
[
  {
    relation: ["delegate_permission/common.handle_all_urls"],
    target: {
      namespace: "android_app",
      package_name: "com.example",
      sha256_cert_fingerprints: [
        "14:6D:E9:83:C5:73:06:50:D8:EE:B9:95:2F:34:FC:64:16:A0:83:42:E6:1D:BE:A8:8A:04:96:B2:3F:CF:44:E5",
      ],
    },
  },
];
```

### Associating a website with multiple apps

A website can declare associations with multiple apps within the same assetlinks.json file. The following file listing shows an example of a statement file that declares association with two apps, separately, and resides at https://www.example.com/.well-known/assetlinks.json:

```jsx showLineNumbers
[
  {
    relation: ["delegate_permission/common.handle_all_urls"],
    target: {
      namespace: "android_app",
      package_name: "com.example.puppies.app",
      sha256_cert_fingerprints: [
        "14:6D:E9:83:C5:73:06:50:D8:EE:B9:95:2F:34:FC:64:16:A0:83:42:E6:1D:BE:A8:8A:04:96:B2:3F:CF:44:E5",
      ],
    },
  },
  {
    relation: ["delegate_permission/common.handle_all_urls"],
    target: {
      namespace: "android_app",
      package_name: "com.example.monkeys.app",
      sha256_cert_fingerprints: [
        "14:6D:E9:83:C5:73:06:50:D8:EE:B9:95:2F:34:FC:64:16:A0:83:42:E6:1D:BE:A8:8A:04:96:B2:3F:CF:44:E5",
      ],
    },
  },
];
```

Different apps may handle links for different resources under the same web host. For example, app1 may declare an intent filter for https://example.com/articles, and app2 may declare an intent filter for https://example.com/videos.

https://developer.android.com/training/app-links/verify-site-associations

```jsx showLineNumbers
// add this Manifest.xml
 <intent-filter>
           <action android:name="android.intent.action.VIEW" />
           <category android:name="android.intent.category.DEFAULT" />
           <category android:name="android.intent.category.BROWSABLE" />
           <!-- <data android:scheme="mychat" /> -->
           <data android:scheme="https" android:host="retailo.co" />
       </intent-filter>
```

E.g

//Manifest.xml

```jsx showLineNumbers
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
 package="com.app.retailohisaab">

   <uses-permission android:name="android.permission.INTERNET" />
   <uses-permission android:name="android.permission.READ_CONTACTS"/>
   <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
   <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
   <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
   <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
   <application
     android:name=".MainApplication"
     android:label="@string/app_name"
     android:icon="@mipmap/ic_launcher"
     android:roundIcon="@mipmap/ic_launcher_round"
     android:allowBackup="false"
     android:usesCleartextTraffic="true"
     android:theme="@style/AppTheme"
     android:supportsRtl="true">
     <activity
       android:name=".MainActivity"
       android:label="@string/app_name"
       android:screenOrientation="portrait"
       android:configChanges="keyboard|keyboardHidden|orientation|screenSize|uiMode"
       android:launchMode="singleTask"
       android:windowSoftInputMode="adjustPan"
       >
       <intent-filter>
           <action android:name="android.intent.action.MAIN" />
           <category android:name="android.intent.category.LAUNCHER" />
           <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
       </intent-filter>
       <intent-filter>
           <action android:name="android.intent.action.VIEW" />
           <category android:name="android.intent.category.DEFAULT" />
           <category android:name="android.intent.category.BROWSABLE" />
           <!-- <data android:scheme="mychat" /> -->
           <data android:scheme="https" android:host="retailo.co" />
       </intent-filter>
     </activity>
   </application>
</manifest>
```
