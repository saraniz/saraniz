---
title: "React Conditional Rendering: A Complete Guide"
datePublished: Thu Dec 25 2025 13:17:07 GMT+0000 (Coordinated Universal Time)
cuid: cmjlgvx4g000002kz7gxc3imh
slug: react-conditional-rendering-a-complete-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1766668523675/4054d134-cbc3-4330-b918-34f7c3accd1a.png
tags: javascript, reactjs, rendering, conditional-statement, react-libraries, conditionalrendering

---

In React, **conditional rendering** allows you to display different content or components depending on certain conditions. It is a key concept for building dynamic user interfaces because it ensures that users see only the relevant information based on their actions, data, or system state. Instead of manually changing the DOM, React updates the UI automatically when conditions change.

## What is Conditional Rendering?

Conditional rendering lets components **render different outputs** based on state or props. For example, you can show a login button if a user is not authenticated, or display a profile page if they are logged in. This approach makes the UI **dynamic, efficient, and user-friendly**.

## How to Implement Conditional Rendering

There are several ways to conditionally render elements in React:

### <mark>1. Using If/Else Statements</mark>

If/else statements allow you to decide which component or element to render based on a condition. This is useful for **complex logic**.

```javascript
function Item({ name, isPacked }) {
    if (isPacked) {
        return <li className="item">{name} ✅</li>;
    }
    return <li className="item">{name}</li>;
}

// If isPacked is true: Space Suit ✅
// If isPacked is false: Space Suit
```

---

### <mark>2. Using Ternary Operator</mark>

The **ternary operator** is a **short form of an if–else condition**. It checks a condition and returns **one of two values** based on whether the condition is true or false.

```plaintext
condition ? value_if_true : value_if_false
```

```javascript
function Greeting({ isLoggedIn }) {
    return <h1>{isLoggedIn ? "Welcome Back!" : "Please Sign In"}</h1>;
}

//  isLoggedIn = true: Welcome Back!
//  isLoggedIn = false: Please Sign In
```

---

### <mark>3. Using Logical AND (&amp;&amp;) Operator</mark>

The `&&` operator is a **logical operator** from JavaScript. It is commonly used in React for **conditional rendering**. It renders content **only when the condition is true**.

```plaintext
condition && result
```

```javascript
function Notification({ hasNotifications }) {
    return <div>{hasNotifications && <p>You have new notifications!</p>}</div>;
}

//  hasNotifications = true: You have new notifications!
//  hasNotifications = false: Nothing is displayed
```

---

### <mark>4. Using Switch Case Statements</mark>

Switch statements are helpful when there are **multiple possible conditions**.

```javascript
function StatusMessage({ status }) {
    switch (status) {
        case 'loading':
            return <p>Loading...</p>;
        case 'success':
            return <p>Data loaded successfully!</p>;
        case 'error':
            return <p>Error loading data.</p>;
        default:
            return <p>Unknown status</p>;
    }
}

// 'loading': Loading...
//  'success': Data loaded successfully!
//  'error': Error loading data
```

---

### <mark>5. Conditional Rendering in Lists</mark>

**Conditional rendering in lists** means **showing only some items from a list**, based on a condition. This is commonly done using `map()` , a condition like a ternary operator or logical checks.

```javascript
const items = ["Apple", "Banana", "Cherry"];
const fruitList = items.map((item, index) =>
    item.includes("a") ? <p key={index}>{item}</p> : null
);

// The key helps React identify which items have changed. Each item in a list should have a unique key.
```

* ### How This Works Step by Step
    
    1. [`items.map`](http://items.map)`()` loops through each item in the array.
        
    2. For each item, it checks the condition:
        
        ```javascript
        item.includes("a")
        ```
        
        This checks whether the item contains the letter **"a"**.
        
    3. If the condition is **true**:
        
        * A `<p>` element is returned and rendered.
            
    4. If the condition is **false**:
        
        * `null` is returned.
            
        * React ignores `null`, so **nothing is displayed** for that item.
            
    

`filter()` is a **JavaScript array method** used to **remove items that do not match a condition**.  
In React, it is commonly used **before rendering a list** to display only the items you want.

```javascript
array.filter(item => condition)

// If the condition returns true, the item is kept.
// If the condition returns false, the item is removed.
```

```javascript
const items = ["Apple", "Banana", "Cherry"];

const fruitList = items
  .filter(item => item.includes("a"))
  .map((item, index) => <p key={index}>{item}</p>);
```

### How This Works

1. `filter()` checks each item in the array.
    
2. It keeps only items that contain the letter `"a"`.
    
3. `map()` then converts the filtered items into JSX elements.
    

### Why do we use `map()` here?

In React, **you cannot directly render an array of raw data** (like strings or objects) as UI elements.  
React needs **JSX elements** (`<p>`, `<div>`, `<li>`, etc.) to display something on the screen.That is exactly why `map()` is used.

What `filter()` does

```javascript
items.filter(item => item.includes("a"))
```

* This only **selects data**.
    
* After filtering, the result is still **an array of strings**:
    

```plaintext
["Apple", "Banana"]
```

At this stage, React **still cannot display this properly** as UI.

### What `map()` does

```javascript
.map(item => <p>{item}</p>)
```

* `map()` **transforms each data item into JSX**.
    
* It converts:
    

```javascript
"Apple"  →  <p>Apple</p>
"Banana" →  <p>Banana</p>
```

Now React receives:

```plaintext
[<p>Apple</p>, <p>Banana</p>]
```

This is something React **can render**. Simple rule to remember

* `filter()` → decides WHAT data to keep
    
* `map()` → decides HOW to display that data
    

You almost always use `map()` when rendering lists in React because **each item must become a JSX element**.

---

### <mark>6. Conditional Rendering with Component State</mark>

You can render elements based on the component’s **state**. For example, show a loading message while data is being fetched, then display the content after it’s ready.

```javascript
if (loading) {
  // Render Loading Component
} else {
  // Render Data Component
}
```

---

Conditional rendering is a powerful feature in React that allows developers to create **dynamic, responsive, and interactive interfaces**. By using **if/else statements, ternary operators, logical AND, switch cases, or state-based conditions**, you can control exactly what appears on the screen based on user actions or data changes.

Mastering conditional rendering improves **user experience** and makes your React applications more **efficient and maintainable**.