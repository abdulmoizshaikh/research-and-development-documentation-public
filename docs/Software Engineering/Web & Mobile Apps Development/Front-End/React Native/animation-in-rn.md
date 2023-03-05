# Animation in react native

---

## Animation work done for Hisaab project in retailo

how to move an element using animation in react native

https://www.w3schools.com/cssref/tryit.asp?filename=trycss3_keyframes

moving animation in react native
keyframes in react native styled components

https://reactnative.dev/docs/animations
https://stackoverflow.com/questions/55748343/animate-move-x-and-y-with-soft-move-react-native

https://reactnative.dev/docs/transforms
https://www.youtube.com/watch?v=1Q9efh7OcR8
https://codepen.io/A-G/pen/mdVoxPo
looping
https://snack.expo.dev/@git/github.com/wcandillon/can-it-be-done-in-react-native:bonuses/looping
https://github.com/wcandillon/can-it-be-done-in-react-native/tree/master/bonuses/looping
https://www.w3schools.com/cssref/css3_pr_transform.asp
https://www.w3schools.com/cssref/playdemo.asp?filename=playcss_margin-bottom
https://stackoverflow.com/questions/63052512/styled-components-keyframe-animation-not-applying-on-react-component
https://stackoverflow.com/questions/43022281/react-native-animation-event-style-property-is-not-supported
https://github.com/facebook/react-native/tree/main/packages/rn-tester/js/examples/AnimatedGratuitousApp
https://github.com/facebook/react-native/blob/main/packages/rn-tester/js/examples/NativeAnimation/NativeAnimationsExample.js
https://gist.github.com/loganpowell/2be75c1d0266d301fb1446ed14ebe7e6
https://snack.expo.dev/HJvm5WI5N

how to reset animation react native
move from to animation in react native
animate move x and y with soft move react native
https://stackoverflow.com/questions/55748343/animate-move-x-and-y-with-soft-move-react-native

keyframes in react native
https://www.w3schools.com/cssref/tryit.asp?filename=trycss3_keyframes
https://www.w3schools.com/cssref/css3_pr_animation-keyframes.asp
https://docs.swmansion.com/react-native-reanimated/docs/next/api/LayoutAnimations/keyframeAnimations/
http://reactnative.dev/docs/animations#responding-to-the-current-animation-value
https://docs.swmansion.com/react-native-reanimated/docs/fundamentals/animations
https://docs.swmansion.com/react-native-reanimated/docs/1.x.x/transitions/

recommended for infinite loop
animation in react native example

animated.timing loop
https://stackoverflow.com/questions/31578069/repeat-animation-with-new-animated-api
139

There's now loop animation available:

```jsx showLineNumbers
Animated.loop(
  Animated.sequence([
    Animated.timing(this.state.animatedStartValue, {
      toValue: 1,
      duration: 500,
      delay: 1000,
    }),
    Animated.timing(this.state.animatedStartValue, {
      toValue: 0,
      duration: 500,
    }),
  ]),
  {
    iterations: 4,
  }
).start();
```

animation in react native example
https://reactnativeexample.com/tag/animated/
https://medium.com/react-native-training/react-native-animations-using-the-animated-api-ebe8e0669fae
https://reactnative.dev/docs/animated

Implementation in hisaab app of retailo

Arrow up and down animation for click here purpose:

## ![image ](../../../../../assets/images/image125.png)

Code :

Arrow down svg icon

```jsx showLineNumbers
<svg
  width="24"
  height="48"
  viewBox="0 0 24 48"
  fill="none"
  xmlns="http://www.w3.org/2000/svg"
>
  <path
    d="M10.9393 47.0607C11.5251 47.6464 12.4749 47.6464 13.0607 47.0607L22.6066 37.5147C23.1924 36.9289 23.1924 35.9792 22.6066 35.3934C22.0208 34.8076 21.0711 34.8076 20.4853 35.3934L12 43.8787L3.51472 35.3934C2.92894 34.8076 1.97919 34.8076 1.3934 35.3934C0.807615 35.9792 0.807615 36.9289 1.3934 37.5147L10.9393 47.0607ZM10.5 3.31397e-08L10.5 46L13.5 46L13.5 -3.31397e-08L10.5 3.31397e-08Z"
    fill="#B4BAC0"
  />
</svg>
```

```jsx showLineNumbers
import AnimatedDownArrowSvg from './animation-down-arrow.svg';
 Export {  AnimatedDownArrowSvg};
```

Animation component:

```jsx showLineNumbers
import React, { useRef, useEffect } from "react";
import { Animated } from "react-native";

export const ArrowDownAnimation = (props) => {
  let animatedStartValue = useRef(new Animated.Value(0)).current;

  useEffect(() => {
    Animated.loop(
      Animated.sequence([
        Animated.timing(animatedStartValue, {
          toValue: -50,
          duration: 1000,
          useNativeDriver: true,
          delay: 50,
        }),
        Animated.timing(animatedStartValue, {
          toValue: 0,
          duration: 1000,
          useNativeDriver: true,
        }),
      ])
    ).start();
  }, [animatedStartValue]);

  return (
    <Animated.View
      style={{
        ...props.style,
        transform: [{ translateY: animatedStartValue }],
      }}
    >
      {props.children}
    </Animated.View>
  );
};
```

Usage of component:

```jsx showLineNumbers
const ListEmptyComponent = () => {
  return (
    <ListEmptyContainer>
      <ArrowDownAnimation style={homeStyles.downAnimationStyle}>
        <DownSvgIconWraper>
          <AnimatedDownArrowSvg />
        </DownSvgIconWraper>
        <DownSvgIconWraper>
          <AnimatedDownArrowSvg />
        </DownSvgIconWraper>
      </ArrowDownAnimation>
    </ListEmptyContainer>
  );
};

return <ListEmptyComponent />;

import styled, { css } from "styled-components/native";

export const ListEmptyContainer = styled.View`
  flex: 1;
  flex-direction: row;
  align-items: flex-end;
`;

export const DownSvgIconWraper = styled.View`
  width: 50%;
  align-items: center;
  justify-content: center;
  margin-bottom: 10;
`;
```
