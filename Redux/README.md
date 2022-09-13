
- Make you have installed packages redux ans react-redux to work with redux.

# What is Redux?



# Actions & Reducers

An action is just a plain JavaScript object:

    { 
    type: 'ADD_CONTACT', 
    name: 'James' 
    }

The code above defines an action with type ADD_CONTACT and a name property.

To tie the store and the action together, we need to write a function, called a reducer.

It takes state and action as arguments, and returns the next state of the app.

        function contactsApp(state, action) {
        if (action.type === 'ADD_CONTACT') {
            return [ ...state,  action.name ]
        } else {
            return state
        }
        }

The code above defines a simple reducer function, that checks the action and returns the new state.

These concepts are basically the idea of Redux: you hold the global state in a store, define actions to describe what to change in the store and write reducer functions to handle those actions.

# Actions 

Action can be viewed as payloads of information that send data to the store.
Actions are represented by simple JavaScript object and need to have a type property which defines the action name.

{
    type: 'ADD_CONTACT',
    payload: {
        name: "Jimmy Barnes"
    }
}
 

# Reducer Function 

- Reducers are functions that handle the actions. 
- The function takes the current state and the action as its parameters and returns the new state.

A reducer can handle multiple actions, so usually it includes a switch statement for each action case.

    function contactsApp(state, action) {
    switch (action.type) {
        case 'ADD_CONTACT':
        return [ ...state,  action.person ]
        default:
        return state
    }
    }

Note :- Remember, the reducer has to be a pure function, meaning it cannot modify the current state. It has to return a new state object instead. 

# Multiple Reducers 

If you have more than one entity (i.e. users, products, invoices, orders, etc.), it's typically a good idea to break them into multiple reducer functions to separate concerns.

Redux gives us a method that we can use called combineReducers. This allows us to use more than one reducer so that when an action gets dispatched, the action would get run through all of the reducers instead of only one. It also allows us to separate the concerns of our store state.

    const contactsApp = combineReducers({
    addContacts,
    doSomething
    })

# Redux with React 

- npm install redux  
- npm install react-redux 

The react-redux library binds React with Redux, allowing React components to read data from a Redux store, and dispatch actions to the store to update data.


# Counter App

First, we need to create our action and corresponding reducer.

    function incrementCounter(num) {
    return { 
        type: 'INCREMENT', 
        num: num 
    }
    }

The code above declares an action creator function named incrementCounter(), which returns an action with type INCREMENT and the corresponding payload.

- Our reducer: 

    const initialState = {
    count: 0
    };

    function reducer(state = initialState, action) {
    switch(action.type) {
        case 'INCREMENT':
        return { count: state.count + action.num };
        default:
        return state;
    }
    }

The code above defines a reducer function, which returns the new state based on the given action. We increment the count state variable by the provided num value.

# Creating the Store 

To create the store, we call the createStore() function, which takes the reducer as its parameter:

- const store = createStore(reducer); 

But how do we pass the store to our components?
That is achieved using a special <Provider> element. It makes the store available to any nested child component.


const el = <Provider store={store}>
    <Counter/>
  </Provider>; 
Provider takes the store as an attribute and makes it available to its child component.

We need to import { createStore } and { Provider } using the following syntax:
import { Provider } from 'react-redux';
import { createStore } from 'redux';

# Connecting to the Store

At this point, we have created our action, the reducer, the store, and made it available to our Counter component using the Provider element.


In order to connect our component to the store, we need to call the connect() function.
The connect() function returns a new component, that wraps the component you passed to it and connects it to the store using its special parameter functions. 

    function connect(mapStateToProps?, mapDispatchToProps?) 

mapStateToProps
This function is called every time the store state changes. It receives the state as a parameter and returns the state for the component.
For example, for our Counter, we need to return the count state variable:

    function mapStateToProps(state) {
    return {
        count: state.count
    };
    }


mapDispatchToProps
As you may have guessed from the name, this parameter is used to map the dispatch functions to props.
It can be a simple object, defining the function that needs to be mapped:
    const mapDispatchToProps = {
    incrementCounter
    }

This might seem a bit confusing, but its very straightforward: mapStateToProps simply returns the state variables as props to our component, while mapDispatchToProps allows to define how we dispatch actions and make the dispatching functions available as props.

Both are optional, as, for example, your component might only need to read from the store.

- Note :- that we need to import the connect function: import { connect } from 'react-redux';
# Store 

In Redux, the application's state is stored as a simple object, called store.
There should only be a single store in an app.

- Single source of truth
The global state of the app is stored in a single store.

- State is read-only 
You can change the state only by dispatching actions. Action are objects, that contain information about what should be changed.

- Pure reducers 
Reducers are functions that handle the actions and return the next state of the application. Reducers need to be pure, meaning they cannot modify the state, they need to return a new state object.