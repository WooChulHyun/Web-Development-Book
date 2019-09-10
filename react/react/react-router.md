# React-router

## Installation

There are several react routing libraries such as react-router, reach-router, Next.js, etc. Here, we are going to use react-router here. We need to download the library first.

```bash
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

The query can be retrieved from the `search` value contained in the location object. The location object is passed as props to the component used as a route and contains information about the current address of the web application.

Form of location:

```javascript
{
  "pathname": "/about",
  "search": "?detail=true",
  "hash": ""
}
```

The location object above is when you enter http://localhost: 3000/about?detail=true. To read a specific value from the search value, this string must be converted to an object.

When converting query strings to objects, you use a library called qs.

```bash
npm i qs
yarn add qs
```



About.js

```javascript
import React from 'react';
import qs from 'qs'

const About = ({location}) => {
  const query = qs.parse(location.search, {
    ignoreQueryPrefix: true
  })

const showDetail = query.detail === 'true'
  return (
    <div>
      <h1>About</h1>
      <p>About page</p>
      {showDetail && <p>detail value is set as true</p>}
    </div>
  );
};

export default About;
```



## Sub route

A sub route is defines a route inside a route. To do this, just use the Route component again inside the component that is being used as the route.

App.js

```javascript
import React from 'react';
import { Route, Link } from 'react-router-dom';
import Home from './pages/home/Home';
import About from './pages/about/About';
import Profiles from './pages/profiles/Profiles';

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
          <Link to='/profiles'>Profils</Link>
        </li>
      </ul>
      <hr />
      <Route path='/' component={Home} exact={true} />
      <Route path={['/about', '/info']} component={About} />
      <Route path='/profiles' component={Profiles} />
    </div>
  );
}

export default App;
```



Profiles.js \(not Profile.js\)

```javascript
import React from 'react';
import { Route, Link } from 'react-router-dom';
import Profile from '../profile/Profile';

const Profiles = () => {
  return (
    <div>
      <h3>User List:</h3>
      <ul>
        <li>
          <Link to='/profiles/woochul'>Woochul</Link>
        </li>
        <li>
          <Link to='/profiles/gildong'>Gildong</Link>
        </li>
      </ul>
      <Route path='/profiles' exact render={() => <div>Choose user</div>} />
      <Route path='/profiles/:username' component={Profile} />
    </div>
  );
};

export default Profiles;
```

![](https://i.postimg.cc/vBQBsxXx/React-router6.png)



## history

```javascript
import React from 'react';

const History = ({ history }) => {
  const back = () => {
    history.goBack();
  };

  const home = () => {
    history.push('/');
  };

  return (
    <div>
      <button onClick={back}>back</button>
      <button onClick={home}>Home</button>
    </div>
  );
};

export default History;
```



## withRouter

The withRouter function is a higher-order component \(HoC\). This allows access to match, location, and history objects even if they are not components used as routes.

WithRouterExample.js

```javascript
import React from 'react';
import { withRouter } from 'react-router-dom';

const WithRouterExample = ({ location, match, history }) => {
  return (
    <div>
      <h4>Location</h4>
      <textarea
        value={JSON.stringify(location, null, 2)}
        rows={7}
        readOnly={true}
      ></textarea>
      <h4>Match</h4>
      <textarea
        value={JSON.stringify(match, null, 2)}
        rows={7}
        readOnly={true}
      ></textarea>
    </div>
  );
};

export default withRouter(WithRouterExample);
```



Profiles.js

```javascript
import React from 'react';
import { Route, Link } from 'react-router-dom';
import Profile from '../profile/Profile';
import WithRouterExample from '../withRouter/WithRouterExample';

const Profiles = () => {
  return (
    <div>
      <h3>User List:</h3>
      <ul>
        <li>
          <Link to='/profiles/woochul'>Woochul</Link>
        </li>
        <li>
          <Link to='/profiles/gildong'>Gildong</Link>
        </li>
      </ul>
      <Route path='/profiles' exact render={() => <div>Choose user</div>} />
      <Route path='/profiles/:username' component={Profile} />
      <WithRouterExample />
    </div>
  );
};

export default Profiles;
```

![](https://i.postimg.cc/fT535N7f/React-router7.png)



If you look at the match object here, params is empty. withRouter, a match is passed based on the route component \(current Profiles\) that is currently showing itself. When setting up a route for Profiles, we only type path="/profiles" so we cannot read the username parameter.

If you remove the WithRouterExample component from Profiles and put it in the Profile component, you will see the URL parameter in the match.

Profile.js

```javascript
import React from 'react';
import WithRouterExample from '../withRouter/WithRouterExample';

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
      <WithRouterExample />
    </div>
  );
};

export default Profile;
```

![](https://i.postimg.cc/GpnxnRNT/React-router8.png)



## Switch

The Switch component wraps multiple routes and renders only one matching route. Switch also allows you to implement a Not Found page that will be shown when all rules do not match.

App.js

```javascript
import React from 'react';
import { Route, Link, Switch } from 'react-router-dom';
import Home from './pages/home/Home';
import About from './pages/about/About';
import Profiles from './pages/profiles/Profiles';
import History from './pages/history/History';

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
          <Link to='/profiles'>Profils</Link>
        </li>
        <li>
          <Link to='/history'>History</Link>
        </li>
      </ul>
      <hr />
      <Switch>
        <Route path='/' component={Home} exact={true} />
        <Route path={['/about', '/info']} component={About} />
        <Route path='/profiles' component={Profiles} />
        <Route path='/history' component={History} />
        <Route
          render={({ location }) => (
            <div>
              <h2>Page Not Found</h2>
              <p>{location.pathname}</p>
            </div>
          )}
        />
      </Switch>
    </div>
  );
}

export default App;
```

![](https://i.postimg.cc/2SYh6GkV/React-router9.png)



## NavLink

