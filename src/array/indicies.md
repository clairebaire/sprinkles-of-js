---
layout: page.njk
tags: featured
title: Get Indicies of Each Occurrence
description: You want to find where something is in an array. Maybe you want to see how many times it comes up.
eleventyNavigation:
  key: Get Indicies of Item
  parent: Arrays
---
# {{ title }}

Want to return the indicies of an item in an array?

<h2 class="h5">Explanation</h2>

This uses a combination of [`Array.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) and the `...` (spread) operator to figure out which index the value passed in is at, and returns a new array of the indicies.

The example below is not as succinct as it could be. However, to preserve readability, return statements were added. David Walsh [discusses readability vs "short code"](https://davidwalsh.name/javascript-short-code) in a bit outdated post from 2010.

<details open>
  <summary>JavaScript</summary>
  
```javascript
// Get the indicies of the item in question
const getIndicies = (array, value) => {
  return arr.reduce((accumulation, item, i) => {
    return (item === value ? [...accumulation, i] : accumulation), []
  });
}

// Usage
getIndicies([1, 2, 3, 1, 2, 3], 1); // [0,3]
getIndicies([1, 2, 3], 4); // []
```
</details>

<details>
  <summary>TypeScript</summary>
  
```typescript
// Get the indicies of the item in question
const getIndicies = (array: U[], value: U) => arr.reduce((accumulation, item, i) => (item === value ? [...accumulation, i] : accumulation), []);

// Usage
getIndicies([1, 2, 3, 1, 2, 3], 1); // [0,3]
getIndicies([1, 2, 3], 4); // []
```
</details>

<h2 class="h5">Compatibility</h2>

All evergreen browsers natively. Internet Explorer 11 supports it [via Babel](https://babeljs.io/repl#?browsers=ie%2011&build=&builtIns=false&spec=false&loose=false&code_lz=MYewdgzgLgBAlmAJgUwB4HkBmBBANrmAXhgAoBDAJwoBoYA3M3ASiID4ZKKA6C5RAV2DIS5YMFrJctOC0LsSkooWIMCAfhgBtLjrJjpAXRgAuDmKa1NBpgG4AUEA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=script&lineWrap=true&presets=env%2Cstage-3&prettier=false&targets=&version=7.12.14&externalPlugins=).