# sandbox keyword
## motivation
syntax sugar for running the sandboxed code - causes no side effects during execution.

## high-level api
### Example
```javascript
const result = sandbox './file.js';
```

### equivalent for this:
```javascript
function sandbox(file) {
  return new Promise((resolve, reject) => {
      const worker = new Worker(file);
      worker.onMessage(resolve);
  });
}

const result = await sandbox('./file.js');
```

> Of course, sandboxing of functions and strings is also supported, by analogy with `eval`.

## FAQ
### If an error occurs during execution?
`try / catch` никто не отменял.

### Is it possible to set restrictions on the executable code? from memory, time of execution??
yes
```javascript
await sandbox ["file.js", {memory, timeout}
```

### Is it possible to pass parameters to executable code?
of course
```javascript
await sandbox ["file.js", {arguments}];
```

### whether platform-specific permissions and restrictions?
it is possible. for example, for node.js, you can add file system access restrictions.
```javascript
await sandbox  ["file.js", {fs: "readonly"}];
```

### How about running interactive code in this way?
of course! You can use the constructor generator sandbox!
```javascript
const cli = sandbox* "file.js";
const prompt1 = yield cli;
cli.next({...});
const prompt2 = yield cli;
cli.next({...});
```

> although for this code the construction would not hurt `top level yield` :)
