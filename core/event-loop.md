# Event Loop

## Task 1. What is the console.log's sequence?

```js
console.log('start');

setTimeout(() => {
  console.log('middle');
}, 0);

console.log('end');
```

## Task 2. What is the console.log's sequence?

```js
console.log('start');

setTimeout(() => {
  console.log('setTimeout');
}, 0);

Promise.resolve()
  .then(() => {
    console.log('promise1');
  })
  .then(() => {
    console.log('promise2');
  });

console.log('end');
```

## Event Loop Hint

```
   ----------                                 -------------------                         ---------------------
 | Call Stack |                             | Browser API         |                     | Render                |
 | (LIFO)     |                             | ------------------- |                     | --------------------- |
 | ---------- |                             | setTimeout  (macro) |                     | requestAnimationFrame |
 | ...        |                             | setInterval (macro) |                     | Style Recalculate     |
 | func 1     |                             | Promise     (micro) |                     | Layout                |
 | func 2     |                             | AJAX        (macro) |                     | Paint                 |
 | func 3     |                             | ...                 |                     | ...                   |
   ----------                                 -------------------                         ---------------------
       ↑                                               ↓                                            ↓
   ------------------------------------       -------------------------------------------------------
 | Event Loop                           |   |   -----------------------     -----------------------   |
 | ------------------------------------ | ← | | Microtasks Queue (FIFO) | | Macrotasks Queue (FIFO) | |
 |    ----------       ----------       |   |   -----------------------     -----------------------   |
 |  | Tasks      | → | Microtasks |     |     -------------------------------------------------------
 |    ----------       ----------       |
 |              ↑      ↓                |     -----------------------
 |             ----------               |   |   -------------------   |
 |           | Macrotasks |             | ← | | Render Queue (FIFO) | |
 |             ----------               |   |   -------------------   |
   ------------------------------------       -----------------------
                                                         ↑
                                               ---------------------
                                             | Render                |
                                             | --------------------- |
                                             | requestAnimationFrame |
                                             | Style Recalculate     |
                                             | Layout                |
                                             | Paint                 |
                                             | ...                   |
                                               ---------------------
```
