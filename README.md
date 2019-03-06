# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)  WEB DEVELOPMENT IMMERSIVE

# Review

**Function Declaration:**

```js
function error(status) {
  console.error(status)
}
```

**Function Expression:**

```js
const error = function(status) {
  console.error(status)
}
```

**Anonymous Function:**

```js
function(status) {
  console.error(status)
}
```

# ES6

**ES6 Arrow Functions**

```js
const error = (status) => { 
  console.error(status)
}
```

You can go one step further:

```js
const error = status => console.error(status)
```

No parameters:

```js
const error = () => console.error('404')
```

Multiple Parameters:

```js
const error = (status, msg) => console.error(status, msg)
```

Multiple lines:

```js
const error = (status) => {
  let msg = 'Error: '
  console.error(msg, status)
}
```





