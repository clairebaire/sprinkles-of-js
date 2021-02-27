---
layout: page.njk
title: Check the Validity of a Date
eleventyNavigation:
  key: Check Date Validity
  parent: Date
---
# {{ title }}

Dates are [notoriously weird](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date#the_ecmascript_epoch_and_timestamps) in JavaScript, but they don't necessarily have to be. This particular function deconstructs the date, verifies that it is _indeed_ a valid `Date`, and returns a boolean. The fun thing about JavaScript Dates is that `Invalid Date` is of type `Date`. But this isn't what we really want!

<h2 class="h5">Note</h2>

TC39 is working on [Temporal](https://tc39.es/proposal-temporal/docs/index.html) ([more about it at Igalia](https://blogs.igalia.com/compilers/2020/06/23/dates-and-times-in-javascript/)), a new Date and Time API for JavaScript. 

<!-- <details open>
<summary>JavaScript</summary>

```javascript
export const checkDate = (date) => {
  if (date instanceof Date) {
    date.get
  }
}
```
</details>


<details>
<summary>TypeScript</summary>

```typescript
export const checkDate = (date: Date | string): boolean => {
  return date; // This should do something
}
```
</details> -->