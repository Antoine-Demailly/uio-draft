# uio-draft

## Installation

```
npm install --save @uio/core
```

## Shortest Usage

### First example 

``` javascript
const Server = require('@uio/core');

new Server()
  .get('/', () => 'Hello World')
  .start();
```

### Second example 

``` javascript
const Server = require('@uio/core');

new Server()
  .get('/alive', () => '')
  .start();
```

**Note:** by default, an empty response (`''`) will automatically set the HTTP Status Code at **204 No Content**.

## Component Usage

### First example

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

### Second example

``` javascript
module.exports = {
  name: 'Users',
  path: '/users/',

  body: {
    username: {
      type: String,
      minLength: 5,
      maxLength: 30,
    },
    email: {
      type: String,
      format: 'email',
    },
    password: {
      type: String,
      format: 'password/v1',
    },
    passwordCheck: {
      sameAs: 'password',
    },
  },
  
  async get() {    
    const users = await this.$db.User.findAll();

    return users;
  },
  
  async post() {
    // at this point, the body has already been checked by @uio/validator
    const user = await this.$db.User.create(this.body);
 
    return user;
  },
};
```
