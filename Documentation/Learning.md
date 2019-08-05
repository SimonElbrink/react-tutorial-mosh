# REACT WITH MOSH

## INSTALLATION

In CMD in Project.

> `i` == `install`

```
npm i bootstrap@4.1.1
```

In `PROJECTNAME/src/index.js`

```JavaScript
import 'bootstrap/dist/css/bootstrap.css';
```

`PROJECTNAME/component/counter.jsx`

> The extention`.jsx` gives better code completion

You could export the component this way. But lets keep it to..

```JavaScript
import React, { Component } from "react";

export default class Counter extends Component {
  render() {
    return <h1> Hello world </h1>;
  }
}
```

..this

```JavaScript
import React, { Component } from "react";

class Counter extends Component {
  render() {
    return <h1> Hello world </h1>;
  }
}

export default Counter;
```

## SETTING ATTRIBUTES

### DYNAMIC PICTURE

`state`, `imageUrl`, `{this.state.imageUrl}`, `<React.Fragment>`

```JavaScript
class Counter extends Component {
  state = {
    count: 0,
    imageUrl: "https://picsum.photos/200"
  };
  render() {
    return (
      <React.Fragment>
        <img src={this.state.imageUrl} alt="" />

        <span>{this.formatCount()}</span>
        <button>Increment</button>
      </React.Fragment>
    );
  }

  formatCount() {
    const { count } = this.state;

    return count === 0 ? "Zero" : count;
  }
}
```

### STYLING

You could do it like this..

```JavaScript
 styles = {
    fontSize: 10,
    fontWeight: "bold"
  };
```

```JavaScript
<span style={this.styles}>
  {this.formatCount()}
</span>
```

..or this.

```JavaScript
<span style={{ fontSize: 10, fontWeight: "bold" }}>
  {this.formatCount()}
</span>
```

### RENDERING CLASSES DYNAMICALLY

```JavaScript
GetBadgeClasses() {
let classes = "badge m-2 badge-";
classes += this.state.count === 0 ? "warning" : "primary";
return classes;
}
```

```JavaScript
<span className={this.GetBadgeClasses()}>
  {this.formatCount()}
</span>

```
