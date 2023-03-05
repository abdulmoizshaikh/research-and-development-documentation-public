# moment

How can I remove time from date with Moment.js?

how to extract only utc date from datetime in moment

Filter within a given date #419

```bash showLineNumbers
Sorry to jump in so late, but if you want to remove the time portion of a moment() rather than formatting it, then the code is:

.startOf('day')
Ref: http://momentjs.com/docs/#/manipulating/start-of/
```

demo

```jsx showLineNumbers
 const yesterdayUTCDate = moment()
      .subtract(1, 'days')
      .utc()
      .startOf('day')
      .format();
    const todayUTCDate = moment().utc().startOf('day').format();

    const contracts = await prisma.contract.findMany({
      where: {
        takafulId: 4,
        createdAt: {
          gte: yesterdayUTCDate, //fetching records made in last 24 hours
          lt: todayUTCDate,
        },
      },
```

https://stackoverflow.com/questions/15130735/how-can-i-remove-time-from-date-with-moment-js

# timer | count down | countdown custom made hook and integrated in sweetconnect baker app | background timer

Use Moment.js to convert Unix epoch time to human readable time
convert time into readable format moment
Countdown timer using Moment js
timer in moment js

Solution:

```jsx showLineNumbers
import React, { useEffect, useState } from "react";
import BackgroundTimer from "react-native-background-timer";

export function useTimer({ min, setMin, sec, setSec }) {
  const [showTimer, setTimer] = useState(0);
  const [counter, setCounter] = useState(0);
  const [buttonDisabled, setButtonDisabled] = useState(true);
  const [readableText, setReadableText] = useState("");

  useEffect(() => {
    if (min > 0) {
      setReadableText("mins");
    } else {
      setReadableText("sec");
    }
  }, [min, sec]);

  /**
   * Timer for pincode
   * @param duration
   */
  const startTimer = (duration) => {
    let timer = duration;
    let minutes;
    let seconds;
    // BackgroundTimer is used to emit event periodically when app is in the background
    const returnCount = BackgroundTimer.setInterval(function () {
      minutes = parseInt(timer / 60, 10);
      seconds = parseInt(timer % 60, 10);
      setMin(minutes);
      setSec(seconds);
      minutes = minutes < 10 ? minutes : minutes;
      seconds = seconds < 10 ? "0" + seconds : seconds;

      setTimer(minutes + ":" + seconds);
      if (--timer < 0) {
        setCounter(0);
        BackgroundTimer.clearInterval(returnCount);
      }
    }, 1000);
  };

  useEffect(() => {
    if (counter <= 0) {
      setButtonDisabled(false);
    } else {
      setButtonDisabled(true);
    }
  }, [counter]);

  return {
    showTimer,
    buttonDisabled,
    setCounter,
    startTimer,
    readableText,
    min,
    sec,
  };
}
```

**Usage :**

```jsx showLineNumbers
const { showTimer, startTimer, readableText } = useTimer({
  min,
  setMin,
  sec,
  setSec,
});

useState(() => {
  startTimer(duration);
  setMin(parseInt(duration / 60, 10));
  setSec(parseInt(duration % 60, 10));
}, []);

<Text font={"ubuntu"} fontFamily={"regular"} style={styles.timerText}>
  {showTimer}
</Text>;
```

https://momentjs.com/docs/#/durations/

## difference between 2 dates in seconds javascript

Implemented in sweet connect baker app

```jsx showLineNumbers
var a = new Date(item.createdAt);
var b = new Date();
var difference = Math.round((b - a) / 1000);
console.log("You waited: " + difference + " seconds");
```

### dob validation in javascript using moment

**DOB validation with moment js**

```jsx showLineNumbers
var age = moment().diff(newValue, "years");
```

```jsx showLineNumbers
// The birth date - be sure to parse in the same format you're expecting:
const dob = moment("11/2/1919", "D/M/YYYY");

// The constant number of years you don't want to exceed
const maxAge = 100;

//  Clone the dob (to not mutate it), increment by the years, and compare with day precision
const isValidDate = dob
  .clone()
  .add(maxAge, "years")
  .isSameOrBefore(moment(), "day");
```

https://stackoverflow.com/questions/54632337/dob-validation-with-moment-js

### Moment Js

**Moment get current date**

Sol

```jsx showLineNumbers
moment().format('YYYY-MM-DD');

Fixes timezone issue across the app
time={moment(date).local().format('hh:mmA')}
```

**Write a function 2 calculate days difference between 2 dates ?**

#Get hours difference between two dates in Moment Js
#How to calculate number of days between two dates
#difference between 2 dates using moment in day

Solution:

```jsx showLineNumbers
var start = moment("2022-03-10", "YYYY-MM-DD");
var end = moment().format("YYYY-MM-DD");
//Difference in number of days
const daysDifference = moment.duration(start.diff(end)).asDays();
console.log("daysDifference", daysDifference);
```

80

```jsx showLineNumbers
If you are using moment.js you can do it easily.

var start = moment("2018-03-10", "YYYY-MM-DD");
var end = moment("2018-03-15", "YYYY-MM-DD");

//Difference in number of days
moment.duration(start.diff(end)).asDays();

//Difference in number of weeks
moment.duration(start.diff(end)).asWeeks();



```

https://stackoverflow.com/questions/25150570/get-hours-difference-between-two-dates-in-moment-js  
https://stackoverflow.com/questions/9129928/how-to-calculate-number-of-days-between-two-dates

You can use this to practice
Demo :http://jsfiddle.net/6rjvpk18/5/

**Moment date time comparison:**

how to compare 2 dates using moment js

Moment js date time comparison
SOl:

```jsx showLineNumbers
const dateIsSame = moment("2014-03-24T01:15:00.000Z").isSame(
  moment("2014-03-24T01:14:00.000Z")
);
```

https://stackoverflow.com/questions/22600856/moment-js-date-time-comparison

console.log(moment("2015-01-16T16:00:00").format("hh:mm a"));

https://jsfiddle.net/Bjolja/6mn32xhu/
