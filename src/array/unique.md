---
layout: page.njk
tags: featured
title: Remove Duplicate Values in an Array
eleventyNavigation:
  key: Remove Duplicate Values
  parent: Arrays
---
# {{ title }}

Want to remove duplicates from your array?

<h2 class="h5">Explanation</h2>

This uses the JS `Set()` to filter duplicate values, since `Set` only works with unique values.

<details open>
  <summary>JavaScript</summary>
  
  ```javascript
// Function to find elements
const uniqueElements = arr => [...new Set(arr)];

// Usage
uniqueElements([1, 2, 2, 3, 4, 4, 5]); // [1, 2, 3, 4, 5]
```
</details>

<details>
  <summary>TypeScript</summary>
  
  ```typescript
// Function to find elements
const uniqueElements = arr: [] => [...new Set(arr)];

// Usage
uniqueElements([1, 2, 2, 3, 4, 4, 5]); // [1, 2, 3, 4, 5]
```
</details>

<h2 class="h5">Compatibility</h2>

All browsers, except Internet Explorer 11.