---
layout: page.njk
title: Check the Validity of a Date
eleventyExcludeFromCollections: true
eleventyNavigation:
  key: Check Date Validity
  parent: Date
---
# {{ title }}

Dates are [notoriously weird](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_ecmascript_epoch_and_timestamps) in JavaScript, but they don't necessarily have to be. This particular function deconstructs the date, verifies that it is _indeed_ a valid `Date`, and returns a boolean. The fun thing about JavaScript Dates is that `Invalid Date` is of type `Date`. But this isn't what we really want!

<h2 class="h5">Special Considerations</h2>

Notice in the code there are a few things worth noting:
- `Number.parseInt()` has two parameters. `parseInt()` is relative, meaning it's not always in Base 10. [MDN explains this well](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt#description).
- We allow two different types of inputs here: `string` and `Date`.
  - **But**, as stated above, `Invalid Date` is valid when the input is of type Date. Thus, we want to return false if that is the case.
  - In the case of the string, we literally dissect it by its delimiter (in this case, a "/") and attempt to set the date manually, and verify that is is indeed correctly a date.

<h2 class="h5">Note</h2>

TC39 is working on [Temporal](https://tc39.es/proposal-temporal/docs/index.html) ([more about it at Igalia](https://blogs.igalia.com/compilers/2020/06/23/dates-and-times-in-javascript/)), a new Date and Time API for JavaScript. 

<details open>
<summary>JavaScript</summary>

```javascript
// This expects a date in the format: MM/DD/YYYY
// To switch it to DD/MM/YYYY, change the array accessors in if (dateChunks)
export const checkValidityOfDate = (dateToCheck) => {
  if (typeof dateToCheck === 'string') {
    const date = new Date(dateToCheck);
    const temp = dateToCheck.split('/');
    const dateChunks = [];

    temp.forEach((chunk, i) => (dateChunks[i] = Number.parseInt(chunk, 10)));
    if (dateChunks[0] !== 0) {
      dateChunks[0] = dateChunks[0] - 1;
    }

    if (date.getFullYear() < 1000) {
      return false;
    }

    return date.getMonth() === dateChunks[0] && date.getFullYear() === dateChunks[2] && date.getDate() === dateChunks[1];
  } else {
    return !isNaN(Number(dateToCheck));
  }
};
```
</details>


<details>
<summary>TypeScript</summary>

```typescript
// This expects a date in the format: MM/DD/YYYY
// To switch it to DD/MM/YYYY, change the array accessors in if (dateChunks)
export const checkValidityOfDate = (dateToCheck: string | Date) => {
  if (typeof dateToCheck === 'string') {
    const date = new Date(dateToCheck);
    const temp = dateToCheck.split('/');
    const dateChunks: number[] = [];

    temp.forEach((chunk, i) => (dateChunks[i] = Number.parseInt(chunk, 10)));
    if (dateChunks[0] !== 0) {
      dateChunks[0] = dateChunks[0] - 1;
    }

    if (date.getFullYear() < 1000) {
      return false;
    }

    return date.getMonth() === dateChunks[0] && date.getFullYear() === dateChunks[2] && date.getDate() === dateChunks[1];
  } else {
    return !isNaN(Number(dateToCheck));
  }
};
```
</details>