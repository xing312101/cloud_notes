# Main Concepts
> reference: https://reactjs.org/docs/hello-world.html

> Using create-react-app to initial project

# Hello World
> https://reactjs.org/docs/hello-world.html

先在 src/index.js 做修改
```
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

# Introducing JSX
> https://reactjs.org/docs/introducing-jsx.html

### Embedding Expressions in JSX
在view跟javascript的code可以混著寫進value
```
const name = "Xing312101";
const element = <h1>Hello, {name}</h1>
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

### Specifying Attributes with JSX

React DOM 是採用駝峰式命名property, attribute或class name
```
const element = <img src={user.avatarUrl}></img>;
```

### Specifying Children with JSX
如果tag是沒有對應的結尾tag，需要用 / 來做結尾
```
const element = <img src={user.avatarUrl} />;
```

### JSX Prevents Injection Attacks
```
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```

### JSX Represents Objects
Babel compiler 會把JSX轉譯到React.createElement()
```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);

const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```
React.createElement()會做些檢查然後產出沒有BUG的程式
```
類似這樣的程式，下面範例是簡化的sample
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

# Rendering Elements
> https://reactjs.org/docs/rendering-elements.html

### Rendering an Element into the DOM
通常ReactDOM 會在id是root的div進行
```
html:
<div id="root"></div>

js:
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### Updating the Rendered Element
React Dom 在html只會更新有修改的資料
```
function tick() {
  var now = new Date();
  const element = (
    <div>
      <h1>Hello, YuXing.</h1>
      <h2>Date: {now.toLocaleDateString()}</h2>
      <h2>Time: {now.toLocaleTimeString()}</h2>
    </div>
  );

  ReactDOM.render(element, document.getElementById('root'));
}
setInterval(tick, 1000);
```

# Components and Props
> https://reactjs.org/docs/components-and-props.html

> All React components must act like pure functions with respect to their props.

componet 可以看作是javascript的function，參數可以帶入任何型態的input，react稱這個input叫做 props

### Function and Class Components
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
##### using ES6 class to define acomponet
```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

### Rendering a Component
```
function Wellcome(props) {
  return <h1>Hello, {this.props.name}</h1>
}

const element = <Wellcome name="YuXing" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

### Composing Components
```
function Wellcome(props) {
  return <h1>Hello, {props.name}</h1>
}

function AppCompoents() {
  return (
    <div>
      <Wellcome name="YuXing" />
      <Wellcome name="Yu Xing" />
      <Wellcome name="Xing312101" />
    </div>
  );
}

ReactDOM.render(
  <AppCompoents />,
  document.getElementById('root')
);
```

### Extracting Components
```
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
##### ↓↓↓↓↓↓↓↓↓↓
```
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}

function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}

function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

### Props are Read-Only
以下是 return value or 修改自己本身的值的function，都不是修改props
```
function sum(a, b) {
  return a + b;
}
```
```
function withdraw(account, amount) {
  account.total -= amount;
}
```

# State and Lifecycle
> https://reactjs.org/docs/state-and-lifecycle.html

### Converting a Function to a Class
```
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, YuXing. This is class Clock.</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

### Adding Local State to a Class
```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, YuXing. This is class Clock.</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
    <Clock />,
    document.getElementById('root')
);
```

### Adding Lifecycle Methods to a Class
> componentDidMount
> componentWillUnmount

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerId = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerId);
  }

  tick() {
    this.setState({
      date: new Date()
    })
  }

  render() {
    return (
      <div>
        <h1>Hello, YuXing. This is class Clock.</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);

```

# Using State Correctly
> There are three things you should know about setState().

### Do Not Modify State Directly
```
// Wrong
this.state.comment = 'Hello';

// Correct
this.setState({comment: 'Hello'});
```

### State Updates May Be Asynchronous
> Because this.props and this.state may be updated asynchronously, you should not rely on their values for calculating the next state.

```
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});

// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));

// Correct
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
```

### State Updates are Merged
> You can update them independently with separate setState()

```
  constructor(props) {
    super(props);
    this.state = {
      posts: [],
      comments: []
    };
  }

  componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
  }
```

# Handling Events
> https://reactjs.org/docs/handling-events.html

### Some different
##### event name
```
// HTML:
<button onclick="activateLasers()">
  Activate Lasers
</button>

// React:
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

##### It can't return false in react
```
// HTML:
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>

// React:
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

### Using an ES6 class
```
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>{this.state.isToggleOn ? 'On' : 'Off'}</button>
    );
  }
}

ReactDOM.render(<Toggle />, document.getElementById('root'));
```
##### without binding code
experimental
```
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```
use an arrow function in the callback
```
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={() => this.handleClick()}>
        Click me
      </button>
    );
  }
}
```

### Passing Arguments to Event Handlers
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```
