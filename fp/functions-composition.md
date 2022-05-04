[Functional Programming](.)

# Functions Composition

## Task 1. Develop a `compose` function

Let's imagine that we have the following pure functions:

```js
const increment = (n) => n + 1;
const double = (n) => n * 2;
const format = (n) => `Number ${n}`;
```

We can combine these functions. One of the possible combinations:

```js
const input = 2;
const output = format(double(increment(input)));

// `Number ${(input + 1) * 2}` -> "Number 6"
```

The task is to create a `compose` function. Its usage should look as follows:

```js
const input = 2;
const formatNumber = compose(format, double, increment);
const output = formatNumber(input); // -> "Number 6"
```
