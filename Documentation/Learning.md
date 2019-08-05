# REACT WITH MOSH

## INSTALLATION

In CMD in Project.

> `i` == `install`

```
npm i bootstrap@4.1.1
```

In `PROJECTNAME/src/index.js`

```
import 'bootstrap/dist/css/bootstrap.css';
```

`PROJECTNAME/component/counter.jsx`

> The extention`.jsx` gives better code completion

You could export the component this way. But lets keep it to..

```Javascript
import React, { Component } from "react";

export default class Counter extends Component {
  render() {
    return <h1> Hello world </h1>;
  }
}
```

..this

```Javascript
import React, { Component } from "react";

class Counter extends Component {
  render() {
    return <h1> Hello world </h1>;
  }
}

export default Counter;
```
