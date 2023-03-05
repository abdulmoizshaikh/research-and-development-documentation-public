# Retailo Deep Linking Mechanism

**How to open one app from another app using link**

**How-to**

1. Add the code in android/app/AndroidMenifest.xml like so within main activity:

```jsx showLineNumbers
<intent-filter>
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />
  <data android:scheme="https" android:host="retailo.co" />
</intent-filter>
```

2. Add the code to Navigation container file like so:

```jsx showLineNumbers
   const linking = {
   prefixes: ['https://retailo.co'],
   config: {
   screens: {
   [NAVIGATION_ROUTES_NAMES.PRODUCTS]: 'products/:categoryId/:subcategoryId',
   ...
   },
   },
   };
```

3. The nesting of screens inside navigators should be catered here the same way the navigation stack is structured. For example, to open sub category screen config object would look like this (provided that subcategory screen is stacked as “Main navigator => Bottom tab => home stack => sub category”):

```jsx showLineNumbers
   config: {
   screens : {
   [ROUTES.BOTTOM_NAV]: {
   screens: {
   [ROUTES.HOME_STACK]: {
   screens: {
   [ROUTES.SUBCATEGORY]: 'products/:categoryId/:subcategoryId',
   }
   }
   }
   }
   }
   },
```

4. Specify the screens with required params and query. Use ? for optional params like:
   `products/:categoryId/:subcategoryId?`
5. Now add the linking prop to NavigationContainer component from react-navigation

```jsx showLineNumbers
   <NavigationContainer
   linking={linking}
   {...props} >...
```

6.  The categoryId and subcategoryId are available in “route.params” objects of the navigation screens
7.  Execute in terminal
    `“npx uri-scheme open https://retailo.co/products/<categoryID>/<sub-categoryID> --android” to open in emulator`

    In my case its

8.  “npx uri-scheme open https://retailo.co/hisaab-app --android
9.  If you want to specify additional information like UTM source etc. it can be appended as query to the URL like https://retailo.co/products/:categoryId/:subcategoryId?utm_source=fb
10. The params and query params can be accessed from “route.params”
11. The back button behaviour would be needed to be catered like so:

```jsx showLineNumbers
import { useFocusEffect } from "@react-navigation/core";
import { BackHandler } from "react-native";

useFocusEffect(
  useCallback(() => {
    const onBackPress = () => {
      if (route.params?.categoryId) {
        navigation.navigate(ROUTES.CATEGORY);
        return true;
      }

      return false;
    };

    BackHandler.addEventListener("hardwareBackPress", onBackPress);

    return () =>
      BackHandler.removeEventListener("hardwareBackPress", onBackPress);
  }, [route])
);
```

12. Similarly handle back button on top bar
13. The useEffect to update the category ID and sub category ID to be active would look like:

```jsx showLineNumbers
useEffect(() => {
  const { categoryId } = route.params || {};

  if (categoryId) {
    reportCategoryOpened({
      categoryId,
      userId,
      locationId: userLocationId,
    });
    dispatch(getSubCategoryAction(categoryId));
  }
  if (subcategoryId) {
    showProductDetails(subcategoryId);
  }
}, []);
```

14. The useEffect has to be adjusted such that it fetches the products once the category ID and sub category ID are updated in Redux according to the deep link.

```jsx showLineNumbers
useEffect(() => {
  dispatch(fetchSubCategories());
  dispatch(fetchProductsByCategory());
}, [activeCategoryName]);
```
