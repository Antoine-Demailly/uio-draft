# uio-draft

## Installation

```
npm install --save @uio/core
```

## Basic Usage

``` javascript
const Server = require('@uio/core');

new Server()
  .get('/', () => 'Hello World')
  .start();
```

## Component Usage

**components/Home.js**
``` javascript
module.exports = {
  name: 'Home',
  path: '/',

  get() {
    return 'Hello World';
  },
};
```

**index.js**
``` javascript
const Server = require('@uio/core');

new Server()
  .registerComponent('components/Home.js')
  .start();
```
