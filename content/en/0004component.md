---
title: component
description: ""
position: 5
category: Guide
---

## function component

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### rendering the component

```js
const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

## class component

```js
class Welcome extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      return <h1>Hello, {this.props.name}</h1>;
    );
  }
}
```

### rendering the component

```js
ReactDOM.render(<Welcome name="sarah" />, document.getElementById('root'))
```

## jsx

use {} to use javascript expressions

use className instead of class and

use htmlFor instead of for

use camel case to all html property

exemple

```jsx
return(
    <div className="test-class" onClick={() => {
        alert("clicked");
    }}>test jsx</div>
)
```

## props

### props in function component

pass an anrgument to the fuction conmponent and access the props in this argument

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### props in class component

add the props argument to the constructor, call supper(props) access this with the this.props property

```jsx
class Welcome extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      return <h1>Hello, {this.props.name}</h1>;
    );
  }
}
```

to access the children element of a component, use props.childer

```jsx
<Welcome>
    <h1>children element</h1>
</Welcome>
```

to get his h1, use props.children

## state

initialize an property state iny the constructor

and use the this.setState method to change the state

exemple

```jsx
export default class Welcome extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            message: "welcome"
        };
    }

    handleClick() {
       this.setState((state, props) => {
            return { message: "button clicked" }
        });
    }
    render() {
        return (
            <div>
                <div>{ this.state.message }</div>
                <button onClick={ () => {this.handleClick()} }>Click</button>
            </div>
        )
    }
}
```

## class component lifecycle

use the componentDidMont() and componentWillUnmon() method

## event handling

### in fuctional component

```jsx
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={(e) => {handleClick(e)}}>
      Click me
    </a>
  );
}
```

### in class component

```jsx
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

## child component to parent component communication

pass a function **reference** as a props to the child component

exemple

parent component

```jsx
export default function Parent() {
    function communicationHandler(message) {
        console.log(message);
    }
    return (
        <div>
            <Child communicationHandler= {communicationHandler} ></Child>
        </div>
    )
}
```

child component

```jsx
export default function Child(props) {
    return (
        <div>
            <button onClick={ (e) => {props.communicationHandler("data form child")} }>communicate to parent</button>
        </div>
    )
}
```

## conditional rendering

use an element variable

exemple

```jsx
export default function Conditional() {
    const isLogedIn = true;
    let button;
    if (isLogedIn) {
        button = (
            <button>logout</button>
        )
    } else {
        button = (
            <button>login</button>
        );
    }
    return (
        <div>
            {button}
        </div>
    )
}
```

## list rendering

trasform the array to a jsx using the javascript map function

exemple

```jsx
export default function List() {
    let cars = ["BMW", "Toyota", "Nissan"]
    return (
        <ul>
            {
                cars.map((item, index) => {
                    return (
                        <li key={index}>{ item }</li>
                    )
                })
            }
        </ul>
    )
}
```

## styling

to use css, import the css file in the component js file

exemple

```jsx
import React from 'react'

import './List.css'

export default function List() {
    let cars = ["BMW", "Toyota", "Nissan"]
    return (
        <ul>
            {
                cars.map((item, index) => {
                    return (
                        <li key={index} className="test">{ item }</li>
                    )
                })
            }
        </ul>
    )
}
```

### scoped style

use the styles module

exemple

```php
import React from 'react'

import styles from './List.module.css';

export default function List() {
    let cars = ["BMW", "Toyota", "Nissan"]
    return (
        <ul>
            {
                cars.map((item, index) => {
                    return (
                        <li key={index} className={styles.test}>{ item }</li>
                    )
                })
            }
        </ul>
    )
}
```

### inline style

not recomended

exemple

```jsx
export default function List() {
    let cars = ["BMW", "Toyota", "Nissan"]
    let liStyle = {
        color: "red",
        fontWeight: "bold"
    }
    return (
        <ul>
            {
                cars.map((item, index) => {
                    return (
                        <li key={index} style={liStyle}>{ item }</li>
                    )
                })
            }
        </ul>
    )
}
```

## lifecycle

use the componentDidMount(), componentWillUnmount(), and componentDidUpdate()