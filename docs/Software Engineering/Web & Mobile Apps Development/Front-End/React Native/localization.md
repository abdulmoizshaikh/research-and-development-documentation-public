# Localization

---

## Localization R&D for React native in hisaab project of Retailo .

List of top localization library in react native
https://simplelocalize.io/blog/posts/the-most-popular-react-localization-libraries/

Full list of localization libraries and tools on Github. Feel free to add your resources as pull requests or just create a new issue.
https://github.com/jpomykala/awesome-i18n

Recommended (because of large community and top libraries and highest stars on github and highest weekly downloads on npm and check no of dependencies (either this package is dependent on other package/library or not If this also dependent on other lib then its not recommended or less no of dependencies package would be recommended)

1-https://www.npmjs.com/package/react-i18next
https://react.i18next.com/getting-started
Demo : https://i18next.simplelocalize.io/
https://locize.com/

2-npm i i18n
https://www.npmjs.com/package/i18n

3-https://www.npmjs.com/package/react-intl this is formatJs is has 12.8k start
https://hybridheroes.de/blog/2021-03-25-formatjs/
https://formatjs.io/docs/tooling/cli/

4-https://www.npmjs.com/package/react-native-localize
https://github.com/zoontek/react-native-localize 1.7k stars
https://lokalise.com/blog/react-native-localization/

Not recommended (because of low stars on github repo and last publish is very old)

https://github.com/stefalda/react-localization
https://github.com/sealninja/react-i18nify
https://github.com/jpomykala/awesome-i18n

https://www.npmjs.com/package/react-native-i18n (2.0.15 • Public • Published 3 years ago)
This package is deprecated
This library is deprecated in favor of react-native-localize. You can use react-native-localize with I18n-js (but also with react-intl, react-i18next, etc. The choice is yours!)

https://github.com/evandhq/react-persian
https://github.com/Assembless/react-littera
https://github.com/bloodyowl/react-translate
https://github.com/vinissimus/next-translate (not using because i18n API for Next.js )1.3k stars
https://github.com/amsul/react-translated
https://github.com/CreateThrive/react-intl-hooks
https://github.com/ivanhofer/typesafe-i18n

Conclusion and finalized output before dig into implementation :

can use
https://www.npmjs.com/package/react-native-localize (recommended because this is only build for React native: A toolbox for your React Native app localization.)
https://www.npmjs.com/package/react-i18next
https://www.youtube.com/watch?v=osScyaGMVqo&ab_channel=locize
https://codesandbox.io/s/1zxox032q

not using
https://www.npmjs.com/package/react-intl (this is for web not mobile app)
https://www.npmjs.com/package/i18n ( because it is for node js : Lightweight simple translation module for node.js / express.js with dynamic json storage. Uses common \_\_('...') syntax in app and templates.)

Implementation
https://dev.to/ramonak/react-native-internationalization-with-i18next-568n

Error fixes:

i18next::pluralResolver: Your environment seems not to be Intl API compatible, use an Intl.PluralRules polyfill. Will fallback to the compatibilityJSON v3 format handling
to fix this add this line in i18n.config.ts

You may need to polyfill the Intl.PluralRules API, in case it is not available it will fallback to the i18next JSON format v3 plural handling.
To enforce old behaviour you can enable compatibilityJSON = 'v3' on i18next init call.
i18n.use(initReactI18next).init({
compatibilityJSON: 'v3',
})
References:

https://www.i18next.com/misc/migration-guide
https://github.com/i18next/i18next/issues/1671

https://dev.to/ramonak/react-native-internationalization-with-i18next-568n
https://giters.com/formatjs/formatjs/issues/2926
https://github.com/locize
https://www.i18next.com/principles/namespaces
https://codesandbox.io/s/react-i18next-forked-68yno?file=/src/app.js
https://www.freecodecamp.org/news/how-to-add-localization-to-your-react-app/
https://react-i18next-demo.mot01.repl.co/

---
