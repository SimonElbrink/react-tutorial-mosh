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

### BINDING EVENT HANDLER

To access `this` in my function below. You need..

```JavaScript
  handleIncrement() {
    console.log("Increment clicked" + this);
  };
```

to make a constructor. Or..

```JavaScript
  constructor () {
    super();
    this.handleIncrement = this.handleIncrement.bind(this);
  }
```

..just do it like this with the arrow function without constructor.

```JavaScript
  handleIncrement = () => {
    console.log("Increment clicked" + this);
  };
```

### UPDATING THE STATE

You need to ´setState´ like this. Not like this `this.state.count++`.

```JavaScript
  handleIncrement = () => {
    this.setState({
      count: this.state.count + 1
    });
  };
```

### PASSING EVENT ARGUMENTS

Adding `doHandleIncrement` temporary, for illustration.  
Adding argument `product`.

```JavaScript
  state = {
    count: 0
  };

 handleIncrement = product => {
    console.log(product);
    this.setState({
      count: this.state.count + 1
    });
  };

  doHandleIncrement = () => {
    this.handleIncrement({ id: 1 });
  };

 render() {
   return (
      <React.Fragment>
        //...some irrelevant code
        <button
          onClick={this.doHandleIncrement}
          className="btn btn-secondary btn-sm">
          Increment
        </button>
        //...more irrelevant code
      </React.Fragment>
    );
```

You could do it more clean, like this.  
Remove `doHandleIncrement` and make a inline function instead.

> sources says that this is not efficient code. For now we leave it there.

```JavaScript
  state = {
    count: 0,
    tags: ["tag1", "tag2", "tag3"]
  };

 handleIncrement = product => {
    console.log(product);
    this.setState({
      count: this.state.count + 1
    });
  };

 render() {
   return (
     <React.Fragment>
        //...some irrelevant code
        <button
          onClick={
            () => this.handleIncrement(product)}
          className="btn btn-secondary btn-sm">
          Increment
        </button>
        //...more irrelevant code
      </React.Fragment>
    );
```
