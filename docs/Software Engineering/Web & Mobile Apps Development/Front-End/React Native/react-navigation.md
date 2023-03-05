# React Navigation

**React Navigation 5 Hide Drawer Item**

how to hide name from Drawer.Screen

Solution:

```jsx showLineNumbers
<Drawer.Screen
  name="Home"
  component={MainStackScreen}
  options={{
    drawerItemStyle: { height: 0 },
  }}
/>
```

https://stackoverflow.com/questions/60395508/react-navigation-5-hide-drawer-item

## stack navigation with tab navigation in react navigation

Combining Stack Navigation with Tab Navigation in React Native: React Navigation

https://medium.com/wesionary-team/combining-stack-navigator-with-tab-navigator-in-react-native-react-navigation-253656f45181

## How to Hide tab bar on specific screen in react navigation v6 react native:

Possible to hide tab navigator from screen in stack nested in tab?

#how to hide tab navigator in react native screen inside stack navigator
#React Navigation how to hide tabbar from inside stack navigation
#Hiding tab bar in specific screens
#how to hide tab navigator in react native screen

Solution: `Implemented in whatsapp status save app github repo`

```jsx showLineNumbers
//App.js
import React, { useEffect, useState } from "react";
import {
  createNavigationContainerRef,
  NavigationContainer,
} from "@react-navigation/native";
import { SafeAreaProvider } from "react-native-safe-area-context";
import Toast from "react-native-toast-message";
import { createDirectory } from "./src/config/utils/utils";
import { TabNavigator } from "./src/navigation";
import { StatusBar } from "react-native";
import { THEME_COLORS } from "./src/config/constants";

function App() {
  const ref = createNavigationContainerRef();
  const [routeName, setRouteName] = useState();

  useEffect(() => {
    createDirectory();
  }, []);

  return (
    <SafeAreaProvider>
      <StatusBar backgroundColor={THEME_COLORS.primary} />
      <NavigationContainer
        ref={ref}
        onReady={() => setRouteName(ref.getCurrentRoute().name)}
        onStateChange={async () => setRouteName(ref.getCurrentRoute().name)}
      >
        <TabNavigator routeName={routeName} />
        <Toast />
      </NavigationContainer>
    </SafeAreaProvider>
  );
}

export default App;
```

```jsx showLineNumbers
//Tabnavigator

import React from "react";
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
import { Saved } from "../../screens";
import Ionicons from "react-native-vector-icons/Ionicons";
import { CONSTANTS, THEME_COLORS } from "../../config/constants";
import styles from "./styles";
import { SettingsStackScreen, WhatsAppStackScreen } from "../stack";

const Tab = createBottomTabNavigator();
const { TAB_SCREENS } = CONSTANTS;

const TabNavigator = (props) => {
  const hide = props.routeName == "ImageViewer";

  return (
    <Tab.Navigator
      screenOptions={({ route }) => ({
        tabBarIcon: ({ focused, color, size }) => {
          let iconName;

          if (route.name === TAB_SCREENS.WHATSAPP) {
            iconName = focused ? "ios-logo-whatsapp" : "ios-logo-whatsapp";
          } else if (route.name === TAB_SCREENS.SAVED) {
            iconName = focused ? "ios-save" : "ios-save-outline";
          } else if (route.name === TAB_SCREENS.SETTINGS) {
            iconName = focused ? "ios-settings" : "ios-settings-outline";
          }

          // You can return any component that you like here!
          return <Ionicons name={iconName} size={size} color={color} />;
        },
        tabBarActiveTintColor: THEME_COLORS.primary,
        tabBarInactiveTintColor: THEME_COLORS.gray,
        headerShown: false,
      })}
    >
      <Tab.Screen
        name={TAB_SCREENS.WHATSAPP}
        component={WhatsAppStackScreen}
        options={{
          tabBarStyle: {
            display: hide ? "none" : "flex",
            ...styles.tabBarStyle,
          },
        }}
      />
      <Tab.Screen name={TAB_SCREENS.SAVED} component={Saved} />
      <Tab.Screen name={TAB_SCREENS.SETTINGS} component={SettingsStackScreen} />
    </Tab.Navigator>
  );
};

export default TabNavigator;
```

reference:

https://stackoverflow.com/questions/71607226/possible-to-hide-tab-navigator-from-screen-in-stack-nested-in-tab
