# Utility functions in javascript

**Utils file in Hefazat Posapp**

```jsx showLineNumbers title="src/utils/handlers.ts"
import moment from "moment";
import numeral from "numeral";

export const getDuration = (date: Date) => {
  const years = moment().diff(date, "years");
  const days = moment().diff(date, "days");
  const months = moment().diff(date, "months");
  const totalYears = months / 12;
  console.log(totalYears, "totoal year");

  return {
    years,
    days,
    months,
    totalYears,
  };
};

export const is18Above = (date) => {
  const { years } = getDuration(date);
  if (years < 18) {
    return false;
  }
  return true;
};

export const isBelow70 = (date) => {
  const { totalYears } = getDuration(date);
  console.log(totalYears, "see years and days");
  if (totalYears > 70) {
    return false;
  }
  return true;
};
//export const numberWithCommas = (x) => x?.toString()?.replace(/\B(?=(\d{3})+(?!\d))/g, ',');
export const numberWithCommas = (x) => numeral(x).format("0,0");
export const numberWithCommasAndZero = (x) => numeral(x).format("0,0.00");

export const removeComma = (x) => {
  return +x.toString().replace(/\,/g, "");
};
```
