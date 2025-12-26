---
title: "Mastering React Router: Navigation, Routing, and Hooks in React"
datePublished: Fri Dec 26 2025 15:37:41 GMT+0000 (Coordinated Universal Time)
cuid: cmjn1cji1000802jpayzp2abq
slug: mastering-react-router-navigation-routing-and-hooks-in-react
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1766763386305/c7259a7e-b4ae-4578-95a4-21e366cd4ccf.png
tags: react-router, javascript, reactjs, react-router-dom, reacthooks

---

React applications often require multiple pages or views, but unlike traditional web apps, React uses Single Page Applications (SPAs). In SPAs, content changes dynamically without refreshing the entire page. React Router is the most popular library in React to handle this navigation smoothly.

This article will guide you through everything you need to know about React Router, React Router DOM, types of routers, dynamic routing, hooks, and navigation components.

---

### What is React Router?

**React Router** is a library that enables **navigation and routing** in React applications, allowing you to build multi-view applications without full page reloads. It is essential for creating **Single Page Applications (SPAs)** with multiple screens or “pages.”

**<mark>Key Features</mark>**

1. **Declarative Routing**
    
    * You define routes in your JSX using `<Routes>` and `<Route>` components.
        
    * React Router automatically renders the correct component based on the URL.
        
    
    ```javascript
    import { Routes, Route } from "react-router-dom";
    import Home from "./Home";
    import About from "./About";
    
    function App() {
        return (
            <Routes>
                <Route path="/" element={<Home />} />
                <Route path="/about" element={<About />} />
            </Routes>
        );
    }
    ```
    
2. **Nested Routes**
    
    * Routes can be **nested** inside other routes for hierarchical layouts.
        
3. **Dynamic Routing**
    
    * Routes can include **parameters** to render dynamic content.
        
    
    ```javascript
    <Route path="/user/:id" element={<UserProfile />} />
    ```
    
4. **Programmatic Navigation**
    
    * You can navigate using hooks like `useNavigate()` instead of `<Link>`.
        
    
    ```javascript
    import { useNavigate } from "react-router-dom";
    
    function Home() {
        const navigate = useNavigate();
        return <button onClick={() => navigate("/about")}>Go to About</button>;
    }
    ```
    
5. **TypeScript Support**
    
    * React Router supports TypeScript for type-safe routes and props.
        

---

## Types of React Routers

React offers several routers depending on the environment:

### 1\. BrowserRouter

* Uses the HTML5 History API (`pushState`, `replaceState`) to manage URLs.
    
* Creates clean URLs without `#`.
    
* Ideal for web apps hosted on servers that support dynamic URLs.
    
* The **History API** is a feature built into modern browsers that allows a web application to change the URL in the address bar without triggering a full page refresh.
    
* It provides methods such as `pushState()`, which adds a new entry to the browser history, and `replaceState()`, which replaces the current history entry.
    
* This is particularly important in React applications because it enables navigation between routes such as moving from `/` to `/about` without reloading the page. Instead of fetching a new HTML document, React reads the updated URL and dynamically renders the corresponding component, keeping the application fast and seamless.
    
    ```javascript
    import { BrowserRouter, Routes, Route } from "react-router-dom";
    
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
    ```
    

### 2\. HashRouter

* Some routers (like `HashRouter`) use a `#` in the URL, e.g., [`www.example.com/#/about`](http://www.example.com/#/about).
    
* `BrowserRouter` avoids the `#`, giving **clean URLs**: [`www.example.com/about`](http://www.example.com/about).
    
* This is more professional and looks like a traditional website URL.
    
    ```javascript
    import { HashRouter, Routes, Route } from "react-router-dom";
    
    <HashRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </HashRouter>
    ```
    

### 3\. MemoryRouter

* **MemoryRouter** is a type of React Router that keeps the navigation history **in memory** instead of using the browser’s URL. This means that when you navigate between routes, the URL in the address bar does not change.
    
* Because of this, it is especially useful in scenarios where a browser URL is not needed or available, such as **testing components**, **server-side rendering (SSR)**, or **React Native apps**.
    
* MemoryRouter allows you to simulate navigation and route changes entirely in memory, making it ideal for environments where managing the actual browser history or URL is unnecessary.
    
    ```javascript
    import React from "react";
    import { MemoryRouter, Routes, Route, Link } from "react-router-dom";
    
    // Example pages/components
    function Home() {
        return <h2>Home Page</h2>;
    }
    
    function About() {
        return <h2>About Page</h2>;
    }
    
    function App() {
        return (
            <MemoryRouter initialEntries={["/"]}>
                <nav>
                    <Link to="/">Home</Link> | <Link to="/about">About</Link>
                </nav>
                <Routes>
                    <Route path="/" element={<Home />} />
                    <Route path="/about" element={<About />} />
                </Routes>
            </MemoryRouter>
        );
    }
    
    export default App;
    ```
    
    * `MemoryRouter` stores the navigation history **in memory**, so the browser URL does **not change**.
        
    * `initialEntries={["/"]}` sets the initial route to `/`.
        
    * Navigation between Home and About works, but the URL in the browser’s address bar stays the same.
        
    * This is useful for **testing** components or **React Native apps**, where a real browser URL is not needed.
        

---

## React Router DOM

**React Router DOM** is an npm package specifically designed for enabling routing in **React web applications**. It allows developers to create **Single Page Applications (SPAs)**, where different components or views are rendered dynamically based on the URL path, without requiring a full page reload. This makes navigation smooth, fast, and seamless, giving users the feel of a multi-page website while actually staying on a single HTML page.

### **Why use React Router DOM?**

* **Smooth navigation:** Move between different views or pages without refreshing the browser.
    
* **URL-based dynamic rendering:** Components render based on the current URL path.
    
* **Nested routes:** Allows hierarchical or nested layouts for complex apps.
    
* **Maintainability:** Makes it easier to structure and manage large React applications with multiple views.
    

### **Core Components**

1. `<BrowserRouter>` – Wraps the entire app to enable routing using the browser’s history API.
    
2. `<Routes>` & `<Route>` – Define all the routes in your app. Each `<Route>` specifies a path and the component to render.
    
3. `<Link>` – Provides navigation between routes **without refreshing** the page.
    
4. `<NavLink>` – Similar to `<Link>`, but can automatically apply styles or highlight the active route.
    

### **Important Hooks**

* `useNavigate` – Programmatically navigate to a route.
    
* `useParams` – Access dynamic route parameters from the URL.
    
* `useLocation` – Get the current URL location object.
    
* `useRouteMatch` – Check if a route matches the current URL (useful for nested routes).
    

---

## Creating Routes in React

1. **Initialize a React Project:**
    

```javascript
npm create vite@latest react-router-example
cd react-router-example
```

2. **Install React Router:**
    

```javascript
npm install react-router-dom@6
```

3. **Set Up Router in App.js:**
    

```javascript
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";
import Home from "./components/Home";
import About from "./components/About";
import Contact from "./components/Contact";

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
        <Link to="/contact">Contact</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## Dynamic Routing

Dynamic routing allows routes to change based on data or user input. For example, if you have multiple courses:

```javascript
const courses = ["JavaScript", "React", "HTML"];

<ul>
  {courses.map(course => (
    <li key={course}>
      <Link to={`courses/${course}`}>{course}</Link>
    </li>
  ))}
</ul>

<Routes>
  <Route path="courses/:courseId" element={<CourseDetails />} />
</Routes>
```

Here, `:courseId` is a dynamic parameter accessed in the `CourseDetails` component using the `useParams()` hook.

---

## React Router Hooks

Hooks allow functional components to interact with the router.

### 1\. `useNavigate()`

* Navigate programmatically without `<Link>`.
    

```javascript
import { useNavigate } from "react-router-dom";

function Home() {
  const navigate = useNavigate();
  return <button onClick={() => navigate("/dashboard")}>Go to Dashboard</button>;
}
```

### 2\. `useParams()`

* Access dynamic URL parameters.
    

```javascript
import { useParams } from "react-router-dom";

function Profile() {
  const { userName } = useParams();
  return <h1>Profile: {userName}</h1>;
}
```

### 3\. `useLocation()`

* Get the current URL and query parameters.
    

```javascript
import { useLocation } from "react-router-dom";

function Profile() {
  const location = useLocation();
  const searchParams = new URLSearchParams(location.search);
  return <div>ID: {searchParams.get("id")}</div>;
}
```

### 4\. `useRouteMatch()`

* Check how the current URL matches a route (useful for nested routes).
    

```javascript
import { useParams, useRouteMatch, Link } from "react-router-dom";

function Profile() {
  const { userName } = useParams();
  const match = useRouteMatch();

  return (
    <div>
      {match.isExact ? (
        <div>
          <h1>{userName}'s Profile</h1>
          <Link to={`${match.url}/followers`}>Followers</Link>
        </div>
      ) : (
        <div>Followers List</div>
      )}
    </div>
  );
}
```

---

## Link vs NavLink

| Feature | Link | NavLink |
| --- | --- | --- |
| Navigation | Yes | Yes |
| Active Styling | No | Yes |
| Use Case | Normal links | Menus, tabs, sidebars |

Mastering React Router is essential for building smooth and interactive SPAs. By understanding different router types, dynamic routing, hooks, and navigation components like Link and NavLink, you can create well-structured, user-friendly React applications. Programmatic navigation, nested routes, and dynamic parameters make your app scalable and efficient.

React Router provides everything you need to build seamless navigation without page reloads, enhancing the user experience and making your web app feel fast and modern.