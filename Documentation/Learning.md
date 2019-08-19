# REACT WITH MOSH

Author: [Simon Elbrink](https://github.com/SimonElbrink)

Source : [Youtube: Programming with Mosh
](https://www.youtube.com/watch?v=Ke90Tje7VS0&t=4592s)

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

### PASSING CHILDREN

`PROJECTNAME/component/counter.jsx`

```JavaScript
  render() {
    console.log(this.props);

    return (
      <React.Fragment>
        {this.props.children}
        ...some irrelevent code
      </React.Fragment>
    );
  }
```

Add `<h4>` between `<Counter>` tags like this.

`PROJECTNAME/component/counters.jsx`

```JavaScript
          <Counter key={counter.id} value={counter.value}>
            <h4>Counter #{counter.id}</h4>
          </Counter>
```

**You could also do it like this:**

> There are use cases for them both.

change the props we wrote in `counter` from:

```
{this.props.children}
```

To:

```
<h4>{this.props.id}</h4>

```

In `counters` add `id` in `<Counter>` like this:

```JavaScript
          <Counter key={counter.id} value={counter.value} id={counter.id}>
            <h4>Counter #{counter.id}</h4>
          </Counter>
```

### PROPS VS STATE

- Both `state` and `props` are handled by React.

- `state` local/private to the component.

  > React is watching if the state is changed, if so it will update the DOM.

- `Props` get sent between components.
  > props are **Readonly**

Sending Props to `<Counter>`

> In this case `counter={counter}` sends all.

> `value={counter.value}` would be an example of sending `value`.

```JavaScript
        {this.state.counters.map(counter => (
          <Counter
            key={counter.id}
            onDelete={this.handleDelete}
            counter={counter}
          />
        ))}
```

Here is a example of `state`.

```JavaScript
  state = {
    counters: [
      { id: 1, value: 4 },
      { id: 2, value: 3 },
      { id: 3, value: 1 },
      { id: 4, value: 0 }
    ]
  };
```

### RAISING AND HANDLING EVENTS

And

### UPDATING THE STATE

**Rule:**
The component that _ownes_ a piece of the state, should be the one _modifying_ it.

---

Apply a modification in the component that ownes the information.

```JavaScript
  handleDelete = counterId => {
    const counters = this.state.counters.filter(c => c.id !== counterId);
    this.setState({ counters });
  };
```

Send over the prop to the component. In my case `<Counter>`

> Here i changed `value={counter.value} id={counter.id}` to just  
> `counter={counter}`, you access it like this: `this.props.counter.id`

```JavaScript
        {this.state.counters.map(counter => (
          <Counter
            key={counter.id}
            onDelete={this.handleDelete}
            counter={counter}
          />
        ))}
```

Access it in `counter` component like this.

```JavaScript
        <button
          onClick={() => this.props.onDelete(this.props.counter.id)}
          className="btn btn-danger btn-sm m-2">
          Delete
        </button>

```

### SINGLE SOURCE OF TRUTH

#### REMOVING THE LOCAL STATE\*

We have learn about this rule.

> **Rule:**  
> The component that _ownes_ a piece of the state, should be the one _modifying_ it.

So lets do it in practice.

- Remove `state` from the Component not owning the item, replace with props if needed. - single source of truth
- Make component handle what it should. - single source of truth

Should look something like this:

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

  handleIncrement = counter => {
    const counters = [...this.state.counters];
    const index = counters.indexOf(counter);
    counters[index] = { ...counter };
    counters[index].value++;
    this.setState({ counters });
  };

  handleReset = () => {
    const counters = this.state.counters.map(c => {
      c.value = 0;
      return c;
    });
    this.setState({ counters });
  };

  handleDelete = counterId => {
    const counters = this.state.counters.filter(c => c.id !== counterId);
    this.setState({ counters });
  };

  render() {
    return (
      <div>
        <button
          onClick={this.handleReset}
          className="btn btn-primary btn-sm m-2"
        >
          Reset
        </button>
        {this.state.counters.map(counter => (
          <Counter
            key={counter.id}
            onDelete={this.handleDelete}
            onIncrement={this.handleIncrement}
            counter={counter}
          />
        ))}
      </div>
    );
  }
}
export default Counters;
```

---

`PROJECTNAME/component/counter.jsx`

```JavaScript
import React, { Component } from "react";
class Counter extends Component {
  render() {
    return (
      <React.Fragment>
        <span className={this.GetBadgeClasses()}>{this.formatCount()}</span>
        <button
          onClick={() => this.props.onIncrement(this.props.counter)}
          className="btn btn-secondary btn-sm"
        >
          Increment
        </button>

        <button
          onClick={() => this.props.onDelete(this.props.counter.id)}
          className="btn btn-danger btn-sm m-2"
        >
          Delete
        </button>
        <ul />
      </React.Fragment>
    );
  }

  GetBadgeClasses() {
    let classes = "badge m-2 badge-";
    classes += this.props.counter === 0 ? "warning" : "primary";
    return classes;
  }

  formatCount() {
    const { value } = this.props.counter;
    return value === 0 ? "Zero" : value;
  }
}

export default Counter;

```

### MULTIPLE COMPONENTS IN SYNC

> - `App`
>   - `NavBar`
>   - `Counters`
>     - `Counter`

Make sure that you import and use `app`, like this.  
`PROJECTNAME/component/index.js`

```JavaScript
import App from './App';
```

```JavaScript
ReactDOM.render(<App />, document.getElementById('root'));
```

Create a `Navbar` component.  
`PROJECTNAME/component/navbar.jsx`

```JavaScript
class NavBar extends Component {
  render() {
    return (
      <nav className="navbar navbar-light bg-light">
        <a className="navbar-brand" href="#">
          Navbar
        </a>
      </nav>
    );
  }
}

export default NavBar;
```

Import `NavBar` and add it to the render.  
`PROJECTNAME/component/app.js`

```Javascript
import NavBar from './components/navbar';
```

```Javascript
class App extends Component {

  render() {
    return (
      <React.Fragment>
        <NavBar/>
      </React.Fragment>
    );
  }
}

export default App;
```

Now import and add the `Counters` part inside a `container`

```JavaScript
import Counters from './components/counters';
```

```JavaScript
class App extends Component {

  render() {
    return (
      <React.Fragment>
        <NavBar/>
        <main className="container">
          <Counters/>
        </main>
      </React.Fragment>
    );
  }
}
```

### LIFTING STATE UP

**We want too display the number of unique items in `Navbar`**
Start by  
Moving `Counters` state and functions to `App`

```JavaScript
  state = {
    counters: [
      { id: 1, value: 4 },
      { id: 2, value: 3 },
      { id: 3, value: 1 },
      { id: 4, value: 0 }
    ]
  };

  handleIncrement = counter => {
    const counters = [...this.state.counters];
    const index = counters.indexOf(counter);
    counters[index] = { ...counter };
    counters[index].value++;
    this.setState({ counters });

  };

  handleReset = () => {
    const counters = this.state.counters.map(c => {
      c.value = 0;
      return c;
    });
    this.setState({ counters });
  };

  handleDelete = counterId => {
    const counters = this.state.counters.filter(c => c.id !== counterId);
    this.setState({ counters });
  };
```

Pass the parameters to `Counters` from `App` like this.

```JavaScript
          <Counters
            counters = {this.state.counters}
            onReset={this.handleReset}
            onIncrement={this.handleIncrement}
            onDelete={this.handleDelete} />
```

In `Counters` access the props instead of the states.

For example like tihs.

`PROJECTNAME/component/Counters.jsx`

```JavaScript
          <Counter
            key={counter.id}
            onDelete={this.props.onDelete}
            onIncrement={this.props.onIncrement}
            counter={counter}
          />
```

Lets pass information between `NavBar` and `App`

`PROJECTNAME/component/App.js`

```JavaScript
<NavBar
  totalCounters={this.state.counters.filter(c => c.value > 0).length}
  />
```

You could access it like this.

`PROJECTNAME/component/navbar.jsx`

```JavaScript
<span className="badge badge-pill badge-secondary">
  {this.props.totalCounters}
</span>
```

## STATELESS FUNCTIONAL COMPONENTS

We have made component with classes so far,
but we could make them with something called stateless functional components.  
First we have the class but underneath i show you the stateless functional component.

`PROJECTNAME/component/navbar.jsx`

> **TIPS**  
> _(Require extension: `burkeholland.simple-react-snippets`
> )_
>
> Type `imrc` to import React component.  
> Type `cc` to create a class component stem.

```JavaScript
import React, { Component } from "react";

class NavBar extends Component {
  render() {
    return (
      <nav className="navbar navbar-light bg-light">
        <a className="navbar-brand" href="https://www.google.com">
          Navbar{" "}
          <span className="badge badge-pill badge-secondary">
            {this.props.totalCounters}
          </span>
        </a>
      </nav>
    );
  }
}

export default NavBar;
```

`PROJECTNAME/component/navbar.jsx`

```JavaScript
import React from "react";

const NavBar = props => {
  return (
    <nav className="navbar navbar-light bg-light">
      <a className="navbar-brand" href="https://www.google.com">
        Navbar{" "}
        <span className="badge badge-pill badge-secondary">
          {props.totalCounters}
        </span>
      </a>
    </nav>
  );
};

export default NavBar;
```

## DESTRUCTURING ARGUMENTS

These things may not look much to the world, but think of the possibilities.

From this..

```JavaScript
const NavBar = props => {
  return (
    <span className="badge badge-pill badge-secondary">
     {props.totalCounters}
    </span>
  );
};

```

..to this.

```JavaScript
const NavBar = ({ totalCounters }) => { };
```

```JavaScript
<span className="badge badge-pill badge-secondary">
  {totalCounters}
</span>
```

---

From this..

```JavaScript
        {this.props.counters.map(counter => (
          <Counter
            key={counter.id}
            onDelete={this.props.onDelete}
            onIncrement={this.props.onIncrement}
            counter={counter}
          />
        ))}
```

To This.

Add this const and remove `this.props.`.

```JavaScript
    const { onReset, counters, onDelete, onIncrement } = this.props;
```

```JavaScript
 {counters.map(counter => (
          <Counter
            key={counter.id}
            onDelete={onDelete}
            onIncrement={onIncrement}
            counter={counter}
          />
        ))}
```

## LIFECYCLE HOOKS

> NOTE:  
> You can not use lifecycle hooks in stateless Functional components.  
>  Use class components.

### MOUNTING PHASE

Console outputs after adding loggs in code.
Executes in this order.

```
App.js:19          App - Constructor
App.js:54          App - Rendered
navbar.jsx:4       NavBar - Rendered
counters.jsx:6     Counters - Rendered
(4)counter.jsx:5   Counter - Rendered
App.js:27          App - Mounted
```
