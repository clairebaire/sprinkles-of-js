---
layout: page.njk
tags: dom
title: Manipulate DOM Elements
eleventyNavigation:
  key: Manipulate Elements
  parent: DOM
---
# {{ title }}

In modern browsers, you can iterate over the result of `document.querySelectorAll()` (which is a `NodeList`) with a familiar Array method, `forEach()`. This is a _static_ version of the elements though - so this is good for a "point in time" usage of the DOM elements - say you want to note which elements were on the page at one time for example.

<h2 class="h5">Explanation</h2>

This uses a combination of [`Array.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) and the `...` (spread) operator to figure out which index the value passed in is at, and returns a new array of the indicies.

<details open>
  <summary>JavaScript</summary>
  
```javascript
// Find All Indicies
const indexOfAll = (arr, val) => arr.reduce((acc, el, i) => (el === val ? [...acc, i] : acc), []);

// Usage
indexOfAll([1, 2, 3, 1, 2, 3], 1); // [0,3]
indexOfAll([1, 2, 3], 4); // []
```
</details>

<details>
  <summary>TypeScript</summary>
  
```typescript
// Find All Indicies
const indexOfAll = (arr, val) => arr.reduce((acc, el, i) => (el === val ? [...acc, i] : acc), []);

// Usage
indexOfAll([1, 2, 3, 1, 2, 3], 1); // [0,3]
indexOfAll([1, 2, 3], 4); // []
```
</details>

<h2 class="h5">Compatibility</h2>

All evergreen browsers natively. Internet Explorer 11 supports it [via Babel](https://babeljs.io/repl#?browsers=ie%2011&build=&builtIns=false&spec=false&loose=false&code_lz=MYewdgzgLgBAlmAJgUwB4HkBmBBANrmAXhgAoBDAJwoBoYA3M3ASiID4ZKKA6C5RAV2DIS5YMFrJctOC0LsSkooWIMCAfhgBtLjrJjpAXRgAuDmKa1NBpgG4AUEA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=script&lineWrap=true&presets=env%2Cstage-3&prettier=false&targets=&version=7.12.14&externalPlugins=).