# pragma syntax
## motivation
Adds hints to the runtime that the code can be parallelized or vectorized.

in the first case, it speeds up execution by using multi-threading without explicitly creating workers, while in the second case, it reduces the number of memory accesses.

> Other pragma instructions may be added in the future.

## high-level api
### cycles
```javascript
% pragma parallel
for (const i = 0; i < array.length; ++i) {
  array[i] = i ** 2;
}

% pragma parallel
array.map(e => e ** 2);
```

### short syntax

```javascript
for%parallel (const i = 0; i < array.length; ++i) {
  array[i] = i ** 2;
}

array.map%parallel(e => e ** 2);
```

## FAQ
### What if the calculation depends not only on the i-th element of the array, but also on the previous (calculated values)?
in this case, the execution is "vectorized": not one element of the array is read from memory to cache, but a certain sequence of elements, usually at least a "page" (depends on the processor and its cache).

Usually, at the beginning of each iteration of the cycle, the previous values are unloaded from the cache, new ones are loaded and work is already underway with them. If this code accesses the previous values, a new memory access is sent.

Vectorization "says" processor "unload previous values as rarely as possible."
