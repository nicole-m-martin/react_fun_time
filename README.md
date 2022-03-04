Sharpening my react skills with tutorials. Always learning! Yay!

# General Notes:

Components can be classes, or functions with hooks

A class component can have State and it used to be functional components could not, but with the addition of Hooks, they allow us to have state with functional components.

To use **inline style** you need to use two curly brace. ex: style={{ width: '60px' }}

.map() is a high order array method and it takes a function

## Lifecycle Methods:

Lifecycle methods are special methods built-in to React, used to operate on components throughout their duration in the DOM. For example, when the component mounts, renders, updates, or unmounts.

Render is a **Lifecycle Method** (it is the only one that's actually required it runs at a certain point when the components are loaded)

componentDidMount() runs when the app is loaded or mounted, it will fire off immediately

## Class Components:

You can not return directly from a class. We need a method (a function within a class) That method is called **render**.

```javascript
class App extends Component {
  render() {
    return (
      <div className="App">
        <h1>Class Component</h1>
      </div>
    );
  }
}
```

**_Key Prop_** you will get a warning if you do not have a unique 'key' for the items in a list. A common way is to use the id as the key because id's should all be unique. ex: key={user.id}

## Functional Components:

When components don't have State or no longer have state, they don't need to be classes. They are functional components. With the introduction of **_Hooks_** most all of your components will be functional components, because with the hooks, we can have State within the functional components.

Using functional components with Hooks uses less code and looks cleaner.

Traditionally you would have stateless functional components and then you would Class-Based, where you needed to use state or **_lifecycle methods_**

Refactoring into a functional component, because we don't have state. Using an arrow function below. With a function, you don't need a render. You now pass props into the arrow function, so you don't need 'this dot':

```javascript
const UserItem = (props) => {
  const { avatar_url, login, html_url } = props.user;

  return (
    <div className="card text-center">
      <img
        src={avatar_url}
        alt="pic"
        className="round-img"
        style={{ width: '60px' }}
      />
      <h3>{login}</h3>
      <div>
        <a href={html_url} className="btn btn-dark btn-sm my-1">
          More
        </a>
      </div>
    </div>
  );
};
```

## JSX:

**Javascript Syntax Extension**
Basically syntactic sugar to be able to write the output of our component in an XML or HTML like way. Under the hood its actually JS. You don't need to use JSX but it will save time and code to use JSX for your output.

There are a couple of differences between HTML and JSX. One of them is using **className** within JSX, instead of **class**. It will render, but you will get a warning.

for attributes, you will use **htmlFor** with JSX.

```javascript
<div className="App">
  <label htmlFor="name">Name</label>
</div>
```

JSX expressions must have one parent element.
Can use a **fragment** instead of a div. <Fragment> </Fragment>

Add expressions and conditionals in JSX inside of { }.

```javascript
class App extends Component {
  render() {
    const name = 'Lara Croft';

    return (
      <div className="App">
        <h1>Hello {name.toUpperCase()}</h1>
      </div>
    );
  }
}
```

this returns Hello LARA CROFT in browser

## Props:

**Props** are properties that you can pass into a component from the outside. Wherever you want to place the prop, go to that file and use curly braces { } to add an expression, and the way you access props in **class based components** is with {this.props.}

```javascript
App.js;
class App extends Component {
  render() {
    return <Navbar title="Github Finder" icon="fab fa-github" />;
  }
}
```

```javascript
Navbar.js;
export class Navbar extends Component {
  render() {
    return (
      <nav className="navbar bg-primary">
        <h1>
          <i className={this.props.icon}></i>
          {this.props.title}
        </h1>
      </nav>
    );
  }
}
```

_or you can use **defaultProps** within that file._

```javascript
App.js;
class App extends Component {
  render() {
    return <Navbar />;
  }
}
```

```javascript
Navbar.js;
export class Navbar extends Component {
  static defaultProps = {
    title: 'Github Finder',
    icon: 'fab fa-github',
  };
  render() {
    return (
      <nav className="navbar bg-primary">
        <h1>
          <i className={this.props.icon}></i>
          {this.props.title}
        </h1>
      </nav>
    );
  }
}
```

**Prop Types**
Prop types are basically a type checking to tell you your prop should be a string or number or array or object etc. Helps to make sure the props are the correct data type. Use them! Similar to Typescript.

```javascript
Navbar.propTypes = {
  title: PropTypes.string.isRequired,
  icon: PropTypes.string.isRequired,
};
```

## State:

State in React is a JS Object

**Component Level State** component level state means that state is contained within a single component.

When you want to grab something from State within a class, you use {this.state. }

**Better Practice is destructuring**:
before this.state was repeated many times:

```javascript
render() {
    return (
      <div className='card text-center'>
        <img
        src={this.state.avatar_url}
        alt="pic"
        className='round-img'
        style={{ width: '60px'}}
        />
        <h3>{this.state.login}</h3>
        <div>
          <a href={this.state.html_url}
          className='btn btn-dark btn-sm my-1'>
          More</a>
        </div>
      </div>
    )
  }
```

Refactored into destructured code: DRY Code (Don't Repeat Yourself)
pull the values from the state, or the object.

```javascript
 render() {
  const { avatar_url, login, html_url } = this.state
  return (
    <div className='card text-center'>
      <img
      src={avatar_url}
      alt="pic"
      className='round-img'
      style={{ width: '60px'}}
      />
      <h3>{login}</h3>
      <div>
        <a href={html_url}
        className='btn btn-dark btn-sm my-1'>
        More</a>
      </div>
    </div>
  )
}
```

**_Destructured even more inside the refactored functional component_**
from this:

```javascript
const UserItem = (props) => {
  const { avatar_url, login, html_url } = props.user

```

to this:

```javascript
const UserItem = ({ user: { avatar_url, login, html_url } }) => {
  return (
    <div className="card text-center">
      <img
        src={avatar_url}
        alt="pic"
        className="round-img"
        style={{ width: '60px' }}
      />
      <h3>{login}</h3>
      <div>
        <a href={html_url} className="btn btn-dark btn-sm my-1">
          More
        </a>
      </div>
    </div>
  );
};
```

## Pulling Data from an Api:

Use .env file to hold onto secrets like api keys and other info you want to keep hidden.

**Asynchronous Programming**
The modern way to refactor a promise code, is to make asynchronous programming easier with async / await.

no more .then() blocks since **_async_** turns the function into a promise.

With the **_async_** keyword added to the beginning of your function declaration makes it an async function. Then the function now knows to expect the possibility of **_await_** keyword used to invoke asynchronous code.

```javascript
app.js;
class App extends Component {
  // set starting state:
  state = {
    users: [],
    loading: false,
  };
  // make the promise function with async / await
  // on mount the state will change loading to true, then we call axios to pull data from github api and the res awaits the promise, and when it returns the loading is now false and the users are rendered to the page.
  async componentDidMount() {
    this.setState({ loading: true });

    const res = await axios.get('https://api.github.com/users');

    this.setState({ users: res.data, loading: false });
  }
  render() {
    return (
      <div className="App">
        <Navbar />
        <div className="container">
          <Users loading={this.state.loading} users={this.state.users} />
        </div>
      </div>
    );
  }
}
```

with an arrow function you add **async** before the parameter, not the beginning.
ex:

```javascript
searchUsers = async (text) => {
  this.setState({ loading: true });

  const res = await axios.get(
    `https://api.github.com/search/users?q=${text}&client_id=${process.env.REACT_APP_GITHUB_CLIENT_ID}&client_secret=${process.env.REACT_APP_GITHUB_CLIENT_SECRET}`
  );

  this.setState({ users: res.data.items, loading: false });
};
```
