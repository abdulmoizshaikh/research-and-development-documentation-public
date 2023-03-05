# React native boilerplate and best practices

- A React Native template for building solid applications 🐙, using JavaScript 💛 or Typescript 💙 (you choose).

  https://thecodingmachine.github.io/react-native-boilerplate/docs/AddALangTranslation
  https://github.com/thecodingmachine/react-native-boilerplate

**Usefull libraries list below**

https://redux-saga.react-boilerplate.com/private

**matrix for responsiveness**

```jsx showLineNumbers
import { Dimensions, PixelRatio, Platform } from "react-native";
import { isIphoneX } from "./isIPhoneX";
import Colors from "../colors";
let { height, width } = Dimensions.get("window");

height -= Platform.OS == "ios" ? (isIphoneX() ? 70 : 20) : 24;

const scale = height / 812;

const normalize = (size) => {
  const newSize = size * scale;
  // if (Platform.OS === 'ios') {
  return Math.round(PixelRatio.roundToNearestPixel(newSize));
  // } else {
  //return Math.round(PixelRatio.roundToNearestPixel(newSize)) -2
  // }
};

const VerticalSize = (size = 812) => (size / 812) * height;
const HorizontalSize = (size = 375) => (size / 375) * width;
const createShadow = (
  number = 5,
  opacity = 0.2,
  offset = { height: 5 },
  color = Colors.Shadow,
  backgroundColor = "white"
) => {
  return {
    elevation: number,
    shadowOffset: offset,
    shadowOpacity: opacity,
    shadowColor: color,
    backgroundColor,
  };
};
export default {
  Radius: VerticalSize(10),
  LightRadius: VerticalSize(6),
  ActiveOpacity: 0.5,
  customFontSize: normalize,
  FontRegular: normalize(16),
  FontExtraSmall: normalize(12),
  FontSmallest: normalize(10),
  FontSmall: normalize(14),
  FontMedium: normalize(18),
  FontLarge: normalize(22),
  VerticalSize,
  HorizontalSize,
  createShadow,
};
```
