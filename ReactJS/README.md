# What is React.

React is one of the most popular JavaScript libraries for front-end web applications.React uses a Virtual DOM, allowing to update only the parts of the website that have changed.


# How to create React App.
- Make sure you have node installed in your machine.

npx create-react-app my-app
cd my-app
npm start 

# Folders of React App.

- Public Folder :- The public folder contains files related to how the application will display on the client, the most important of those being index.html, which is the HTML template of our page:

- Src Folder :-The src folder contains all of the JavaScript, CSS, and image files that will be compiled into a bundle file and injected into index.html

package.json: holds various metadata relevant to the project, like dependencies.

index.js file is the entry point to the React Application.

# How is React compiled into a bundle file? 

It uses what is called a "file loader". In the case of Create React App, Webpack is used.
Webpack creates a "bundle" file containing the content of multiple files that need to be "bundled" together and it is all added together into a single file. Instead of making the HTML file go and find multiple files, which can slow down load times tremendously, it only has to find one file.


While there are other files in the src folder that come with Create React App when it is generated, the two files below are the only critical files:
• index.js: This file is the entry point into our application. In our code, a method called ReactDOM.render() is used to find an element with id="root" in the HTML and add our React application inside of that element (similar to the previous lesson).
• App.js: This file is the main component that will be rendered to the DOM, which currently includes the React logo image and the default text, that we see in the output.


# Let's have a Quiz.

Which of the following bundling tools does Create React App use?

- PackIt
- BundleJS
- Webpack
- Babel

Answer :- webpack

# ReactDOM.render 

Used to add the React application inside the element


# What is JSX? 

    ReactDOM.render(
    <h1>Hello, React!</h1>,
    document.getElementById('root')
    );

    We can use any JavaScript expression inside JSX using curly braces.

    const name = "David";
    const el = <p>Hello, {name}</p>;

    ReactDOM.render(
    el,
    document.getElementById('root')
    ); 

    Let's start to break down the code and understand each part of it.
    We will start with the <h1>Hello, React!</h1> element.

    As you can see, the element is not in quotes to represent a string. It's like an HTML element, however we use it right in the JavaScript code!
    This is called JSX, and it is a syntax extension to JavaScript. It allows us to build UI elements right in the JavaScript code!


#  How Does JSX Work? 

When the JSX expressions are compiled, they are converted into JavaScript objects, representing React elements.React then uses these elements to build the corresponding HTML DOM and display it in the browser.

# Virtual DOM 

We learned in the previous part that React updates only the elements that are necessary.This allows React apps to be much faster than apps built with other front-end technologie

- But how does React achieve that?

React uses a Virtual DOM, which is a lightweight representation of the DOM.When an element gets changed, it is first updated in the Virtual DOM. That process is fast, as the virtual DOM is represented by simple objects.After that, React compares the Virtual DOM to its previous state and only applies the DOM updates necessary to bring the DOM to the desired state.

# Components
 
Components let you split the page into independent and reusable parts.This makes organizing the page leaps and bounds easier, but even more importantly, components allow us as the developers to separate concerns from one another.


# Functional Components 

In React, there are two types of components that you can use: Functional Components and Class Components.

A functional component is a simple JavaScript function:

- Example 

    
        import React from 'react';
        import ReactDOM from 'react-dom';
        import Demo from './App';
        
        ReactDOM.render(
        <React.StrictMode>
            <Demo />
        </React.StrictMode>,
        document.getElementById('root')
        );


# Props 


Functional components can accept arguments, similar to JavaScript functions. These arguments are called props, and represent an object.

- Example 

    function Hello(props) {
         return <p>Hello, {props.name}!</p>;
    }

- Props in Class Components 

Props can be accessed in class components using this.props.

        class Hello extends React.Component {
        render() {
            return <p>Hello, {this.props.name}!</p>;
        }
        } 

# State 

Many web apps need their components to change their data, for example, after user interaction (clicking a button, submitting a form, etc.).
However, props cannot be changed.

- Changing State 

State should not be modified directly. Instead, React provides a setState() method, that can be used to modify state.

when setState is called, React automatically re-renders the affected component with the new state!


# Props vs State 

- We use props to pass data to components.
- Components use state to manage their data.
- Props are read-only and cannot be modified.
- State can be modified by its component using the setState() method.
- The setState() method results in re-rendering the component affected.


# Hooks 

Earlier version of React allowed to use state only with class components.
In recent iterations of React, a new feature called hooks was introduced, allowing to use state inside of functional components.

useState returns a pair, the current state value and a function, that lets you change the state.
useState takes one argument, which is the initial value of the state.

- Example 

    import React, { useState } from 'react'; 
    function Hello() {
    const [name, setName] = useState("David");

    return <h1>Hello {name}.</h1>;
    }

 we create a name state variable and a setName function. The square brackets syntax is called array destructuring. It assigns the name variable to the current state value, and setName to the function that allows to change the state. You can name these variables anything you like.


        function Counter() {
        const [counter, setCounter] = useState(0);

        function increment() {
            setCounter(counter+1);
        }

        return <div>
        <p>{counter}</p>
        <button onClick={increment}>
            Increment
        </button>
        </div>;
        } 

- Note : Hooks cannot be used in the class component.


# Lifecycle Methods 

Three life cycle method of the class are 

- componentDidMount : After rendered
- componentDidUpdate : once component gets updated
- componentWillUnmount :- Clean up code (While unmountig the component)


React provides special lifecycle methods for class components, which are called when components are mounted, updated or unmounted.

- Mounting :  is the process when a component is rendered on the page.The componentDidMount method is called when a component is rendered on the page.
    componentDidMount() {
    this.setState({counter: 42});
    }

componentDidMount is typically used for populating the state inside of a component when it initially mounts to the DOM.

- Unmounting : is the process when a component is removed from the page.Similarly, the componentWillUnmount() lifecycle method is called right before the component is removed from the DOM. It can be used to free up resources taken by the component.


- componentDidUpdate : Another lifecycle method is componentDidUpdate(), which is called when a component is updated in the DOM.componentDidUpdate() is only called when the component is updated

# useEffect  

The lifecycle methods we covered are only available for class components.
However, React provides a special Hook called useEffect to make lifecycle methods available in functional components. It combines the componentDidMount, componentDidUpdate, and componentWillUnmount methods into one.


        useEffect(() => {
        //do something
        }, [count]);  

Now, the useEffect() method will run only if count changes.

To mimic componentWillUnmount, useEffect may return a function that cleans up after it:

        useEffect(() => {
        // do something
        
        return () => {
            // cleanup
        }; 
        });

Just like with the useState hook, we need to import useEffect to be able to use it: import React, { useState, useEffect } from 'react';