# React-router

## Installation

There are several react routing libraries such as react-router, reach-router, Next.js, etc. Here, we are going to use react-router here. We need to download the library first.

```javascript
npm i react-router-dom
yarn add react-router-dom
```



## Apply a router to project

When you apply react router to your project, you use a component called BrowserRouter that is built-in react-router-dom in the src/index.js file. This component uses HTML5's History API for web applications to allow you to change addresses without having to refresh and easily search or use information related to the current address with props.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);

serviceWorker.unregister();
```



## Pages

Home.js

```javascript
import React from 'react';

const Home = () => {
  return (
    <div>
      <h1>Home</h1>
      <p>Main page</p>
    </div>
  );
};

export default Home;
```



About.js

```javascript
import React from 'react';

const About = () => {
  return (
    <div>
      <h1>About</h1>
      <p>About page</p>
    </div>
  );
};

export default About;
```



## Route to specific addresses with the Route component

```javascript
<Route path='address' component={component that will be shown}
```



App.js

```javascript
import React from 'react';
import { Route } from 'react-router-dom';
import Home from './pages/home/Home';
import About from './pages/about/About';

function App() {
  return (
    <div>
      <Route path='/' component={Home} />
      <Route path='/about' component={About} />
    </div>
  );
}

export default App;
```



http://localhost:3000/

![](https://i.postimg.cc/cJn3fpPm/React-router1.png)



