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
