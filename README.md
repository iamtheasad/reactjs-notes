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

## Why Learn React?

- Organization
- Reusable
- Flexibility - Mobile and Desktop
- Popularity & Support
- Performance

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

- `state` is a object property and `setState` is a method of a class
- Class Component is statefull component
- Functional Component is a stateless component
- In functional component we use `useEffect()` hook instead of class lifecycle method
- `props` will be change from outside of the component and `state` will be define inside the component
- `state` means data of `component`
- `state` is property of `React.Component` method
- `rendar` is a method
- `state` is js `object` property
- A `state` always should have initial value
- If we need `setSate` change with `state` value we can use arrow function of normal function in `setState`
- Whenever call `setState()` it will call react `render` method

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

- Note: `.bind(this, parameter)` this syntax every time render new function so it should not be use.

<b>Full Example:</b>

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

<h4>componentDidMount()</h4>

- `componentDidMount()` is invoked immediately after a component is mounted (inserted into the tree). Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.
- `componentDidMount` means after the browser load complete what we want to do that logic will be in this react lifecycle method

```
componentDidMount() {
     this.clockTimer = setInterval(() => this.tick(), 1000);
 }
```

<h4>componentWillUnmount()</h4>

- `componentWillUnmount()` is invoked immediately before a component is unmounted and destroyed. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in `componentDidMount()`
- `componentWillUnmount` means after the `componentDidMount` completion or This method is called when a component is being removed from the DOM

```
 componentWillUnmount() {
     clearInterval(this.clockTimer);
 }
```

<h4>componentDidUpdate()</h4>

- It works after `componentDidMount()` render whenever need to update something in your component it should use there

<h4>shouldComponentUpdate(nextProps, nextState)</h4>

- It should use only when a huge component re rendering every time and it's cost a huge perfamnce issue other wise don't use it.

<b>Clock Component</b>

```
import React from "react";
import Button from "./Button";

class Clock extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      locale: "en-US",
      date: new Date()
    };
  }

  componentDidMount() {
    this.localTimer = setInterval(() => {
      this.setState({
        date: new Date()
      });
    }, 1000);
  }

  componentWillUnmount() {
    clearInterval(this.localTimer);
  }

  handleClick = (locale) => {
    this.setState({
      locale: locale
    });
  };

  render() {
    console.log("Clock Component Rendered");

    const { locale, date } = this.state;
    return (
      <>
        <div>{date.toLocaleTimeString(locale)}</div>
        <Button change={this.handleClick} locale="bn-BD" />
      </>
    );
  }
}

export default Clock;

```

**Button Component**

```
import React from "react";

class Button extends React.Component {
  shouldComponentUpdate(nextProps) {
    const { change: currentChange, locale: currentLocale } = this.props;
    const { change: nextChange, locale: nextLocale } = nextProps;

    if (currentChange === nextChange && currentLocale === nextLocale) {
      return false;
    } else {
      return true;
    }
  }

  render() {
    const { change, locale } = this.props;
    console.log("BUttonr rendered");
    return (

      <button type="button" onClick={() => change(locale)}>
        Time Language Change On click
      </button>
    );
  }
}

export default Button;

```

## Composition & Inheritance

- Reactjs don't sajest to do inheritance in class.

## React Lifting State Up

- React lifting state up, HOC and render props are the same thing. But it's have some difference.

## HOC - Higher Order Component

- HOC is a function
- It's reduce code duplication
- HOC component start with small letter `withCounter`

- HOC creation:

```
import React from "react";
import Counter from "../HigerOrder/Counter";

const withCounter = (OriginalComponent) => {
  class NewComponent extends React.Component {
    state = {
      count: 0
    };

    incrementalCount = () => {
      this.setState((prevState) => ({
        count: prevState.count + 1
      }));
    };

    render() {
      const { count } = this.state;
      return (
        <OriginalComponent
          count={count}
          incrementalCount={this.incrementalCount}
        />
      );
    }
  }

  return NewComponent;
};

export default withCounter;

```

- HOC uses in component label:

```
import React from "react";
import withCounter from "./HOC2/withCounter";

const Counter2 = (props) => {
  const { count, inCrementCounter } = props;
  return (
    <div>
      <p onClick={inCrementCounter}>You Clicked {count} Times</p>
    </div>
  );
};

export default withCounter(Counter2);
```

## React Render Props

- Render props define render logic outside of component
- Render props pass as a function and itself can get props

`Counter.js` file

```
import React from "react";

export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  incrementCount = () => {
    this.setState((prevState, props) => ({
      count: prevState.count + 1
    }));
  };

  render() {
    const { count } = this.state;
    const { render } = this.props;

    return <div>{render(count, this.incrementCount)}</div>;
  }
}
```

`App.js`

- I called `Counter` component and pass `render` as `function` props

```
import React from "react";
import ClickCounter from "./components/ClickCounter";
import { Counter } from "./components/Counter";
import HoverCounter from "./components/HoverCounter";

import "./styles.css";

export default class App extends React.Component {
  render() {
    return (
      <div className="App">
        {/* <User name={(isLoggedIn) => isLoggedIn ? 'RAna' : 'Guest'} /> */}

        <Counter
          render={(count, incrementCount) => (
            <ClickCounter count={count} incrementCount={incrementCount} />
          )}
        />

        <Counter
          render={(count, incrementCount) => (
            <HoverCounter count={count} incrementCount={incrementCount} />
          )}
        />
      </div>
    );
  }
}

```

`ClickCounter` File

```
import React from "react";

class ClickCounter extends React.Component {
  render() {
    const { incrementCount, count } = this.props;

    return (
      <button type="button" onClick={incrementCount}>
        click here {count}
      </button>
    );
  }
}

export default ClickCounter;

```

`HoverCounter` file

```
import React from "react";

class HoverCounter extends React.Component {
  render() {
    const { incrementCount, count } = this.props;

    return <h1 onMouseOver={incrementCount}>Hover Over Counter {count}</h1>;
  }
}

export default HoverCounter;
```

## Hooks

### useEffect Hook

<h4>React Responsibilities:</h4>

- UI Render
- React to user input / actions
- Render jsx code
- Manage state and props
- React events / inputs
- Evaluating state / props change

<h4>useEffect Details</h4>

- <b>It only works for maintain side effects of a react component</b>

- **Exampe of side effects:**

  1. Fetchind data from any API
  2. Updating Dom
  3. Settings any subscriptions or timers

- `useEffect` is a function
- `useEffect` run in every render
- It works like `componentDidMount componentDidUnmount componentDidUpdate` lifecycle method of class component
- On every render `useEffect` will run again but you can stop re-render `useEffect` by conditionally using `[]` array as optional argument

<b>without condition</b>

```
useEffect(() => {
  document.title = `You clicked ${count} times`;
}); // Everytime will re-render this if component render
```

<b>first time render</b>

```
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, []); // Only run first time when component render
```

<b>with condition</b>

```
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

- If you start any timer in `useEffect` you should stop it, otherwise it will create memory leak situation and it will create performance issues grately.

```
const [date, setDate] = useState(new Date());

const tick = () =>{
  setDate(new Date());
}

useEffect(() => {
  console.log('Starting Timer');

const interval = setInerval(tick, 1000); // Initialize timer in every 1 seconds after.

// Clearing set interval using return a function

return () => {
  clearInterval(interval);
}

}, []); // Only first time run on first time DOM loading
```

- If `useEffect` hook reuturn something it will clean up the thins what `useEffect` started like React class lifecyle method `componentDidUnmount`.
- Timer always should be stop manually whenever component unmounted

## useCallback Hook

- `useCallback` remember function between re-render.
- `useCallback` return memoized version of the callback function that only changes if one of the dependencies has changed. Just like `useEffect` it will return a cleanup function.
- `useCallback` is similar to `useMemo` but it will return a memoized function.
- `useCallback` is useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders.
- `useCallback` remember the function reference between re-render.
- `useCallback` mainly used for remembering function reference.

## useMemo Hook

- `useMemo` remember the value between re-render. Not reference like `useCallback`.
- `useMemo` remember a function return value and avoid re-render the value
- `useMemo` will re-render only when his dependecy array change.
- `useMemo` itself a function so don't need to call function in jsx.

## useReducer Hook

I don't understatnd what is this

`myUsReducer.js`

```
import { useReducer } from "react";

let initialState = 5;

const reducer = (state, action) => {
  switch (action) {
    case "increment":
      return state + 1;
    case "decrement":
      return state - 1;
    default:
      return state;
  }
};

function MyUseReducer() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      <p>Count - {state}</p>
      <button onClick={() => dispatch("increment")}>Increment</button>
      <br />
      <br />
      <button onClick={() => dispatch("decrement")}>Decrement</button>
    </>
  );
}

export default MyUseReducer;

```

`useReducerComplexExample.js`

```
import { useReducer } from "react";

let initialState = {
  counter: 0,
  counter2: 0
};
const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return { ...state, counter: state.counter + action.value };
    case "decrement":
      return { ...state, counter: state.counter - action.value };
    case "increment2":
      return { ...state, counter2: state.counter2 + action.value };
    case "decrement2":
      return { ...state, counter2: state.counter2 - action.value };
    default:
      return state.counter;
  }
};

export const MyUseReducerComplex = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <div>
        <p>Count - {state.counter}</p>
        <button
          onClick={() =>
            dispatch({
              type: "increment",
              value: 1
            })
          }
        >
          Increment By 1
        </button>

        <button onClick={() => dispatch({ type: "decrement", value: 1 })}>
          Decrement By 1
        </button>
      </div>
      <div>
        <p>Count2 - {state.counter2}</p>
        <button
          onClick={() =>
            dispatch({
              type: "increment2",
              value: 1
            })
          }
        >
          Increment2 By 1
        </button>

        <button onClick={() => dispatch({ type: "decrement2", value: 1 })}>
          Decrement2 By 1
        </button>
      </div>
    </div>
  );
};

```

- Multiple useReducer in same component
  `CounterThree.js`

```
import { useReducer } from "react";

let initialState = 0;
let initialState2 = 5;

const reducer = (state, action) => {
  switch (action) {
    case "increment":
      return state + 1;
    case "decrement":
      return state - 1;
    default:
      return state;
  }
};

function CounterThree() {
  const [state, dispatch] = useReducer(reducer, initialState);
  const [state2, dispatch2] = useReducer(reducer, initialState2);

  return (
    <>
      <div>
        <p>Count - {state}</p>
        <button onClick={() => dispatch("increment")}>Increment</button>
        <br />
        <br />
        <button onClick={() => dispatch("decrement")}>Decrement</button>
      </div>
      <div>
        <p>Count2 - {state2}</p>
        <button onClick={() => dispatch2("increment")}>Increment</button>
        <br />
        <br />
        <button onClick={() => dispatch2("decrement")}>Decrement</button>
      </div>
    </>
  );
}

export default CounterThree;

```

## Event Bubbling or Event Propagation

- When we click or any event happen on child element it's also fire event on it's parent, this is call event bubbling. We can prevent it with `event.stopPropagation()` function

```
import './App.css';
function App() {
  const handleHeaderClick = () => {
    console.log('Header was clicked');
  };
  const handleButtonClick = (event) => {
    event.stopPropagation();
    console.log('The logout button was clicked');
  };

  return (
    <>
      <div className="styleHeader" onClick={handleHeaderClick}>
        <div>Header</div>
        <button type="button" onClick={handleButtonClick}>
          Log Out
        </button>
      </div>
    </>
  );
}
export default App;
```

## Creating New Array With Custom Array Property

```
const essentialData = books.map((book) => ({
  title: book.title,
  author: book.author,
  reviewsCount: getTotalReviewCount(book),
}));

```

## Moste Used Javascript For Reactjs

```
const data = [
  {
    id: 1,
    title: "The Lord of the Rings",
    publicationDate: "1954-07-29",
    author: "J. R. R. Tolkien",
    genres: [
      "fantasy",
      "high-fantasy",
      "adventure",
      "fiction",
      "novels",
      "literature",
    ],
    hasMovieAdaptation: false,
    pages: 1216,
    translations: {
      spanish: "El señor de los anillos",
      chinese: "魔戒",
      french: "Le Seigneur des anneaux",
    },
    reviews: {
      goodreads: {
        rating: 4.52,
        ratingsCount: 630994,
        reviewsCount: 13417,
      },
      librarything: {
        rating: 4.53,
        ratingsCount: 47166,
        reviewsCount: 452,
      },
    },
  },
  {
    id: 2,
    title: "The Cyberiad",
    publicationDate: "1965-01-01",
    author: "Stanislaw Lem",
    genres: [
      "science fiction",
      "humor",
      "speculative fiction",
      "short stories",
      "fantasy",
    ],
    hasMovieAdaptation: false,
    pages: 295,
    translations: {},
    reviews: {
      goodreads: {
        rating: 4.16,
        ratingsCount: 11663,
        reviewsCount: 812,
      },
      librarything: {
        rating: 4.13,
        ratingsCount: 2434,
        reviewsCount: 0,
      },
    },
  },
  {
    id: 3,
    title: "Dune",
    publicationDate: "1965-01-01",
    author: "Frank Herbert",
    genres: ["science fiction", "novel", "adventure"],
    hasMovieAdaptation: false,
    pages: 658,
    translations: {
      spanish: "",
    },
    reviews: {
      goodreads: {
        rating: 4.25,
        ratingsCount: 1142893,
        reviewsCount: 49701,
      },
    },
  },
  {
    id: 4,
    title: "Harry Potter and the Philosopher's Stone",
    publicationDate: "1997-06-26",
    author: "J. K. Rowling",
    genres: ["fantasy", "adventure"],
    hasMovieAdaptation: true,
    pages: 223,
    translations: {
      spanish: "Harry Potter y la piedra filosofal",
      korean: "해리 포터와 마법사의 돌",
      bengali: "হ্যারি পটার এন্ড দ্য ফিলোসফার্স স্টোন",
      portuguese: "Harry Potter e a Pedra Filosofal",
    },
    reviews: {
      goodreads: {
        rating: 4.47,
        ratingsCount: 8910059,
        reviewsCount: 140625,
      },
      librarything: {
        rating: 4.29,
        ratingsCount: 120941,
        reviewsCount: 1960,
      },
    },
  },
  {
    id: 5,
    title: "A Game of Thrones",
    publicationDate: "1996-08-01",
    author: "George R. R. Martin",
    genres: ["fantasy", "high-fantasy", "novel", "fantasy fiction"],
    hasMovieAdaptation: true,
    pages: 835,
    translations: {
      korean: "왕좌의 게임",
      polish: "Gra o tron",
      portuguese: "A Guerra dos Tronos",
      spanish: "Juego de tronos",
    },
    reviews: {
      goodreads: {
        rating: 4.44,
        ratingsCount: 2295233,
        reviewsCount: 59058,
      },
      librarything: {
        rating: 4.36,
        ratingsCount: 38358,
        reviewsCount: 1095,
      },
    },
  },
];
/*
function getTotalReviewCount(book) {
  const goodread = book.reviews?.goodreads?.reviewsCount;
  const librarything = book.reviews?.librarything?.reviewsCount ?? 0;

  goodread;
  librarything;
  return goodread + librarything;
}

const essentialData = data.map((ele) => {
  return {
    bookTitle: ele.title,
    bookAuthor: ele.author,
    reviewsCount: getTotalReviewCount(ele),
  };
});

console.log(essentialData);

const rana = essentialData.map((ele) => ele.bookTitle);

console.log(rana);
 */
// function getBooks() {
//   return data;
// }

// function getBook(id) {
//   return data.find((d) => d.id === id);
// }

// // Destructuring

// const book = getBook(3);

// // const title = book.title;
// // const author = book.author;

// const { title, publicationDate, author, genres } = book;

// const primaryGenre = genres[0];
// const secondaryGenre = genres[1];

// primaryGenre;
// secondaryGenre;

// // Rest Operator
// const [a, d, f, ...resOp] = genres;
// console.log(a, d, f, resOp);

// const newBook = { book, rana: 1 };
// newBook;

// // Spread Operator Using in a Object
// const newObj = {
//   ...book,
//   // Adding new property in newObj
//   movieReleaseDate: "24-12-24",
//   // Over writing existing property
//   pages: 343,
// };
// newObj;

// // Spread Operator Using in a Array
// const newGenres = [...genres, "rana"];
// newGenres;

// /* const countWrong = book.reviews.librarything.reviewsCount || "no data";
// countWrong;
// // Nullis Coalescing Operator
// const count = book.reviews.librarything.reviewsCount ?? "no data";
// count; */

function getTotalReviewCount(book) {
  const goodread = book.reviews.goodreads.reviewsCount;
  const librarything = book.reviews.librarything?.reviewsCount ?? 0;

  goodread;
  librarything;
  return goodread + librarything;
}

// console.log(getTotalReviewCount(book));

function getBook(id) {
  return data;
}

const books = getBook();

books;

const essentialData = books.map((book) => ({
  title: book.title,
  author: book.author,
  reviewsCount: getTotalReviewCount(book),
}));

essentialData;

let x = essentialData.map((item) => item.title);
x;

const longBooksWithMovie = books
  .filter((book) => book.pages > 500)
  .filter((book) => book.hasMovieAdaptation);
longBooksWithMovie;

let adventureBook = books
  .filter((book) => book.genres.includes("adventure"))
  .map((book) => book.title);
adventureBook;

// Reducer
const pagesAllBooks = books.reduce((acc, book) => acc + book.pages, 0);
pagesAllBooks;

// Array Sorting
const arr = [3, 7, 1, 9, 6];

const sorted = arr.slice().sort((a, b) => b - a);
sorted;
arr;

const sortedByPages = books.slice().sort((a, b) => b.pages - a.pages);
sortedByPages;

```

## Js Notes

### `rest` operator

- `rest` operator only works with array
- It means বাকি যা আছে তা সব দেখানো

### `spread` operator

- It means ছরিয়ে দেয়া
- `spread` operator works with both array and object
