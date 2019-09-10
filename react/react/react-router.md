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



## Route Component

```javascript
<Route path='address rule' component={component that will be shown}
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

http://localhost:3000/about

![](https://i.postimg.cc/Px0W8mXC/React-router2.png)

Both the home and about components are visible because the `/about` path also matches the `/` rule.

To fix this, set the props called exact to true when you use Route component for Home.

```javascript
import React from 'react';
import { Route } from 'react-router-dom';
import Home from './pages/home/Home';
import About from './pages/about/About';

function App() {
  return (
    <div>
      <Route path='/' component={Home} exact={true} />
      <Route path='/about' component={About} />
    </div>
  );
}

export default App;
```

![](https://i.postimg.cc/Yq04w4MV/React-router3.png)



## Link Component

```javascript
<Link to='address'>contents</Link>
```



App.js

```javascript
import React from 'react';
import { Route, Link } from 'react-router-dom';
import Home from './pages/home/Home';
import About from './pages/about/About';

function App() {
  return (
    <div>
      <ul>
        <li>
          <Link to='/'>Home</Link>
        </li>
        <li>
          <Link to='/about'>About</Link>
        </li>
      </ul>
      <hr />
      <Route path='/' component={Home} exact={true} />
      <Route path='/about' component={About} />
    </div>
  );
}

export default App;
```

![](https://i.postimg.cc/xTNzzkhm/React-router4.png)



## Setting multiple paths in one route

Specifying multiple paths in one route feature has been applied since react-router v5.

Earlier versions used the following code to do this:

```javascript
import React from 'react';
import { Route, Link } from 'react-router-dom';
import Home from './pages/home/Home';
import About from './pages/about/About';

function App() {
  return (
    <div>
      <ul>
        <li>
          <Link to='/'>Home</Link>
        </li>
        <li>
          <Link to='/about'>About</Link>
        </li>
      </ul>
      <hr />
      <Route path='/' component={Home} exact={true} />
      <Route path='/about' component={About} />
      <Route path='/info' component={About} />
    </div>
  );
}

export default App;
```



Since v5, the following code is used:

```javascript
<Route path={['/about', '/info']} component={About} />
```



## URL parameter and query

Sometimes you need to pass floating values when defining page addresses. It can be divided into parameters and queries.

* Parameter: /profiles/**woochul**
* Query: /about?**details=true**

There are no rules when deciding whether to use parameters or queries when you need to use floating values. In general, parameters are used to searching a specific ID or name, and a query is used when we search for a keyword or pass options that are needed for a page.



### URL parameter

On the profile page, when the user enters a floating username in the form of `/profile /woochul` at the end, you can get username as a props.

App.js

```javascript
import React from 'react';
import { Route, Link } from 'react-router-dom';
import Home from './pages/home/Home';
import About from './pages/about/About';
import Profile from './pages/profile/Profile';

function App() {
  return (
    <div>
      <ul>
        <li>
          <Link to='/'>Home</Link>
        </li>
        <li>
          <Link to='/about'>About</Link>
        </li>
        <li>
          <Link to='/profile/woochul'>Woochul</Link>
        </li>
        <li>
          <Link to='/profile/gildong'>Gildong</Link>
        </li>
      </ul>
      <hr />
      <Route path='/' component={Home} exact={true} />
      <Route path={['/about', '/info']} component={About} />
      <Route path='/profile/:username' component={Profile} />
    </div>
  );
}

export default App;
```



Profile.js

```javascript
import React from 'react';

const data = {
  woochul: {
    name: 'Woochul Hyun',
    description: 'Hello'
  },
  gildong: {
    name: 'Gildong Hong',
    description: 'Hi'
  }
};

const Profile = ({ match }) => {
  const { username } = match.params;
  const profile = data[username];

  if (!profile) {
    return <div>User does not exist</div>;
  }

  return (
    <div>
      <h3>
        {username}({profile.name})
      </h3>
      <p>{profile.description}</p>
    </div>
  );
};

export default Profile;
```

![](https://i.postimg.cc/MGbSr835/React-router5.png)



### URL Query





