[Core](/core)

# Event Loop

## Task 1. What are the console.log's outputs?

```js
console.log('start');

setTimeout(() => {
  console.log('middle');
}, 0);

console.log('end');
```

## Task 2. What are the console.log's outputs?

```js
console.log('start');

setTimeout(() => {
  console.log('setTimeout 1');
}, 0);

Promise.resolve()
  .then(() => {
    console.log('promise1');
  })
  .then(() => {
    console.log('promise2');
  });
  
setTimeout(() => {
  console.log('setTimeout 2');
}, 0);

console.log('end');
```

## Task 3. What code fragment will stuck?

```js
const macrotask = () => {
  setTimeout(macrotask, 0);
};
```

```js
const microtask = () => {
  Promise.resolve().then(microtask);
};
```

## Event Loop Hint

```
   -----------------                          -------------------                       ---------------------
 | Call Stack (LIFO) |                      | Browser API         |                   | Render                |
 | ----------------- |                      | ------------------- |                   | --------------------- |
 | ...               |                      | setTimeout  (macro) |                   | requestAnimationFrame |
 | func 4            |                      | setInterval (macro) |                   | Style Recalculate     |
 | func 3            |                      | Promise     (micro) |                   | Layout                |
 | func 2            |                      | AJAX        (macro) |                   | Paint                 |
 | func 1            |                      | ...                 |                   | ...                   |
   -----------------                          -------------------                       ---------------------
       ↑                                               ↓                                          ↓
   ------------------------------------       ---------------------------------------------------------------
 | Event Loop                           |   |   ---------------------------     ---------------------------   |
 | ------------------------------------ | ← | | Microtasks Queue (FIFO) [1] | | Macrotasks Queue (FIFO) [2] | |
 |    ----------       ----------       |   |   ---------------------------     ---------------------------   |
 |  | Macrotasks | → | Microtasks |     |     ---------------------------------------------------------------
 |    ----------       ----------       |
 |              ↑      ↓                |     ---------------------------
 |             ----------               |   |   -----------------------   |
 |           |   Render   |             | ← | | Render Queue (FIFO) [3] | |
 |             ----------               |   |   -----------------------   |
   ------------------------------------       ---------------------------
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

## References

- https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/
- https://www.youtube.com/watch?v=8aGhZQkoFbQ
- https://javascript.info/event-loop
