---
layout: page.njk
tags: featured
title: Find the Union Between Two Arrays
description: Finding the common items between two arrays is very easy with this small function.
eleventyNavigation:
  key: Union
  parent: Arrays
---
# {{ title }}

Let's say you have two arrays. One has some items in it, and the other has another set of items. You want a _new_ array with the shared items in each.

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

[All browsers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set/Set#browser_compatibility), except Internet Explorer 11. Internet Explorer 11 does not support initializing a new `Set()` _with_ a value other than null, nor does it support the spread operator. However, via Babel, [it does](https://babeljs.io/repl#?browsers=ie%2011&build=&builtIns=false&spec=false&loose=false&code_lz=MYewdgzgLgBArmAluGBeGAKAhgGhgIwEo0A-GAQQCdKsBPAOgDNKQBbDMAUwHcYBlTlAwBtemNwwx9fAF1ChANxA&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=false&fileSize=false&timeTravel=false&sourceType=script&lineWrap=true&presets=env%2Cstage-2&prettier=false&targets=&version=7.12.14&externalPlugins=).