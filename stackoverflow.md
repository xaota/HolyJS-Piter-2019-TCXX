# try stackoverflow

## motivation
many problems have already been solved by other developers, it allows to use other people's work.

## high-level api
There are several possibilities for using SO in your code.


### import code
```javascript
import {"exit vim" as exitVim} from "stackoverflow";
```

### dynamic import
```javascript
const exitVim = await import("exit vim", "stackoverflow")
```

### try catch extensions
```javascript
try {
  ... code
} catch (error) untill {
  const resolve = await import(error, "stackoverflow");
  resolve(error);
}
```
