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

# Conditional Rendering
> https://reactjs.org/docs/conditional-rendering.html

```
class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
);
```

### Inline If with Logical && Operator

```
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```

### Inline If-Else with Conditional Operator
```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
    </div>
  );
}
```
or
```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn
        ? <LogoutButton onClick={this.handleLogoutClick} />
        : <LoginButton onClick={this.handleLoginClick} />
      }
    </div>
  );
}
```

### Preventing Component from Rendering
```
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }

  return (
    <div className="warning">
      Warning!
    </div>
  );
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = {showWarning: true};
    this.handleToggleClick = this.handleToggleClick.bind(this);
  }

  handleToggleClick() {
    this.setState(state => ({
      showWarning: !state.showWarning
    }));
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Hide' : 'Show'}
        </button>
      </div>
    );
  }
}
```

# Lists and Keys
> https://reactjs.org/docs/lists-and-keys.html

```
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
```

### Rendering Multiple Components'
每個item一定要有key

```
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number, index) => <li key={index}>{number}</li>)
  return (<ul>{listItems}</ul>);
}

const numbers = [1, 2, 3, 4, 5];

ReactDOM.render(
  <NumberList numbers={numbers} />, document.getElementById('root')
);
```

### Extracting Components with Keys
key定義的時間點要在array同一個block
```
function ListItem(props) {
  // key 不能定義在這裡
  return <li>{props.value}</li>
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // key 要定義在這裡
    <ListItem key={number.toString()} value={number} />
  );

  return (<ul>{listItems}</ul>);
}

const numbers = [1, 2, 3, 4, 5];

ReactDOM.render(
  <NumberList numbers={numbers} />, document.getElementById('root')
);

```

### Keys Must Only Be Unique Among Siblings
不同的array可以用同一個名稱的key，不需要考慮全域的狀況

```
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);
```

### Embedding map() in JSX
```
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

# Forms
> https://reactjs.org/docs/forms.html

### Controlled Components
```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {name: '', description: '', age: 0};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({[event.target.name]: event.target.value});
  }

  handleSubmit(event) {
    console.log('name:' + this.state.name);
    console.log('description:' + this.state.description);
    console.log('age:' + this.state.age);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" name="name" value={this.state.name} onChange={this.handleChange} />
        </label>
        <br />
        <label>
          Description:
          <textarea name="description" value={this.state.description} onChange={this.handleChange} />
        </label>
        <br />
        <label>
          Age:
          <select name="age" value={this.state.age} onChange={this.handleChange}>
            <option value="10">Ten years</option>
            <option value="20">Twenty years</option>
            <option value="30">Thirty years</option>
            <option value="40">Forty years</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    )
  };
}

ReactDOM.render(<NameForm />, document.getElementById('root'));
```

##### Note:
You can pass an array into the value attribute, allowing you to select multiple options in a select tag:
```
<select multiple={true} value={['B', 'C']}>
```

### The file input Tag
> https://reactjs.org/docs/uncontrolled-components.html#the-file-input-tag

```
<input type="file" />
```

### Handling Multiple Inputs
```
// ES6
this.setState({
  [name]: value
});

// ES5
var partialState = {};
partialState[name] = value;
this.setState(partialState);
```

### Controlled Input Null Value
```
ReactDOM.render(<input value="hi" />, mountNode);

setTimeout(function() {
  ReactDOM.render(<input value={null} />, mountNode);
}, 1000);
```

### Alternatives to Controlled Components
> https://reactjs.org/docs/uncontrolled-components.html

### Fully-Fledged Solutions
> https://jaredpalmer.com/formik

# Lifting State Up
> https://reactjs.org/docs/lifting-state-up.html






