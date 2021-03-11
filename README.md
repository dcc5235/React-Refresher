# React Refresher Notes/Cheat Sheet

Developed by Facebook to upgrade codebases/architecture (there was a need for it as websites became more complex and bugs became more prevalent in code). React was released to the developer community in 2013. Documentation [here](https://reactjs.org/).

<details><summary>Highlights of React</summary>
  
#### 1. DOM Manipulation

The DOM (Document Object Model) is used to display websites through JavaScript (vanilla JS uses imperative style). <strong>Imperative</strong> style directly performs an action for each and every part of an app in response to various user events. The developer must explicitly state each step of how something should be done in order to <strong>repaint</strong> (change an element and add it onto a page) and <strong>reflow</strong> (recalculate layout of the page). This makes it difficult to see relationships between events as the page flow/layout becomes more complex. In React, declarative style is used, instead. <strong>Declarative</strong> style holds the state (data) which allows React to find the best way to manipulate the DOM to load that information. The different states are accounted for in one place which means cleaner and more efficient code quality, as well as faster load time. 

#### 2. Component Architecture

React works heavily with reusable components that can be copied over to various areas on a page or even into other projects. Small components are built and added together to make larger ones. Components are created as JavaScript functions that receive a prop (attribute) and returns something that <em>looks like</em> HTML but is called JSX.

#### 3. Data Flow

React follows a <strong>unilateral</strong> data flow from top to bottom which makes it easier to debug code. It creates a virtual DOM that is a treelike object which gives React the ability to look at the blueprint of what needs to be built and modifies the DOM for us. Any time the state (data) changes, React intercepts that and updates the DOM as needed.

#### 4. Library

React only focuses on the <strong>UI (user-interface)</strong> which is why it is considered a <strong>library</strong> rather than a framework. Frameworks give developers all the tools necessary to build an application, whereas libraries provide the core of some functionality (React provides the UI). With React, other modules/libraries can be used to mix and match and customized as needed. React doesn't make assumptions on the tech stack being used, and so it also has cross-platform interactivity (e.g. React Native, React360).
</details>
<details><summary>Next Topic</summary>

#### 
</details>

</details>
<details><summary>Next Topic</summary>

#### 
</details>
