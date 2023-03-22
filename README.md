```
 // Title
  ## Prototype

    // Sub Title
    ### Home

      // Sub Title descriptor
      <h4> Rest Oeprator </h4>

  // Text Bold
  **For Bold Text**
```

## React Components and Props Core Concept

- React is a vanilla js library and React element is a vanilla js object
- You can write the element at once but you can't change it but you can create so many components as a chilidren of that component
- React element and the component is not the same thing
- What we pass in the component attribute that will be the parameter of the function and that will stay and pass as an object
  -React give us the class component so that we can write stateful component
- After extends React.Component react call the render method
- In the class component props will write with this. props
- Should not change the props value in jsx when already pass the value in the component

## React State & Lifecycle in Class Component

- Class Component is statefull component
- Functional Component is a stateless component
- In functional component we use `useEffect()` hook instead of class lifecycle method
- `props` will be change from outside of the component and `state` will be define inside the component
- `state` means data of `component`
- `state` is property of `React.Component` method
- `rendar` is a method
- `state` is js `object`
- A `state` always should have initial value
- If we need `setSate` change with `state` value we can use arrow function of normal function in `setState`

```
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

- If we work on any `reference value` we should not work with `this.state.value`. Instead we will create another instance in `immutable` way and we will modify them.

- `React` is one way data flow. Always data flow to it's child.

### componentDidMount

- `componentDidMount(){}` is lifecycle `event` or `hook`
- After loading browser that means when browser get load and ready to show website what will be happen to the website that will be define in `componentDidMount(){}` `hook`

### componentWillUnmount

- `componentWillUnmount(){}` is lifecycle `event` or `hook`
- When element get away from dom before that what will be happen to that element that will be define in `componentWillUnmount(){}` `hook`

```
import React from 'react';

class Clock extends React.Compotent{
  constructor(props){
    super(props);
    this.state = {date: new Date()}
  }

componentDidMount(){
 this.clockTimer =  setInterval(() => this.tick(), 1000);
}

tick(){
  this.setState(){
    date: new Date(),
  };
}

componentWillUnmount(){
  clearInterval(this.clockTimer)
}

  render(){
    return(
      <h1 className="heading">
        <span className="text">{new Date().toLocalTimeString(this.state.date)}</span>
      </h1>
    );
  }
}
```

## React Event Handling & Control Re Rendering

<h4>Contents of this video:</h4>

- 0:00 - Intro
- 1:34 - Event Handling
- 06:57 - ESLint Warning Solution
- 14:42 - "this" confusion & solution
- 34:49 - Passing parameters
- 37:30 - Detect & Control Re-render
- 59:45 - My last words

### We can solve `this` keyword issue in three 4 ways in `class component`

1. `arrow function`

- This is the best way to prevent `this` keyword confusion in react
- This is one of the main reason `arrow function` created for

```
    handleClick = (locale) => {
        this.setState({
            locale,
        });
    };
```

2. `bind(this)` in `constructor`

```
    constructor(props) {
        super(props);
        this.state = { date: new Date(), locale: 'bn-BD' };
        this.handleClick = this.handleClick.bind(this);
    }
```

3. Directly use `arrow function` in button

```
 <Button change={() => this.handleClick()} locale="en-US">
      Click here
  </Button>
```

4. We can directly bind `this` with `handleclick()` function. In this way we can also pass parameter.

```
 <Button change={() => this.handleClick().bind(this, parameter)}>
      Click here
  </Button>
```

- Full Example:

```

import React from 'react';
import Button from './Button';

class Clock extends React.Component {
    state = { date: new Date(), locale: 'bn-BD' };

    // constructor(props) {
    //     super(props);
    //     this.state = { date: new Date(), locale: 'bn-BD' };
    //     // this.handleClick = this.handleClick.bind(this);
    // }

    componentDidMount() {
        this.clockTimer = setInterval(() => this.tick(), 1000);
    }

    componentWillUnmount() {
        clearInterval(this.clockTimer);
    }

    // handleClick = (locale) => {
    //     this.setState({
    //         locale,
    //     });
    // };

    handleClick(locale) {
        this.setState({
            locale,
        });
    }

    tick() {
        this.setState({
            date: new Date(),
        });
    }

    render() {
        console.log('clock component rendered');
        const { date, locale } = this.state;
        return (
            <div>
                <h1 className="heading">
                    <span className="text">{date.toLocaleTimeString(locale)}</span>
                </h1>
                <Button change={() => this.handleClick()}>
                    Click here
                </Button>
            </div>
        );
    }
}

export default Clock;
```

-  `componentDidMount()` is invoked immediately after a component is mounted (inserted into the tree). Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.
- `componentDidMount` means after the browser load complete what we want to do that logic will be in this react lifecycle method

```
componentDidMount() {
     this.clockTimer = setInterval(() => this.tick(), 1000);
 }
```

- `componentWillUnmount()` is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in `componentDidMount()`
- `componentWillUnmount` means after the `componentDidMount` completion or This method is called when a component is being removed from the DOM

`
 componentWillUnmount() {
     clearInterval(this.clockTimer);
 }
    `

