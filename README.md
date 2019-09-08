# Test-Driven Development (TDD)
Resources for learning Test-Driven Development


___


## Links

[Wikipedia: Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development)


___


## Red Green Refactor TDD Methodology

:x: **Red** - Write a test. The test fails because you haven't written any code yet.

:white_check_mark: **Green** - Write code that passes your text (and all previous tests). Don't be clever, just write code so your tests pass.

:recycle: **Refactor** - There are many reason to refactor, such as efficency, code style, and readibility. Make sure your code still passes your tests as you refactor.


___


## Example
<sub>Based on [TypeofNaN's video on YouTube](https://www.youtube.com/watch?v=SbKPgaRZsxA)</sub>


### Install
```
npm i -D jest
```

**File Structure**
```
touch feature.js feature.test.js
```


___


### :x: Red
**feature.js**
```js
module.exports = null;
```

**feature.test.js**
```js
const add = require("./add");

describe("add", () => {
  it("should add two numbers", () => {
    expect(add(1, 2)).toBe(3);
  });
});
```

**Run**
```
npm jest
```

**Result**
> Fails


___


### :white_check_mark: Green
**feature.js**
```js
function add(a, b) {
  return a + b;
}

module.exports = add;
```

**Run**
```
npm jest
```

**Result**
> Passes


___


### :recycle: Refactor
**feature.js**
> Example: teams style is to use arrow functions and implicit returns.
```js
const add = (a, b) => a + b;

module.exports = add;
```

**Run**
```
npm jest
```

**Result**
> Passes


___


### :x: Red
**function.test.js**
```js
const add = require("./add");

describe("add", () => {
  it("should add two numbers", () => {
    expect(add(1, 2)).toBe(3);
  });
  it("should return a sole input", () => {
    expect(add(5)).toBe(5);
  });
  it("should add three numbers", () => {
    expect(add(1, 2, 3)).toBe(6);
  });
  it("should return 0 if no numbers are passed", () => {
    expect(add()).toBe(0);
  });
  it("should add any number of arguments", () => {
    expect(add(1, 2, 3, 4, 5, 6)).toBe(21);
  });
});
```

**Run**
```
npm jest
```

**Result**
> Fails


___


### :white_check_mark: Green
**feature.js**
```js
const add = (a, b, c) => {
  return a + b + c;
};

module.exports = add;
```

**Run**
```
npm jest
```

**Result**
> Fails

**feature.js**
```js
const add = (a, b, c) => {
  return a + (b || 0) + (c || 0);
};

module.exports = add;
```

**Run**
```
npm jest
```

**Result**
> Fails

**feature.js**
```js
const add = (a, b, c) => {
  return (a || 0) + (b || 0) + (c || 0);
};

module.exports = add;
```

**Run**
```
npm jest
```

**Result**
> Fails

**feature.js**
```js
const add = (...nums) => {
  return num.reduce((total, num) => total + num, 0);
};

module.exports = add;
```

**Run**
```
npm jest
```

**Result**
> Passes


___


### :recycle: Refactor
**feature.js**
```js
const add = (...nums) => num.reduce((total, num) => total + num, 0);

module.exports = add;
```

**Run**
```
npm jest
```

**Result**
> Passes
