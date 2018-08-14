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

---

### But what is it

> I thought you were going to tell us something useful

---

### Let&rsquo;s start with React

- React doesn&rsquo;t have the concept of a browser
- It handles creating components, sending props to children, etc.
- &ldquo;Doing stuff&rdquo; with components is the renderer&rsquo;s job (e.g. [`react-dom`](https://reactjs.org/docs/react-dom.html), [`react-native`](https://github.com/facebook/react-native), etc.)

---

### React for native components

- Same underlying concepts as writing for browser
- Instead of rendering DOM elements, renders native elements
- `<div> => <View>`

---

### Abstractions from RN

- `Animated`
- `CameraRoll`
- `Geolocation`
- `StatusBar`
- `StyleSheet`
- [many more](https://facebook.github.io/react-native/docs/getting-started.html)

Note:

- Native code doesn't know CSS. That means we can't use CSS keyframes CSS transitions with native views, so we have `Animated`.
- `Animated` gives us both easing & spring animations.
- `Animated` handles putting animations on another thread.
- Probably the most powerful abstraction is `StyleSheet`. It would be painful to do styling without this.
- For example, [`styled-components` uses `StyleSheet`](https://github.com/styled-components/styled-components/blob/master/src/native/index.js#L17).

---

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

---

### General differences

- different components
- files loaded differently
- some functions not built-in or must be supplied
  - `atob()`, `btoa()`, `navigator.*`, `document.*`
- native components have to be compiled and linked
- styling quite different&hellip;

---

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

---

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
Think about this: Facebook, Instagram, Airbnb, Walmart, and Tesla all are transitioning away from full-native because it&rsquo;s not as profitable for them. If they—who have access to the best-of-the-best app engineers—have found it better to move away from native because the cost (time/money/people), how much more should we be moving away from that?

---

### Cordova - what is it?

- **Cordova** was made by Apache.
- Adobe took it and &ldquo;created&rdquo; **PhoneGap** by using the exact same codebase and adding no known value.
- **Ionic** is essentially an Angular + UI starter kit for Cordova.

---

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

---

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

---

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

---

## Best fits

- Native
  - _Extremely_ performance-critical app
- Cordova, PhoneGap, Ionic
  - Put a website with native plugins for app stores
  - Would be good option for shops that don&rsquo;t have JS devs
- PWA
  - Most everything that don&rsquo;t need native functionality
- React Native
  - Most everything that does need native functionality

---

## Expo

---

### Expo vs. React Native

- Expo is like a subset of RN
- handles some of the hard things
  - no Xcode/Android Studio
  - develop on Windows/Linux/macOS
  - instant updates
- limited in native code to what&rsquo;s provided by Expo

---

### Expo limitations

- no external native modules
- external assets are served over CDN (+/-)
- background execution limited
- limited to Expo push notification servers

---

### Expo features

- Barcode scanner
- Camera
- Contacts
- Fingerprint
- Location
- MapView
- Payments
- [lots more](https://docs.expo.io/versions/latest/index.html)

---

### Snack

[https://snack.expo.io](https://snack.expo.io)
