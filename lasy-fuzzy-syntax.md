## motivation
Describes a set of instructions that will be executed only when the external code needs the result of executing these instructions.

## examples from other languages
LINQ in .NET

## high-level api
```javascript
const result = lasy array.map(...).filter(...).reduce(...);
// instructions will not be calculated at all
...

console.log(result[0]) // result will be calculated just now.
```

### Принудительное исполнение
```javascript
const result = lasy array.map(...).filter(...);
// result will not be calculated at all
...
(fuzzy result).reduce(...);
// calculate the value at the time of calling fuzzy, and then add a new call to the calculation queue

console.log(result[0]); // final calculation result
```
