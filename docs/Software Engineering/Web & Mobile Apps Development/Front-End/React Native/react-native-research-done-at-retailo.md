# react native research done when working with retailo

react-native get country code from GPS coordinates
how to get country code from lat long react native
https://stackoverflow.com/questions/55470679/react-native-get-country-code-from-gps-coordinates

https://github.com/devfd/react-native-geocoder
Country name for GPS coordinates
https://stackoverflow.com/questions/3633504/country-name-for-gps-coordinates/3633619#3633619
http://jsfiddle.net/hippietrail/nrS9Q/1/

we can add some delay in reloading screen and check if app crashing or not.
https://www.npmjs.com/package/react-native-geocoder

https://github.com/zoontek/react-native-localize/issues/145
https://github.com/zoontek/react-native-localize/issues/158

R&D of device info library

how to get the timezone of device in to react native || how to get timezone in react native
Solution:
you can get by using this library: react-native-localize
import \* as RNLocalize from 'react-native-localize';
console.log('RNLocalize.getTimeZone())', RNLocalize.getTimeZone());

https://stackoverflow.com/questions/37552973/get-the-time-zone-with-react-native

cannot read property getCountryCode of null in react native
ON android 11 its not working when I unintsll react antive country picker lib
but on android 8 workign

now testing with lib on both devices
yes by using this libaray issues fixed
https://www.npmjs.com/package/react-native-device-country
https://www.npmjs.com/package/react-native-currency-picker

npm run variant release

try make build using android studio
try to change SHA on mac

ref
https://stackoverflow.com/questions/52507156/your-android-app-bundle-is-signed-with-the-wrong-key-ensure-that-your-app-bundl
https://stackoverflow.com/questions/54314838/googleplay-wrong-signing-key-for-app-bundle
https://reactnative.dev/docs/signed-apk-android
https://support.google.com/googleplay/android-developer/answer/9842756?visit_id=637867268105747073-1920739985&rd=1#reset
https://pilloxa.gitlab.io/posts/safer-passwords-in-gradle/
https://docs.google.com/document/d/1pcSbbXKXvrsMSpQlfegpFXbdXVVpt_FbEW_uc4chkyc/edit
how to make build in android studio
https://www.youtube.com/watch?v=mbRbzbGTNfk&ab_channel=JustChill

---

create dummy app using react native webview and apply responsiveness on that

Problem statement:
we need to use that feature

Proposed solutions:

Benefits of using Webview

- its cross platform (Android/IOS)
- it can update OTA (over the air)
- It can be completely responsive
  We can achieve this feature using WebView

references:
https://medium.com/spritle-software/embed-responsive-webpage-on-a-react-native-app-8cd418714bde
https://github.com/react-native-webview/react-native-webview/blob/a36394f598944c1ffe288f739b7441830249dc1e/docs/Guide.md#basic-url-source
https://github.com/react-native-webview/react-native-webview/blob/a36394f598944c1ffe288f739b7441830249dc1e/docs/Guide.md#communicating-between-js-and-native

9 May 2022
https://github.com/react-native-webview/react-native-webview/issues/73

12 May

do we need to pass token in webview call
If yes then I have to do R&D for data binding in webview as well either its possible or not.
I have to find workaround to solve this problem

set token in localstorage and get and use token in website

all things covered in this lecture
https://www.youtube.com/watch?v=0lN0RnOWTlI

how to pass props in react native webview
How to pass value from react native state to webview - Stack ...
https://stackoverflow.com/questions/62902660/how-to-pass-value-from-react-native-state-to-webview

we can share data using query params

call with zohaib
update query aprams 2 solution in sheet
1- encoded one
2- session id and device token one

R&D and POC for team feedback regarding webview in react native
comunication and data binding

Push notification
create deeplink and pass param in it
and open deeplink from webapp and react native screen will open
will create separete component for deepling from webview

deep linking
https://youtu.be/H5NCFXewLlk?t=216
https://youtu.be/s8YaclRknYw?t=1
disable zoom effect in react native webview work

pull to refresh
https://apeatling.github.io/web-pull-to-refresh/
https://bestofreactjs.com/repo/bryaneaton13-react-pull-to-refresh
https://thmsgbrt.github.io/react-simple-pull-to-refresh/
https://github.com/cuongdevjs/pull-to-refresh-react
https://apeatling.com/articles/javascript-pull-to-refresh-web/
https://github.com/apeatling/web-pull-to-refresh
https://www.npmjs.com/package/react-pull-to-refresh
https://github.com/react-native-webview/react-native-webview/issues/103
https://github.com/facebook/react-native/issues/7870#issuecomment-292767858
pull or refresh in react website

not recommended
https://www.npmjs.com/package/react-simple-pull-to-refresh

pull-to-refresh-react
https://github.com/cuongdevjs/pull-to-refresh-react
https://www.npmjs.com/package/pull-to-refresh-react

research on query params parsing
https://www.educative.io/edpresso/how-to-communicate-with-data-between-webviews-in-react-native
https://stackoverflow.com/questions/55764162/how-can-i-send-a-data-to-webview-by-clicking-on-react-native-button

Demo
https://6284ac524c2cab4ef1c7ec55--vocal-piroshki-e861c4.netlify.app/

solution to intellisense not working in tsx class component in react
“react class component state typescript” Code Answer’s

sol

interface IProps {}

interface IState {
isLoading?: boolean;
canGoBack?: boolean;
canGoForward?: boolean;
}

class WebViewScreen extends React.Component<IProps, IState> {

https://www.codegrepper.com/code-examples/typescript/react+class+component+state+typescript

navigation can be challenging

moiz-personal-access-token-api-scope gitlab
glpat-nyRPUrbw3evBts4K8wxx

glpat-nyRPUrbw3evBts4K8wxx

create .npmrc file and replace GL_NPM_TOKEN with your generated token
@development-team20:registry=https://gitlab.com/api/v4/packages/npm/
//gitlab.com/api/v4/packages/npm/:\_authToken=${GL_NPM_TOKEN}

eslint --fix

lint command chalani hy
test ki command chalni hy before push
we have to create config file

gazanfar bhai told that he will be creating config file for linting issues
meanwhile we have to manually parsed the file

"lint-fix": "eslint --fix src --ext .ts,.tsx",
https://github.com/eslint/eslint/issues/7456

how to convert object into array using lodash
solution:
transform object to array with lodash
A modern native solution if anyone is interested:
const arr = Object.keys(obj).map(key => ({ key, value: obj[key] }));

backlog after EID
POC for audio play feature

78:24 error Do not nest ternary expressions no-nested-ternary
https://stackoverflow.com/questions/46272156/how-can-i-avoid-nested-ternary-expressions-in-my-code

find library that will open calender by default

https://www.npmjs.com/package/react-native-calendar-range-picker
https://www.npmjs.com/package/react-native-range-datepicker

https://www.npmjs.com/package/react-native-drag-view
https://www.npmjs.com/package/react-native-android-notification-listener
https://stackoverflow.com/questions/45854450/detect-swipe-left-in-react-native

$ npm depute (not as such worked best solution that works is make library verion same on both apps)
https://docs.npmjs.com/cli/v8/commands/npm-dedupe
