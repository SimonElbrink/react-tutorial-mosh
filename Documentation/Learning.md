# REACT WITH MOSH

[Source : Youtube ](https://www.youtube.com/watch?v=Ke90Tje7VS0&t=4592s)

## INTRODUTION

### INSTALLATION

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

### SETTING ATTRIBUTES

#### DYNAMIC PICTURE

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

#### STYLING

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

#### RENDERING CLASSES DYNAMICALLY

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

#### BINDING EVENT HANDLER

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

#### UPDATING THE STATE

You need to ´setState´ like this. Not like this `this.state.count++`.

```JavaScript
  handleIncrement = () => {
    this.setState({
      count: this.state.count + 1
    });
  };
```

#### PASSING EVENT ARGUMENTS

- Adding `doHandleIncrement` temporary, for illustration.
- Adding argument `product`.

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

## COMPOSING COMPONENTS

### PASSING DATA TO COMPONENTS

- First create `counters.jsx`.
- configure it like i did below.
- Make sure we render `<Counters/>` in `index.js`
- In `counter.jsx` configure like i did below. `props`, `value`, `handleIncrement`

`PROJECTNAME/component/counters.jsx`

```JavaScript
import React, { Component } from "react";
import Counter from "./counter";

class Counters extends Component {
  state = {
    counters: [
      { id: 1, value: 4 },
      { id: 2, value: 3 },
      { id: 3, value: 1 },
      { id: 4, value: 0 }
    ]
  };

  render() {
    return (
      <div>
        {this.state.counters.map(counter => (
          <Counter key={counter.id} value={counter.value} />
        ))}
      </div>
    );
  }
}
export default Counters;
```

`PROJECTNAME/component/counter.jsx`

```JavaScript
import React, { Component } from "react";

class Counter extends Component {
  state = {
    value: this.props.value
  };

  handleIncrement = () => {
    this.setState({
      value: this.state.value + 1
    });
  };

  render() {
    return (
      <React.Fragment>
        <span className={this.GetBadgeClasses()}>
        {this.formatCount()}
        </span>
        <button
          onClick={this.handleIncrement}
          className="btn btn-secondary btn-sm">
          Increment
        </button>
        <ul />
      </React.Fragment>
    );
  }

  GetBadgeClasses() {
    let classes = "badge m-2 badge-";
    classes += this.state.value === 0 ? "warning" : "primary";
    return classes;
  }

  formatCount() {
    const { value } = this.state;
    return value === 0 ? "Zero" : value;
  }
}
export default Counter;
```
