---
layout: page.njk
title: Check the Validity of a Date
---
# {{ title }}

How does one check a date?

##### JavaScript
```javascript
export const checkDate = (date) => {
  return date;
}
```

##### TypeScript
```typescript
export const checkDate = (date: Date | string) => {
  return date; // This should do something
}
```