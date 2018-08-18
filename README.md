# React jsx-data-binding

### Install
~~~~
$ yarn global add live-server  --> install live-server
$ live-server -v   --> verify version
~~~~

Now attach your folder having index.html
~~~~
$ live-server public
~~~~

Install Babel
~~~~
$ npm install -g babel-cli@6.24.1
$ babel --help
$ yarn init   //This creates package.json
~~~~

Add React and ENV preset
~~~~
$ yarn add babel-preset-react@6.24.1 babel-preset-env@1.5.2
~~~~

Realtime Compile JSX into JS
~~~~
$ babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch
~~~~

### Description
when you render elementCount it is displaying data "Count".. When the user clicks on +1 button the count would be incremented but the Count data on the browser does not change…????
~~~~
let count = 0
const addOne = () => ++count
const minusOne = () => --count
const resetCount = () => count = 0

const elementCount = (
    <div>
        <h1>Count: {count}</h1>
        <button onClick={addOne}>+1</button>
        <button onClick={minusOne}>-1</button>
        <button onClick={resetCount}>reset</button>
    </div>
);

const appRoot = document.getElementById('app') 
ReactDOM.render(elementCount, appRoot)
~~~~

> This is because JSX do not have any build in Data Binding

elementCount would resolve to an object with count value as 0… 
ReactDOM.render would then render elementCount with count 0… 
When the button is clicked the count value changes but then elementCount needs to be regenerated and ReactDOM.render needs to be called again…


You can extract elementCount and ReactDOM.render into a function and call it everytime you want to re-render

### Is this HORRIBLE??? 
Since we are re rendering the app (DOM) so many times…??? 
> Answer is NOOOOOOO...

React uses virtual DOM algorithm to identify minimal changes that needs to be made to render the application…

Go to the the Dev tools -> Elements and click on +1 and -1… 
element that flashes is the one that is changed / rendered… you will notice only the count is changed and no other components (button, H1 Count etc) was impacted… 
It basically compares the elementCount (which represent JavaScript) prior with current and learns about the changes…
