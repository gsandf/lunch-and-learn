# React Native & Expo

---

## Intro to React Native

- What is React Native?
- How is it different from web?
- How does it compare to alternatives?
- Of course, we&rsquo;ll make an app

---

## What is React Native?

- React
- for native (who knew?) <!-- .element: class="fragment" -->
- some abstractions <!-- .element: class="fragment" -->
- some common components <!-- .element: class="fragment" -->

+++

### But what is it

> I thought you were going to tell us something useful

+++

### Let&rsquo;s start with React

- React doesn&rsquo;t have the concept of a browser
- It handles creating components, sending props to children, etc.
- &ldquo;Doing stuff&rdquo; with components is the renderer&rsquo;s job (e.g. [`react-dom`](https://reactjs.org/docs/react-dom.html), [`react-native`](https://github.com/facebook/react-native), etc.)

+++

### React components

- state & props
- `propTypes` & `defaultProps`
- `render()`
- `componentDidMount()`
- [other less-frequently used methods](https://reactjs.org/docs/react-component.html)

Note:
At first, JSX seems like magic.  I don't like magic in code.  Plus, I just generally do better with something when I know what's really going on.  So let's demystify JSX and see how React can interact with web, native, and other renderers.

+++

### Types of React components

- functional
- class

+++

### Functional component

```javascript
import React, { PropTypes } from 'react'

// Functional components do not have other lifecycle methods or state.  They are
// simply a function.  An easy way to think about this is whatever is returned
// will be shown on the screen.
const Gradient = ({ deg = 0, from, to, style }) =>
  <div
    style={{
      backgroundImage: `linear-gradient(${deg}deg, ${from}, ${to})`,
      ...style
    }}
  />

export default Gradient
```

+++

### Class component

```javascript
import React, { Component } from 'react'
import getLocation from './get-location'

class DailyForecast extends Component {
  // Unlike functional components, class components can use state.
  // This can make them more difficult to test and predict.  We generally try to
  // abstract as much as possible out of these.
  state = {
    loading: true,
    dailyWeather: null
  }

  // This is the syntax for functions you would add to classes.  Notice below in
  // `componentDidMount` that it calls `this.fetchWeather()`.
  async fetchWeather() {
    const { latitude, longitude } = await getLocation()
    const response = await fetch(
      `https://api.weather.gov/points/${latitude},${longitude}/forecast`
    )
    const data = await response.json()

    // To update state, use `this.setState()`
    // The argument can either be an object or a function that returns an
    // object.  The object will extend (as opposed to replace) the current
    // state.
    this.setState({
      dailyWeather: data.properties.periods,
      loading: false
    })
  }

  // This is a lifecycle method.  `componentDidMount` is most commonly used to
  // make asynchronous changes (for example, making a network request).
  // See here for more details:
  // https://reactjs.org/docs/react-component.html
  componentDidMount() {
    this.fetchWeather()
  }

  // This is a lifecycle method.  An easy way to think about this is whatever is
  // returned here will be shown on the screen.
  render() {
    const { dailyWeather, loading } = this.state

    if (loading) {
      return <div>Loading...</div>
    }

    return (
      <div>
        {dailyWeather.map(forecast =>
          <div>
            <h2>
              {forecast.name}
            </h2>
            <p>
              {forecast.detailedForecast}
            </p>
          </div>
        )}
      </div>
    )
  }
}

export default DailyForecast
```

+++

### Demystify the Syntax

JSX turns this:

```javascript
const MyCoolThing = () => (
  <div className="cool" aNumber={42}>
    Hello!
  </div>
)
```

into [this](https://babeljs.io/repl/#?babili=false&browsers=&build=&builtIns=false&code_lz=MYewdgzgLgBAsgTwMIhAGwCoAsCWYDmMAvDABQCUxAfGQFAwwA8AJjgG4zBoCGEEActwC2AUyIAiUOnExu_AK5CARiIBORAN4AWAEwBfKvQYwAEiLRoQAQiOMA9KzaHyQA&debug=false&circleciRepo=&evaluate=false&lineWrap=true&presets=es2015%2Creact%2Cstage-2&targets=&version=6.26.0):

```javascript
var MyCoolThing = function MyCoolThing() {
  return React.createElement(
    "div",
    { className: "cool", aNumber: 42 },
    "Hello!"
  );
};
```

+++

### React for native components

- Same underlying concepts as writing for browser
- Instead of rendering DOM elements, renders native elements
- `<div> => <View>`

+++

### Abstractions from RN

- `Animated`
- `CameraRoll`
- `Geolocation`
- `StatusBar`
- `StyleSheet`
- [many more](https://facebook.github.io/react-native/docs/getting-started.html)

Note:
- Native code doesn't know CSS.  That means we can't use CSS keyframes CSS transitions with native views, so we have `Animated`.
- `Animated` gives us both easing & spring animations.
- `Animated` handles putting animations on another thread.
- Probably the most powerful abstraction is `StyleSheet`.  It would be painful to do styling without this.
- For example, [`styled-components` uses `StyleSheet`](https://github.com/styled-components/styled-components/blob/master/src/native/index.js#L17).

+++

### Components from RN

- `FlatList` & `SectionList`
- `Image`
- `KeyboardAvoidingView`
- `RefreshControl`
- `View` & `ScrollView`
- `WebView`
- [many more](https://facebook.github.io/react-native/docs/getting-started.html)

---

## React Native vs. web

+++

### General differences

- different components
- files loaded differently
- some functions not built-in or must be supplied
  * `atob()`, `btoa()`, `navigator.*`, `document.*`
- must use `fetch` to make network requests
- native components have to be compiled and linked
- styling quite different&hellip;

+++

### Styling differences

- relies on `StyleSheet` abstraction
- no keyframes
- no CSS transitions
- no `text-transform`
- `Animated` library & `transform` can be used for animations

---

## Alternatives

**Alternatives:**

- Native
- Cordova, PhoneGap, Ionic
- PWA

+++

### Native

**PROS:**

- Full access to system APIs
- Result is fast (great for animation-heavy applications)

**CONS:**

- Require separate resources for each platform
- Time-consuming to create
- Have to maintain a different code base for each platform
- Requires setting up build tools for each platform

Note:
Think about this: Facebook, Instagram, Airbnb, Walmart, and Tesla all are transitioning away from full-native because it&rsquo;s not as profitable for them.  If they—who have access to the best-of-the-best app engineers—have found it better to move away from native because the cost (time/money/people), how much more should we be moving away from that?

+++

### Cordova - what is it?

- **Cordova** was made by Apache.
- Adobe took it and &ldquo;created&rdquo; **PhoneGap** by using the exact same codebase and adding no known value.
- **Ionic** is essentially an Angular + UI starter kit for Cordova.

+++

### Cordova

**PROS:**

- Single code base
- Fairly quick to create
- Some access to system APIs

**CONS:**

- App can be sluggish
- Access to APIs relies on plugins that seem mostly unmaintained
- Can be difficult to take advantage of platform-specific features
- Requires setting up build tools for each platform

+++

### PWA

**PROS:**

- Very quick to create
- Single code base
- Can distribute application to non-mobile devices
- No need to install platform build tools

**CONS:**

- _Extremely_ limited access to system APIs
- App can be sluggish for intensive interactions
- Not as fashionable to some teams
- iOS doesn&rsquo;t support service workers

+++

### React Native

**PROS:**

- Quick to create
- Single code base
- No need to install platform build tools (if using Expo)
- Access to most system APIs built-in
- Great ecosystem for other functionality
- Result is fast

**CONS:**

- It&rsquo;s different
- Styling and debugging can be more difficult than web
- Requires setting up build tools for each platform (if not using Expo)

+++

## Best fits

- Native
  * _Extremely_ performance-critical app
- Cordova, PhoneGap, Ionic
  * Put a website with native plugins for app stores
  * Would be good option for shops that don&rsquo;t have JS devs
- PWA
  * Most everything that don&rsquo;t need native functionality
- React Native
  * Most everything that does need native functionality

---

## Expo

+++

### Expo vs. React Native

- Expo is like a subset of RN
- handles some of the hard things
  * no Xcode/Android Studio
  * develop on Windows/Linux/macOS
  * instant updates
  * snazzy barcode
- limited in native code to what&rsquo;s provided by Expo

+++

### Expo limitations

- no external native modules
- external assets are served over CDN (+/-)
- background execution limited
- limited to Expo push notification servers

+++

### Expo features

- Barcode scanner
- Camera
- Contacts
- Fingerprint
- Location
- MapView
- Payments
- [lots more](https://docs.expo.io/versions/latest/index.html)

+++

### Snack

[https://snack.expo.io](https://snack.expo.io)
