---
layout: page.njk
tags: featured
title: Find the Union Between Two Arrays
eleventyNavigation:
  key: Union
  parent: Arrays
---
# {{ title }}

Let's say you have two arrays. One has some items in it, and the other has another set of items. You want a _new_ array with the unique items in each.

<h2 class="h5">Explanation</h2>

This technique uses [`Set()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/Set) to filter out the items that are not unique, as a `Set` can only have unique values. It then converts that back to an `Array` utilizing `Array.from()`

<details open>
<summary>JavaScript</summary>

  ```javascript
  // Find the Union
  const union = (a, b) => Array.from(new Set([...a, ...b]));

  // Usage
  union([1, 2, 3], [4, 3, 2]); // = [1, 2, 3]
  ```
</details>

<details>
<summary>TypeScript</summary>

```typescript
// Find the Union
const union = (a: unknown[], b: unknown[]) => Array.from(new Set([...a, ...b]));

// Usage
union([1, 2, 3], [4, 3, 2]); // = [1, 2, 3]
```
</details>

<h2 class="h5">Compatibility</h2>

[All browsers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/Set#browser_compatibility), except Internet Explorer 11.