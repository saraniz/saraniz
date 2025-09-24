---
title: "React Simplified: Mastering Import, Export & JSX Without Confusion"
seoTitle: "React Simplified: Mastering Import, Export & JSX Without Confusion"
datePublished: Wed Sep 24 2025 11:17:30 GMT+0000 (Coordinated Universal Time)
cuid: cmfxw3ps5000002l17i4sbxwe
slug: react-simplified-mastering-import-export-and-jsx-without-confusion
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1758712513463/8c688f3f-85d9-4338-92e1-533a8e429a55.png
tags: javascript, reactjs, import, export, reacthooks, jsx-details, jsx-component

---

When you first open a React project, it’s easy to get overwhelmed. You see words like `import`, `export`, and a strange mix of HTML-looking code inside JavaScript files. If you’ve ever wondered, *“Wait, why is there HTML inside JS?”* or *“Why do we need to import and export everything?”* don’t worry, you’re not alone.

The good news is React isn’t as scary as it looks. Once you understand how **import/export** works and why **JSX** exists, everything starts to make sense. Think of it like learning the alphabet before forming sentences simple building blocks that let you create powerful applications.

## <mark>Importing and Exporting Components</mark>

React is built around components. Components are small, reusable building blocks that make up your entire app. They help to keep things clean and organized. You don’t usually keep all your components in one file. Instead, you create them in separate files and then **import** or **export** them whenever you need.

Think of importing and exporting like sharing tools between rooms in your house. If one room has a hammer (a component), you export it from that room and import it into another where you want to use it.

React uses **JavaScript ES6 modules** to do this. ES6 modules are the modern way JavaScript organizes and shares code between files. In JavaScript, before ES6 (2015), code was usually written in one big file or used older systems like `require()` and `module.exports`. With **ES6 (ECMAScript 2015)**, JavaScript introduced a modern system called **modules**.

* A **module** is just a file that contains some code.
    
* Instead of keeping everything in one place, you can split your code into multiple files (modules).
    
* To make parts of one file available to another, you **export** them.
    
* To use them in another file, you **import** them.
    

There are two main types of exports:

1. **Default Export and Import**
    
    A file can have **one default export**. When importing, you can call it whatever you like.
    
    ```javascript
    // MyComponent.js
    function MyComponent() {
      return <h2>Hello from MyComponent!</h2>;
    }
    
    export default MyComponent;
    ```
    
    ```javascript
    // App.js
    import MyComponent from "./MyComponent";
    
    function App() {
      return (
        <div>
          <MyComponent />
        </div>
      );
    }
    
    export default App;
    ```
    
    The keyword `default` means you’re exporting one main thing. When importing, you don’t need curly braces and can rename it if you want.
    
2. **Named Export and Import**
    
    You can also export **multiple items** from a file using named exports.
    
    ```javascript
    // components.js
    export function Header() {
      return <h1>Header Section</h1>;
    }
    
    export function Footer() {
      return <p>Footer Section</p>;
    }
    ```
    
    ```javascript
    // App.js
    import { Header, Footer } from "./components";
    
    function App() {
      return (
        <div>
          <Header />
          <Footer />
        </div>
      );
    }
    
    export default App;
    ```
    
    When you use **named exports** in React (or JavaScript in general), the curly braces `{ }` are required. Because a file can export many items, and the braces let you pick the exact ones by their names. Without curly braces, JavaScript would look for a default export instead. And also we should use the exact name of the component when importing it, because a file can have **many named exports**. JavaScript doesn’t know which one(s) you want unless you **specify them by name**.
    

**Mixing Default and Named Exports**

We can combine both in one file.

```javascript
// layout.js
export function Sidebar() {
  return <p>Sidebar</p>;
}

function Layout() {
  return <div>Main Layout</div>;
}

export default Layout;
```

```javascript
// App.js
import Layout, { Sidebar } from "./layout";

function App() {
  return (
    <div>
      <Layout />
      <Sidebar />
    </div>
  );
}

export default App;
```

**When to Use Which**

* **Default Export** → Use when the file has one main component. (e.g., `App`, `Navbar`)
    
* **Named Export** → Use when you want to share multiple items from one file. (e.g., `Button`, `Card`, `Input`)
    

---

## <mark>JSX: Writing HTML Inside JavaScript</mark>

Normally in JavaScript, you’d write UI like this:

```javascript
const element = React.createElement("h1", null, "Hello, World!");
```

That looks messy. So React uses a special syntax called **JSX**. JSX looks like HTML, but it’s actually JavaScript in disguise. It makes writing React components much easier and more natural.

```javascript
const element = <h1>Hello, World!</h1>;
```

JSX is not actually HTML, even though it looks very similar. It is what developers call **syntactic sugar**, which means it’s a nicer and easier way to write `React.createElement()` calls. When you write JSX, a tool called **Babel** automatically converts it into regular JavaScript code that browsers can understand. This JavaScript code describes the elements you want to render and their properties.

React then takes this code and uses it to build a **virtual DOM**, which is like a lightweight copy of the real browser DOM. The virtual DOM allows React to efficiently figure out what parts of the page have changed and update only those parts, instead of reloading the entire page. This process makes your application faster and smoother. Essentially, JSX lets you write your UI in a readable, HTML-like way, while Babel and React handle all the technical work behind the scenes.

### Features of JSX

**1\. Embedding JavaScript in JSX**

You can write JavaScript directly inside JSX using curly braces `{}`.

```javascript
const name = "Amie";
const element = <h1>Hello, {name}!</h1>;
```

Here, `{name}` is replaced by the value of the variable. If `name = "Amie"`, React will render:

**Hello, Amie!**

**2\. Attributes in JSX**

JSX attributes look like HTML, but with some small differences.

```javascript
const img = <img src="logo.png" alt="Logo" className="logo" />;
```

* In HTML, you’d write `class="logo"`.
    
* In JSX, you must use `className="logo"`, because `class` is a reserved word in JavaScript.
    

Other attributes like `htmlFor` (instead of `for`) follow the same rule.

**3\. Children in JSX**

Just like HTML tags, JSX components can have **children** inside them.

```javascript
function Welcome(props) {
  return <div>{props.children}</div>;
}

function App() {
  return (
    <Welcome>
      <h1>Hello!</h1>
      <p>Welcome to React.</p>
    </Welcome>
  );
}
```

* The `<Welcome>` component wraps around other elements.
    
* `{props.children}` means “whatever is placed between `<Welcome>` and `</Welcome>` will be rendered here.”
    
* This makes components flexible and reusable.
    

**4\. JSX is Actually JavaScript Objects**

Even though JSX looks like HTML, React doesn’t treat it as HTML. JSX is converted into JavaScript **objects** that describe what should appear on the screen.

```javascript
const button = <button onClick={() => alert("Clicked!")}>Click Me</button>;
```

Behind the scenes, this turns into:

```javascript
{
  type: "button",
  props: {
    onClick: () => alert("Clicked!"),
    children: ["Click Me"]
  }
}
```

* `type` is the element type (`button`).
    
* `props` holds attributes like `onClick` and `children`.
    
* `children` is the text or nested elements inside.
    

React then uses this object to create real DOM elements in the browser.

---

At the end, React isn’t about memorizing rules, it’s about writing code that feels natural and works smarter. Import and export keep your code organized, JSX makes your UI easy to read, and together they turn complexity into clarity. Once you’ve got these basics down, you’re no longer just learning React you’re building it with confidence.