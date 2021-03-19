# React Refresher Notes/Cheat Sheet

Developed by Facebook to upgrade codebases/architecture (there was a need for it as websites became more complex and bugs became more prevalent in code). React was released to the developer community in 2013. Documentation [here](https://reactjs.org/).

<details><summary>Highlights of React</summary>
  
#### 1. DOM Manipulation

The DOM (Document Object Model) is used to display websites through JavaScript (vanilla JS uses imperative style). <strong>Imperative</strong> style directly performs an action for each and every part of an app in response to various user events. The developer must explicitly state each step of how something should be done in order to <strong>repaint</strong> (change an element and add it onto a page) and <strong>reflow</strong> (recalculate layout of the page). This makes it difficult to see relationships between events as the page flow/layout becomes more complex. In React, declarative style is used, instead. <strong>Declarative</strong> style holds the state (data) which allows React to find the best way to manipulate the DOM to load that information. The different states are accounted for in one place which means cleaner and more efficient code quality, as well as faster load time. 

#### 2. Component Architecture

React works heavily with reusable components that can be copied over to various areas on a page or even into other projects. Small components are built and added together to make larger ones. Components are created as JavaScript functions that receive a prop (attribute) and returns something that <em>looks like</em> HTML called JSX. Each component has one "job" and does it well.

#### 3. Data Flow

React follows a <strong>unilateral</strong> data flow from top to bottom which makes it easier to debug code. It creates a virtual DOM that is a treelike object which gives React the ability to look at the blueprint of what needs to be built and modifies the DOM for us. Any time the state (data) changes, React intercepts that and updates the DOM as needed.

#### 4. Library

React only focuses on the <strong>UI (user-interface)</strong> which is why it is considered a <strong>library</strong> rather than a framework. Frameworks give developers all the tools necessary to build an application, whereas libraries provide the core of some functionality (React provides the UI). With React, other modules/libraries can be used to mix and match and customized as needed. React doesn't make assumptions on the tech stack being used, and so it also has cross-platform interactivity (e.g. React Native, React360).
</details>
<details><summary>Class-based Components</summary>

Both functions and classes can be written to return HTML. Class-based components in React have many functionality in them.

##### General Syntax
```
class App extends Component {
  render() {
    return (
    // any JSX (HTML-like syntax in React)
    );
  }
}
```
By using class, there is now access to state. <strong>State</strong> is an object with properties that can be accessed at any point inside class. To access state, call a constructor. This allows us to use this state as many times as possible. 

##### Access State with Class
```
class App extends Component {
  constructor() {
    super();
    
    this.state = {
      // any form of state object
      name: 'Example'
    };
  }

  render() {
    return (
      // render the state from class
      <p>{this.state.name}</p>
      // when user clicks the button, the text above will change based on what is declared in state
      // note that anything inside {} is a JS expression
      <button onClick={() => this.setState({ string: 'Different example' })}>Click me</button>
    )
  }
}
```

Keep in mind that since React follows unilateral data flow, when the state changes, it re-renders the component to display the change.
</details>

<details><summary>Functional Components</summary>

Functional components are simply JavaScript functions. 

##### General Syntax
```
function App() {
  return (
    <div>
      <p>Hi</p>
    </div>
  );
}
```

Components take in props (properties that are passed into the component and come out as objects). Children are anything in between tags.

```
<div> {props.child} </div>
```
#### State vs Props
Specific state lives in one location and trickles down as props. Props are pieces of data passed into a child component from the parent while state is data controlled within a component. This is why state is mutable while props are immutable.

![](https://www.techdiagonal.com/wp-content/uploads/2019/09/react-props-blog-image-design-2.jpg)
</details>

<details><summary>Life Cycle Methods</summary>
  
Various life cycle methods serve different purposes and are triggered at different times in a component's lifecycle. See diagram [here](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/). 

#### Mounting
##### componentDidMount(): constructor → render → DOM & refs updates → componentDidMount
This is the phase when components are put on the DOM for the first time (inserted into the tree). Before a life cycle method is called, React first calls the constructor which is where the super()(a method on the class inside the constructor) is located. The super() will pull in all methods and functionality from whatever it is extending (allows class component to have access to all other life cycle components. Inside the constructor, when this.state is called, state is initialized on the class (helpful for other life cycle components that may need state).

```
class componentName extends React.Component {
  constructor() {
    super();
  }
  // components here
}
```

After the state is called, the render method is called. The component tells JavaScript what to display as HTML. Any prop values are evaluated in the HTML at this point, too. Then, React updates the DOM and the component is mounted as a base class component. Finally, the componentDidMount() is called which is when we do things like API calls.

```
componentDidMount() {
  
}
```

#### Updating
##### componentDidUpdate(): New props, setState(), forceUpdate() → render → DOM & refs updates → componentDidUpdate
Any future updates to the props, state, or manual force update on the component will cause the component to go into the updating phase without the need to remount anything. This is because no new elements are needed. Instead, React efficiently makes selective changes to pieces of HTML in the component. Then, React updates the DOM with required changes. Finally, componentDidUpdate() gets called. This is used as an opportunity to operate on the DOM (e.g. network requests).

```
componentDidUpdate() {
  
}
```

##### shouldComponentUpdate(): New props, setState(), forceUpdate() → shouldComponentUpdate → render → DOM & refs updates → componentDidUpdate
This determines whether or not an entire chain of updates need to occur and exists between first part of the phase and render phase. React gets the nextProps and nextState and based on these props/states, it determines whether or not the DOM should be re-rendered. If it returns true, then the DOM will render and the component will update. If it returns false, React won't go through any additional phases of the life cycle method.

This a fundamental part of performance optimization of the application and when we should do what with our components. 

```
shouldComponentUpdate(nextProps, nextState) {
  // if you want re-render
  return true;
  // if you do not want re-render
  return false;
  // if you want to manual force compare if the text is the same between props
  return nextProps.text !== this.props.text;
}
```

#### Unmounting
##### componentWillUnmount(): componentWillUnmount
The component will unmount when it gets called and this life cycle method provides an opportunity for us to do anything before React strips the component off the DOM. This occurs when any re-rendering happens so that React can unmount anything that is no longer being used. Hency why it will no longer exist in the DOM. Perform any necessary cleanup in this method, such as invalidating timers, canceling network requests, or cleaning up any subscriptions that were created in componentDidMount().

```
componentWillUnmount() {
  
}
```
</details>

<details><summary>React Router DOM</summary>
React builds a Single Page Application (SPA) where a web app loads a single page and dynamically updates that page as the user interacts with it. React allows us to pick and choose our own routing for SPA. Routing is the ability to move between different parts of an application when a user enters a URL or clicks an element (link, button, icon, image etc) within the application. React allows you to choose your own router, but one of the most popular variants is <em>react-router-dom</em>.
  
```
react-router-dom: a variant of the core library meant to be used for web applications, especially for those that have several pages that need to be rendered.
```

The react-router package includes a number of routers that we can take advantage of depending on the platform we are targeting. These include <strong>BrowserRouter</strong>, <strong>HashRouter</strong>, and <strong>MemoryRouter</strong>. Its imports used for routing essentially look for changes in the state and render a whole new component on a completely different URL with efficiency without reloading.

#### The BrowserRouter is used for applications which have a dynamic server that knows how to handle any type of URL whereas the HashRouter is used for static websites with a server that only responds to requests for files that it knows about.

### History
Each router creates a history object that it uses to keep track of the current location and re-renders the application whenever this location changes. For this reason, the other React Router components rely on this history object being present; which is why they need to be rendered inside a router.
The BrowserRouter uses the HTML5 history API to keep the user interface in sync with the URL in the browser address bar.

### Routes
The <Route/> component renders the appropriate user interface when the current location matches the route’s path. The path is a prop on the <Route/> component that describes the pathname that the route should match.

### Switch
The react-router library also contains a <Switch/> component that is used to wrap multiple <Route/> components. The Switch component only picks the first matching route among all its children routes.

![](https://miro.medium.com/max/500/1*nfOoDEzgO6Gf_X8o-D8MAw.png)

Read more [here](https://medium.com/the-andela-way/understanding-the-fundamentals-of-routing-in-react-b29f806b157e).
</details>

<details><summary>Higher Order Component</summary>

</details>

<details><summary>Next Topic</summary>

#### 
</details>

<details><summary>Cheat Sheet Definitions</summary>

#### [Life Cycle Methods](https://reactjs.org/docs/glossary.html#lifecycle-methods)
Life cycle methods (used with classes) get called at different stages of when built-in React components gets rendered. In life cycle methods, React renders the component on the page and when it does that, it calls the block of code inside the function.

#### [React Events](https://reactjs.org/docs/handling-events.html#:~:text=React%20events%20are%20named%20using%20camelCase%2C%20rather%20than,the%20HTML%3A%20%3Cbutton%20onclick%3D%22activateLasers%20%28%29%22%3E%20Activate%20Lasers%20%3C%2Fbutton%3E)
React handles changes through the DOM for you at the most optimal time to update the DOM. Event handlers occur through JSX as synthetic events (identified by its camelCasing rather than lowercase). With JSX, you pass a function as the event handler rather than a string. React intercepts the event handler and looks for what it needs to do next. 

#### [Asynchronous setState](https://reactjs.org/docs/faq-state.html#what-does-setstate-do)
setState() schedules an update to a component’s state object (batches multiple setState()). When state changes, the component responds by re-rendering. setState is asynchronous inside event handlers. This ensures that if both Parent and Child call setState during a click event, Child isn’t re-rendered twice. Instead, React “flushes” the state updates at the end of the browser event. This results in significant performance improvements in larger apps. This is an implementation detail, so avoid relying on it directly.
</details>
