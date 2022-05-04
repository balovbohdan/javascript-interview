[Core](/core)

# "var" vs "let" vs "const"

## Task 1. What are the console.log's outputs?

```js
// With "let"

for (let i = 0; i < 4; i++) {
  setTimeout(() => {
    console.log(i);
  }, 0);
}
```

```js
// With "var"

for (var i = 0; i < 4; i++) {
  setTimeout(() => {
    console.log(i);
  }, 0);
}
```

## References

- https://javascript.info/variables
- https://javascript.info/closure
- https://javascript.info/var
