---
title: "Next.js Routing – Complete Guide (Pages Router & App Router)"
datePublished: Sat Dec 27 2025 14:36:56 GMT+0000 (Coordinated Universal Time)
cuid: cmjoem9l5000202kyb0wf9vje
slug: nextjs-routing-complete-guide-pages-router-and-app-router
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1766846129409/6f8e58d2-5690-44fe-a518-bdda88407d41.png
tags: reactjs, nextjs, react-framework, nextjs-132, nextjs-app-router

---

Routing is how a web application decides **which page to show for a given URL**.  
Next.js uses a **file-based routing system**, meaning the folder and file structure you create inside the project automatically becomes your website’s routes.

Next.js supports **two routing systems**:

1. **Pages Router** – the traditional routing system (used before Next.js 13)
    
2. **App Router** – the modern routing system (introduced in Next.js 13)
    

Both are still supported, but **App Router is the recommended approach for new projects**.

### 1\. Pages Router (Traditional Routing System)

The **Pages Router** is the original and traditional routing system in Next.js. It is based entirely on a special folder called `pages/`. This router follows a **file-based routing** approach, which means the structure of your files and folders directly decides the URLs of your application.

When you create a Next.js project using older versions (or when you choose the Pages Router intentionally), this routing system is used by default.

In the Pages Router, **every file inside the** `pages/` directory automatically becomes a route. You do not need to write any routing configuration manually.

Example folder structure:

```javascript
pages/
 ├── index.js
 ├── about.js
 ├── contact.js
```

Resulting routes:

* `pages/index.js` → `/`
    
* `pages/about.js` → `/about`
    
* `pages/contact.js` → `/contact`
    

So, if a user visits `/about` in the browser, Next.js will render the component inside `about.js`.

**<mark>Nested Routes (Pages Router)</mark>**

In the **Pages Router**, nested routes are created by using **folders inside the** `pages/` directory. The folder structure directly represents the URL structure. This makes routing very easy to understand and manage.

Basic Folder-Based Nesting

Consider this folder structure:

```javascript
pages/
 └── blog/
     ├── index.js
     └── post.js
```

Here is how Next.js converts files into URLs:

| File Path | URL Path |
| --- | --- |
| `blog/index.js` | `/blog` |
| `blog/post.js` | `/blog/post` |

* The `blog` folder becomes the `/blog` part of the URL.
    
* The `index.js` file represents the default page of that folder.
    
* Any other file inside the folder becomes a sub-route.
    

The `index.js` file is special. It represents the **root route of a folder**. Without `index.js`, the folder would not have a main page.

**<mark>Dynamic Routes (Pages Router)</mark>**

In the **Pages Router**, **dynamic routes** are used when parts of the URL are not fixed and can change. This is very common for pages like blog posts, product details, user profiles, and articles where each item has a unique identifier.

Instead of creating a separate file for every possible URL, Next.js lets you define a **variable route** using square brackets.

Basic Dynamic Route Structure

Example folder structure:

```javascript
pages/
 └── blog/
     └── [id].js
```

Here, `[id].js` is a **dynamic route file**.

This single file can handle many URLs:

| URL | Meaning |
| --- | --- |
| `/blog/1` | `id = 1` |
| `/blog/hello` | `id = hello` |
| `/blog/abc123` | `id = abc123` |

Anything that appears in the place of `[id]` in the URL will be captured and made available to your page.

**How Dynamic Routing Works Internally:**

* The name inside the square brackets (`id`) becomes a **parameter name**
    
* Next.js reads the URL and assigns the value to that parameter
    
* You can access this value inside your component
    

So for `/blog/hello`, Next.js understands:

```javascript
id = "hello"
```

**Accessing Dynamic Values with** `useRouter`:

To read the dynamic value, you use the `useRouter` hook from `next/router`.

Example code:

```javascript
import { useRouter } from 'next/router';

export default function BlogPost() {
  const router = useRouter();
  const { id } = router.query;

  return <h1>Post ID: {id}</h1>;
}
```

Explanation:

* `useRouter()` gives you access to routing information
    
* `router.query` contains all dynamic route parameters
    
* `{ id }` extracts the value from the URL
    

**Important Behavior to Know:**

#### 1\. Value is undefined at first (Client Side)

On the first render, `id` may be `undefined` because routing data loads after the component mounts.

Safe usage example:

```javascript
if (!id) return <p>Loading...</p>;
```

This avoids runtime errors.

**<mark>Catch-All Routes (Pages Router)</mark>**

In the **Pages Router**, **catch-all routes** are used when you want a single page to handle **multiple URL segments**, no matter how many levels deep the path goes. This is especially useful for documentation sites, nested categories, or flexible content structures.

You create a catch-all route by using **three dots (**`...`) inside square brackets.

**Folder structure:**

```javascript
pages/
 └── docs/
     └── [...slug].js
```

This file matches **any path after** `/docs/`.

**How URLs Are Matched:**

| URL | `slug` value |
| --- | --- |
| `/docs/a` | `['a']` |
| `/docs/a/b` | `['a', 'b']` |
| `/docs/a/b/c` | `['a', 'b', 'c']` |

Key points:

* `slug` is always an **array.** A **slug** is the **part of the URL that comes after the main route** and helps identify what content to show.In simple words, a slug is a **URL-friendly name** for a page or piece of content.
    
* Each URL segment becomes one item in the array
    
* The file `[...slug].js` handles all these routes
    

**Accessing Catch-All Values:**

Use `useRouter` to read the `slug` array.

```javascript
import { useRouter } from 'next/router';

export default function DocsPage() {
  const router = useRouter();
  const { slug } = router.query;

  if (!slug) return <p>Loading...</p>;

  return <p>Path: {slug.join(' / ')}</p>;
}
```

Example output:

* `/docs/a/b` → `Path: a / b`
    

**Optional Catch-All Routes :**

An **optional catch-all route** is a special type of dynamic route in the Next.js Pages Router that can handle **both** the base path and any number of nested paths using **one single file**.

It is called *optional* because the dynamic part of the URL may exist **or may not exist**.

File Naming Pattern:

Optional catch-all routes use **double square brackets** with three dots:

```javascript
[[...slug]].js
```

Folder Structure Example

```javascript
pages/
 └── docs/
     └── [[...slug]].js
```

This single file can handle all of the following URLs.

How URLs Are Matched

| URL | slug value |
| --- | --- |
| `/docs` | undefined |
| `/docs/a` | \['a'\] |
| `/docs/a/b` | \['a', 'b'\] |
| `/docs/a/b/c` | \['a', 'b', 'c'\] |

Important points:

* When the URL is exactly `/docs`, the `slug` value is `undefined`
    
* When there are extra path segments, `slug` becomes an array
    
* Each part of the URL is stored as one element in the array
    

Accessing the Value

You can read the value using `useRouter`.

```javascript
import { useRouter } from 'next/router';

export default function DocsPage() {
  const router = useRouter();
  const { slug } = router.query;

  if (!slug) {
    return <h1>Docs Home Page</h1>;
  }

  return <h1>Docs Path: {slug.join(' / ')}</h1>;
}
```

What This Code Does

* If the user visits `/docs`, `slug` is undefined, so the page shows a docs home page
    
* If the user visits `/docs/intro`, `slug` is `['intro']`
    
* If the user visits `/docs/intro/setup`, `slug` is `['intro', 'setup']`
    

This allows one file to behave like **multiple pages**.

***<mark>Special Files in Pages Router</mark>***

The Pages Router provides some **special files** that have specific purposes in a Next.js application. These files allow you to control **global behavior, HTML structure, error handling, and more**.

#### 1\. `_app.js` – Wraps all pages

* Purpose: Provides a **top-level component** that wraps every page in your application.
    
* Use it for **global layouts, styles, context providers, or persistent UI elements**.
    
* Location: `pages/_app.js`
    

**Example use case:** Adding a global header and footer to all pages.

#### 2\. `_document.js` – Custom HTML structure

* Purpose: Modify the **overall HTML document**, including `<html>` and `<body>` tags.
    
* Use it for **adding global fonts, meta tags, scripts, or language attributes**.
    
* Location: `pages/_document.js`
    

**Example:** Setting a custom language attribute and including a font link.

#### 3\. `404.js` – Custom Not Found Page

* Purpose: Display a **custom 404 page** when a route does not exist.
    
* Location: `pages/404.js`
    

#### 4\. `500.js` – Server Error Page

* Purpose: Display a **custom error page** for server-side errors.
    
* Location: `pages/500.js`
    

### Data Fetching in Pages Router

Next.js provides methods to fetch data for pages, and each method runs at a **different time**.

| Method | When it runs | Use Case |
| --- | --- | --- |
| `getStaticProps` | At **build time** | Pre-render a page with static content (SSG) |
| `getStaticPaths` | At **build time** for dynamic static pages | Generate paths for pages with dynamic routes (SSG) |
| `getServerSideProps` | On **every request** | Pre-render a page with dynamic data on the server (SSR) |

---

### 2\. App Router (Modern Routing System)

The **App Router** is the modern routing system in Next.js. It replaces the traditional Pages Router for new projects and is designed to work with **React Server Components**.

* The App Router uses the `app/` directory instead of `pages/`.
    
* Routing is **folder-based**: each folder represents a path, and `page.js` inside a folder defines the page component for that route.
    
* It supports **Server Components by default**, allowing better performance and scalability. That mean components inside the `app/` directory **run on the server automatically t**hey can fetch data and render HTML before sending it to the client. You only make a component a **Client Component** if it needs browser features \[using “use client”\]
    
* Provides advanced features like **layouts, nested routing, loading states, and templates**.
    

Folder structure example:

```javascript
app/
 ├── page.js
 ├── about/
 │    └── page.js
```

How the URLs map:

| File | URL |
| --- | --- |
| `app/page.js` | `/` |
| `app/about/page.js` | `/about` |

* `page.js` in the root of `app/` → corresponds to the **home page** (`/`)
    
* `page.js` inside a folder → corresponds to the **folder name as the route** (`/about`)
    

**<mark>Layouts</mark>**

Layouts in the **App Router** are a core feature that allow you to define **shared UI components** such as headers, footers, sidebars, or navigation bars that remain consistent across multiple pages. Unlike Pages Router, layouts in App Router are **folder-based and persistent**, meaning they do not get re-rendered when navigating between pages within the layout’s scope. This helps improve performance and maintain a consistent UI structure.

In simply `layout.js` in `app/` is the **root layout**. Any page inside the `app/` folder (or subfolders) will automatically use this layout. So if you add a **header, navbar, or footer** in this root layout, it appears **on all pages** that are inside the `app/` folder.

Example Folder Structure:

```javascript
app/
 ├── layout.js     // Root layout
 └── page.js       // Home page
```

* `layout.js` defines the **overall structure** of your app.
    
* `page.js` is the page content that gets inserted into the layout via `{children}`.
    

**<mark>Nested Layouts</mark>**

Nested layouts allow you to create **section-specific layouts** that apply only to certain parts of your app, while still keeping the **root layout** for shared UI like headers and footers.

Folder Structure Example :

```javascript
app/
 ├── layout.js           // Root layout (applies to entire app)
 └── dashboard/
      ├── layout.js      // Nested layout (applies only to /dashboard and its subpages)
      └── page.js        // Dashboard home page
```

* `app/layout.js` → Root layout for the whole application
    
* `app/dashboard/layout.js` → Nested layout that wraps only `/dashboard` pages
    
* `page.js` → Content specific to `/dashboard`
    

When you visit `/dashboard`:

1. **Root layout** (`app/layout.js`) renders first:
    
    * Includes global UI like navbar, footer, etc.
        
2. **Nested layout** (`app/dashboard/layout.js`) renders inside the root layout:
    
    * Adds additional UI specific to the dashboard, like a sidebar.
        
3. **Page content** (`app/dashboard/page.js`) renders inside the nested layout at `{children}`.
    

**<mark>Dynamic Routes in App Router</mark>**

Dynamic routes allow your application to handle **variable URLs** for example, blog posts, user profiles, or productswithout creating separate files for each one.

  
Folder Structure Example:

```javascript
app/
 └── blog/
      └── [id]/
           └── page.js
```

* `[id]` is a **dynamic segment**. It acts as a placeholder for any value in that part of the URL.
    
* `page.js` is the page that will render the content based on the dynamic `id`.
    

Next.js automatically provides the **dynamic value** via the `params` prop.

**Example code:**

```javascript
export default function BlogPost({ params }) {
  return <h1>Post ID: {params.id}</h1>;
}
```

* If you visit `/blog/1` → [`params.id`](http://params.id) `= "1"` → shows **Post ID: 1**
    
* If you visit `/blog/hello` → [`params.id`](http://params.id) `= "hello"` → shows **Post ID: hello**
    

**<mark>Catch-All and Optional Catch-All Routes in App Router</mark>**

Catch-all routes allow you to handle **multiple nested segments** in a single route without creating individual files for each possible URL. Optional catch-all routes allow the **base route** to work in addition to multiple nested segments.

**Catch-All Route** `[...slug]` :

**Folder structure example:**

```javascript
app/
 └── docs/
      └── [...slug]/
           └── page.js
```

* `[...slug]` is a **catch-all segment**. It captures **all paths after** `/docs`.
    
* The captured values are available in `params.slug` as an **array**.
    

**Optional Catch-All Route** `[[...slug]]` :

**Folder structure example:**

```javascript
app/
 └── docs/
      └── [[...slug]]/
           └── page.js
```

* `[[...slug]]` is **optional**, meaning it works for the **base route** and nested routes.
    
* If no nested segments exist, `params.slug` is `undefined`.
    

**<mark>Route Groups in App Router (No URL Impact)</mark>**

Route groups are a way to **organize your app’s folder structure** without affecting the URLs that users see. They help you keep your code clean, modular, and easier to maintain.

* A **route group** is a folder **wrapped in parentheses** `(groupName)`.
    
* The folder **does not appear in the URL**.
    
* It is purely for **code organization**, grouping related pages together.
    

Example Folder Structure :

```javascript
app/
 └── (auth)/
      ├── login/
      │    └── page.js
      └── register/
           └── page.js
```

* `(auth)` is a route group.
    
* `login/page.js` → the login page component
    
* `register/page.js` → the register page component
    
* `(auth)` is **ignored in the URL**.
    

Even though the files are inside `(auth)`:

| File | URL |
| --- | --- |
| `(auth)/login/page.js` | `/login` |
| `(auth)/register/page.js` | `/register` |

* Users see clean URLs without any trace of the route group.
    

**<mark>Navigation in App Router</mark>**

Navigation in the App Router lets users move between pages either by clicking links or programmatically through code. Next.js provides two main ways: `Link` component for clickable links and `useRouter` hook for programmatic navigation.

**1\. Using** `Link` **Component**

The `Link` component is used for **client-side navigation**. It prevents full page reloads, making transitions faster and smoother.

**Example:**

```javascript
import Link from 'next/link';

export default function Navbar() {
  return (
    <nav>
      <ul>
        <li><Link href="/">Home</Link></li>
        <li><Link href="/about">About</Link></li>
        <li><Link href="/dashboard">Dashboard</Link></li>
      </ul>
    </nav>
  );
}
```

* Use `href` to specify the destination path.
    
* Navigation happens **without reloading the page**.
    
* Works for both **static and dynamic routes**.
    

**2\. Programmatic Navigation with** `useRouter`

Sometimes you need to navigate **via code**, for example after submitting a form or a login action.

**Example:**

```javascript
'use client'; // Required because useRouter is client-side only

import { useRouter } from 'next/navigation';

export default function LoginButton() {
  const router = useRouter();

  const handleLogin = () => {
    // Perform login logic
    router.push('/dashboard'); // Navigate to dashboard
  };

  return <button onClick={handleLogin}>Login</button>;
}
```

* `router.push('/path')` → navigates to a new route.
    
* `router.replace('/path')` → navigates without adding a new entry in browser history.
    
* `useRouter` can only be used in **Client Components** (`'use client';` at the top).
    

**3\. Navigation with Dynamic Routes**

* For dynamic routes, you can pass parameters in `href`:
    

```javascript
<Link href={`/blog/${post.id}`}>Read More</Link>
```

* Programmatic navigation works similarly:
    

```javascript
router.push(`/blog/${post.id}`);
```

**4\. Navigation with Route Groups**

* Route groups `(groupName)` do **not affect the URL**, so navigation works normally:
    

```javascript
<Link href="/login">Login</Link>
<Link href="/register">Register</Link>
```

Even if the files are inside `(auth)` folder, the URLs remain clean.

**<mark>Loading UI</mark>**

```javascript
app/loading.js
```

Automatically shown while loading a route.

**<mark>Error Handling</mark>**

```javascript
app/error.js
```

For route-level errors.

```javascript
app/not-found.js
```

For 404 pages.

### Server vs Client Components in App Router

In the **App Router**, components can run either on the **server** or on the **client**. Understanding the difference is important because it affects **where your code runs, how data is fetched, and what features you can use**.

**<mark>1. Server Components (Default)</mark>**

* All components in the `app/` directory are **Server Components** unless you explicitly mark them as client components. The component renders HTML on the server and sends it to the browser.
    
* **Benefits:**
    
    1. Faster initial load (less JavaScript sent to the client)
        
    2. Can fetch data directly from a database or API securely
        
    3. Reduces client-side JavaScript and improves performance
        

**Example:**

```javascript
export default async function ServerComponent() {
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  return (
    <div>
      <h1>Posts</h1>
      <ul>
        {posts.map(post => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

* Runs entirely on the server.
    
* You **cannot** use browser-only features like `useState`, `useEffect`, or `window`.
    

**<mark>2. Client Components</mark>**

* **Used when you need browser-specific functionality**, such as interactivity, forms, or animations.
    
* **Mark the component** as a client component by adding `'use client';` at the top.
    

**Example:**

```javascript
'use client';

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
}
```

* Runs **in the browser**.
    
* Can use React hooks like `useState` and `useEffect`, or browser APIs like `window` or `localStorage`.
    
* Cannot directly fetch server-only resources (like a database) securely without an API route.
    

### Data Fetching in App Router

In the **App Router**, data fetching is simpler and more flexible compared to Pages Router. You can fetch data **directly inside Server Components** using `fetch()` instead of `getStaticProps` or `getServerSideProps`.

```javascript
export default async function PostsPage() {
  const res = await fetch('https://api.example.com/posts', { cache: 'no-store' });
  const posts = await res.json();

  return (
    <div>
      <h1>Posts</h1>
      <ul>
        {posts.map(post => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

* The component is a **Server Component by default**.
    
* `fetch()` runs on the server.
    
* `cache` option controls how the data is stored and updated.
    

**Cache Options:**

| Option | Meaning |
| --- | --- |
| `force-cache` | **Static** – Cache the response at build time. Content doesn’t change until the next build. |
| `no-store` | **Dynamic** – Fetch new data on **every request**. No caching is done. |
| `revalidate` | **Incremental** – Cache the data but refresh after a certain number of seconds. Example: `{ next: { revalidate: 10 } }` refreshes every 10 seconds. |

### Parallel Routes and Intercepting Routes in App Router

These are **advanced routing features** in Next.js App Router that help you build complex UI patterns like **dashboards, modals, and overlays**.

**<mark>1. Parallel Routes</mark>**

Parallel routes allow you to **render multiple sections of a page independently** at the same time. This is useful for layouts like dashboards where different panels or sections load simultaneously.

Example Folder Structure:

```javascript
app/
 └── dashboard/
      ├── @analytics/page.js
      └── @settings/page.js
```

* The `@` symbol is used to indicate **parallel routes**.
    
* You can have multiple parallel routes inside a layout.
    
* Each section (`analytics` and `settings`) can render independently, but they share the same **dashboard layout**.
    

**Use Case:**

* Dashboard with a sidebar, analytics panel, and settings panel all rendering at once without blocking each other.
    

**<mark>2. Intercepting Routes</mark>**

Intercepting routes are used to **show modals, overlays, or temporary UI** without fully leaving the current page.

* **Special folder names:**
    
    * `(.)folder` → For modals or temporary routes that appear on top of the current page
        
    * `(…)folder` → For overlays that might cover part of the UI
        

Example Use Case:

```javascript
app/
 └── (.)modal/
      └── login/page.js
```

* Visiting `/login` can open a **login modal** on top of the current page instead of navigating away.
    
* Intercepting routes make it easy to handle **UI layers** like modals, popups, or slide-over panels.
    

---

### Pages Router vs App Router

| Feature | Pages Router | App Router |
| --- | --- | --- |
| Directory | `pages/` | `app/` |
| Layouts | Manual | Built-in |
| Server Components | No | Yes |
| Loading UI | Manual | Built-in |
| Route Groups | No | Yes |
| Recommended | Old projects | New projects |

Next.js routing is powerful and easy because of its file-based system. The **Pages Router** is simple and familiar, while the **App Router** introduces advanced features like layouts, server components, and better data handling. For modern applications, **App Router is the future of Next.js routing** and is the best choice moving forward.