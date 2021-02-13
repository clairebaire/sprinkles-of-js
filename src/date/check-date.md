---
layout: page.njk
title: Hello
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