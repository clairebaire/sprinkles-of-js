---
layout: page.njk
title: Build in UTC Assumption in Dates
eleventyExcludeFromCollections: true
eleventyNavigation:
  key: Account for UTC
  parent: Date
---
# {{ title }}

One really picky thing about JavaScript Dates is that they're in the _local timezone_ and not necessarily in UTC. 

This fixes the issue where you set a date like so: `new Date('02/27/2021')` and you get `February 26, 2021 at 06:00:00 PM CST`. [Eleventy users know this all too well](https://www.11ty.dev/docs/dates/#dates-off-by-one-day).

<h2 class="h5">When to Use</h2>

Let's say you have a web component being fed a date that is assumed to be in UTC. Since web components assume any attribute is a string, it will give the offset of your local timezone when you use the `new Date()` constructor. You can then work with that date and whatnot, but what happens when you send it back to the server? Whatever date is sent back is in your local timezone.

This adds the offset in hours to your date so that it displays correctly in a date input, etc.

<h2 class="h5">Special Consideration</h2>

This is not the same use case as using `Date.UTC(2021, 01, 27)` (which is 02/27/2021 - months are 0-indexed). `Date.UTC()` returns an epoch.

It is technically feasible to do this instead:

```javascript
new Date(Date.UTC(2021, 01, 27))
```

However, I'd argue this is less readable / more mental load to understand exactly how this works. Thinking of it another way:
- Dissect the date into its parts (month, day, year)
- Subtract 1 from the month
- Convert to UTC epoch
- Convert to new Date

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
    dateString = `${dateString}${(offset < 0 ? '+' : '-')}${offsetString}00`;
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
    dateString = `${dateString}${(offset < 0 ? '+' : '-')}${offsetString}00`;
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