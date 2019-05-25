## motivation
Allows you to move code execution to a new, preferably unexpected, place.

> Excessive use of the operator can give the code the appearance of a famous Italian dish

## high-level api
### global scope

```javascript
code1();
goto foo;
code2();
foo:
code(3);

// сработает так
code1();
code3();
```

### working in class-scopes

```javascript
class Foo {
  bar() {
    code1()
    goto foo;
  }

  baz() {
    code2()
    foo:
    code3()
  }

// usage
const foo = new Foo();
foo.bar();

// work like that
code1();
code3(); 
// transfer in functions takes place with all the scop - so much more fun.
```

## FAQ
