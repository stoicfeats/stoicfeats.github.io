---
title: "server-side-rendering"
date: 2025-10-26T12:08:58+05:30
draft: false
---

### **🧩 1. What is Client-Side Rendering (CSR)?**

In normal **React** apps (built with create-react-app or similar), the browser:

1. Downloads a mostly **empty HTML file**.
2. Then downloads a big **JavaScript bundle**.
3. React runs **in the browser** to build the visible page (this is called *Client-Side Rendering*, CSR).

So the user just sees a blank screen for a moment — until React finishes running.

---

### **⚙️ Server-Side Rendering (SSR)**

With **Server-Side Rendering**, the **server** runs the React code first, builds the HTML for the requested page, and sends that *ready-to-see* HTML to the browser.

So the steps are:

1. User requests example.com/products.
2. The **server executes React code**, fetches data, and renders full HTML (product list).
3. Browser gets that complete HTML, displays it immediately.
4. Then React’s JavaScript “hydrates” — it attaches event listeners, enabling interactivity.

**In short:**

- CSR = Browser does all rendering.
- SSR = Server builds the page first → faster visible content, better SEO.

---

### **🚀 2. Why SSR is useful**

**Main benefits:**

- **Faster initial page load** (because the HTML already has content).
- **Better SEO** (search engines can read HTML content directly).
- **Better performance for slow devices** (less work on the client).

**Downsides:**

- Needs a running server (not just static files).
- Slightly higher backend load — server must render on every request.

---

### **💡 3. Where Next.js comes in**

React itself doesn’t handle how or *where* rendering happens — it’s just a UI library.

**Next.js** is a framework built *on top of React* that:

- Adds **server-side rendering (SSR)** out of the box.
- Also supports **Static Site Generation (SSG)** and **Client-Side Rendering (CSR)** — you can mix all three as needed.
- Provides **routing**, **API routes**, and **optimizations** (image optimization, caching, etc.).

---

### **🧱 4. How Next.js does SSR**

Example: a Next.js page like pages/users.js:

```
// pages/users.js
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/users');
  const users = await res.json();

  return { props: { users } }; // these props go into the React component
}

export default function UsersPage({ users }) {
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

- When someone visits /users, Next.js runs getServerSideProps() **on the server**, fetches data, renders the HTML with that data, and sends it to the browser.
- The user sees a ready-made page instantly.
- Then React hydrates to make it interactive (clicks, etc.).

---

### **🧠 5. TL;DR Summary**

| **Concept** | **React (CSR)** | **Next.js (SSR)** |
| --- | --- | --- |
| Rendering location | In the browser | On the server first |
| Page load | Blank → content after JS runs | Content visible instantly |
| SEO | Poor by default | Excellent |
| Setup | Simple SPA | Framework (routes, API, SSR) |
| Use case | Dashboards, SPAs, apps behind login | Blogs, e-commerce, landing pages, SEO-driven apps |

---

### **🎯 6. How to think about it as a developer**

Think of **Next.js** as giving React a **brain for how to render** — it decides:

- Should this page be pre-built (SSG)?
- Should it be rendered live on the server (SSR)?
- Should it just render on the client (CSR)?

That flexibility is what makes Next.js so powerful in production — you get the developer experience of React, but with speed and SEO benefits like a traditional server-rendered site.

---

Would you like me to add a quick diagram showing the flow difference between CSR and SSR (React vs Next.js)? It helps visualize what happens under the hood.