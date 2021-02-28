---
layout: page.njk
title: Build in UTC Assumption in Dates
eleventyExcludeFromCollections: true
eleventyNavigation:
  key: Account for UTC
  parent: Date
---
# {{ title }}

One really picky thing about JavaScript Dates is that they're in the _local timezone_ and not necessarily in UTC. Let's say you're given a date from a backend that has everything set in UTC, and then give it back to that backend in Central Standard Time, it will think it's UTC. This function is meant to fix that.

This fixes the issue where you set a date like so: `new Date('02/27/2021')` and you get `February 26, 2021 at 06:00:00 PM CST`

<h2 class="h5">Note</h2>

TC39 is working on [Temporal](https://tc39.es/proposal-temporal/docs/index.html) ([more about it at Igalia](https://blogs.igalia.com/compilers/2020/06/23/dates-and-times-in-javascript/)), a new Date and Time API for JavaScript. 

<details open>
<summary>JavaScript</summary>

```javascript
export const accountForUTC = (date, resetHours = false) => {
  const dateString = date.toUTCString();
  const offset = date.getTimezoneOffset() / 60;

  if (Number.isInteger(offset)) {
    const offsetString = offset < 10 && offset > 0 ? '0' + offset : offset;
    dateString = dateString + (offset < 0 ? '+' : '-') + offsetString + '00';
  }

  const newDate = new Date(dateString);

  if (resetHours) {
    newDate.setHours(0);
    newDate.setMinutes(0);
    newDate.setSeconds(0);
    newDate.setMilliseconds(0);
  }

  return newDate;
};

// Usage
new Date('02/27/2021') // => Date Sat Feb 27 2021 00:00:00 GMT-0600 (Central Standard Time)
accountForUTC(new Date('02/27/2021')) // => Date Sat Feb 27 2021 06:00:00 GMT-0600 (Central Standard Time)
```
</details>


<details>
<summary>TypeScript</summary>

```typescript
export const accountForUTC = (date: Date, resetHours: boolean = false): Date => {
  let dateString = date.toUTCString();
  const offset: number = date.getTimezoneOffset() / 60;

  if (Number.isInteger(offset)) {
    const offsetString = offset < 10 && offset > 0 ? '0' + offset : offset;
    dateString = dateString + (offset < 0 ? '+' : '-') + offsetString + '00';
  }

  const newDate = new Date(dateString);

  if (resetHours) {
    newDate.setHours(0);
    newDate.setMinutes(0);
    newDate.setSeconds(0);
    newDate.setMilliseconds(0);
  }

  return newDate;
};
```
</details>