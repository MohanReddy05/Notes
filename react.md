# Introduction

React JS was created by Jordan Walke, a software engineer at Facebook and open sourced to the world by Facebook and Instagram.

React is a JavaScript library for building user interfaces. It is used to create reusable UI components that can be easily composed to build complex interfaces.

### compitator

**Angular**
: Angular is a JavaScript framework for building web applications. It is used to create reusable UI components that can be easily composed to build complex interfaces.

| React                                                   | Angular                                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------------------------- |
| React is a small view library                           | Angular is a full framework                                                     |
| React covers only the rendering and event handling part | Angular provides the complete solution for front-end development                |
| Presentation code in JavaScript powered by JSX          | Presentation code in HTML embedded with JavaScript expressions                  |
| React's core size is smaller than Angular, so bit fast  | Angular being a framework contains a lot of code, resulting in longer load time |
| React is very flexible                                  | Angular is less flexible                                                        |
| It uses Virtual DOM to render the view                  | It uses Shadow DOM to render the view                                           |

# Pillars of React

### **Components**

Components are the building blocks of React. They are reusable and can be composed to create complex interfaces.

**Types of Components**

1. **Functional Components**

-   Functional components are the simplest type of components. They are functions that `return` JSX.
-   Functional components are stateless.
-   With the introduction of hooks, functional components can now manage state and lifecycle events
-   Example:

```jsx
import React from 'react';

function Greeting(props) {
    return <h1>Hello, {props.name}!</h1>;
}

export default Greeting;
```

2.  **Class Components**

-   Class components are ES6 classes that extend `React.Component`.
-   Class components are stateful and have access to lifecycle methods.
-   Class components are more complex than functional components.
-   They have a render method that returns React elements
-   Example:

```jsx
import { Component } from 'react';
class Greeting extends Component {
    render() {
        return <h1>Hello, {this.props.name}!</h1>;
    }
}
export default Greeting;
```

**Key Concepts of Components**

-   **Props**
    : Properties passed to a component from its parent.
-   **State**
    : Data that is specific to a component and can change over time.
-   **Lifecycle Methods**
    : Methods that are called at different stages of a component's lifecycle.
-   **Hooks**
    : Functions that allow functional components to manage state and lifecycle events.

---

### Virtual DOM

Virtual DOM is a lightweight, in-memory representation of the real DOM. It's a JavaScript object that mimics the structure of the DOM but doesn’t have the power to change what's on the screen directly.

When changes occur in a React component, React creates a new Virtual DOM tree. This tree is compared with the previous Virtual DOM tree (a process called diffing), and only the parts of the tree that need to be updated are updated in the real DOM.

**How Virtual DOM works**

1.  **Render**
    : When a React component is rendered, a Virtual DOM tree is created. This tree is a JavaScript object that mirrors the structure of the actual DOM but doesn’t interact with the browser.
2.  **Update**
    : When a component's state or props change, a new Virtual DOM tree is created. This tree is compared with the previous tree using a process called diffing.

    > **diffing**
    > :Diffing in the Virtual DOM is the process of comparing the current Virtual DOM tree with the previous one to determine what has changed. This comparison is crucial because it allows React to update the real DOM efficiently by only making the necessary changes.

3.  **Efficient Updates**
    : After determining the changes (or diff), React calculates the minimum number of updates needed to bring the real DOM in sync with the new Virtual DOM. This reduces the performance cost compared to updating the real DOM directly.

    -   **Patch**
        : The changes are then applied to the actual DOM. This is done by creating a patch, which is a set of instructions that tell the browser how to update the DOM.
    -   **Reconcile**
        : The browser then updates the DOM according to the patch.

**Benefits of Virtual DOM**

-   **Performance**
    : React's Virtual DOM makes updates more efficient by minimizing the number of changes made to the real DOM.
-   **Isolation**
    : The Virtual DOM is isolated from the real DOM, making it easier to manage and test.
-   **Predictability**
    : The Virtual DOM is predictable(Since React handles the updates efficiently), making it easier to reason about and debug.

## ![Virtual DOM](https://miro.medium.com/v2/resize:fit:828/format:webp/1*NLNoFfBWzu8Uu1RgWw3Z9g.jpeg)

---

### **JSX**

JSX is a syntax extension for JavaScript that allows you to create React elements in a more readable and expressive way. It's a way to write HTML-like code in JavaScript.

**Syntax**

```jsx
const element = <h1>Hello, world!</h1>;
```

**Key Features of JSX**:

-   **HTML-Like Syntax**: JSX looks similar to HTML, but it is transformed into JavaScript code by tools like Babel.
-   **Embedding Expressions**: You can embed JavaScript expressions inside JSX using curly braces `{}`.
-   **Components**: JSX can represent React components, which can be either functions or classes.
-   **Attributes**: JSX attributes are similar to HTML attributes, but they follow camelCase naming conventions (e.g., `className` instead of `class`).

**JSX Under the Hood**
JSX is not valid JavaScript on its own. Tools like Babel transpile JSX into regular JavaScript using `React.createElement()`. This function takes three arguments: the type of element, the attributes, and the children.
Example:

```jsx
const element = <h1>Hello, world!</h1>;
```

Transpiles to:

```javascript
const element = React.createElement('h1', null, 'Hello, world!');
```

**JSX Best Practices**:

-   **Use Fragments**
    : When returning multiple elements, wrap them in React.Fragment (or shorthand <>) instead of a <div> to avoid unnecessary DOM nodes.

    ```jsx
    <>
        <h1>Header</h1>
        <p>Paragraph</p>
    </>
    ```

-   **Keep JSX Simple**
    : If a JSX expression becomes too complex, consider breaking it down into smaller components or helper functions.

-   **Consistent Indentation**
    : Keep your JSX properly indented for better readability.

---

### SEO Performance

**What is SEO?**
SEO is the process of optimizing your website to rank higher in search engine results, thereby increasing organic (non-paid) traffic.

**Challenges of SEO in React**:

-   **Client-Side Rendering (CSR)**
    : React apps often use CSR, which can delay the availability of content to search engines because the HTML is generated after JavaScript execution.
-   **Dynamic Content**
    : Content generated dynamically via APIs might not be immediately visible to search engines unless handled properly.

**SEO Strategies for React**:

1. **Server-Side Rendering (SSR)**
   :

    - SSR generates the HTML on the server and sends it to the browser. This makes content available for search engines immediately.
    - **_Next.js_** is a popular framework built on React that supports SSR and static site generation (SSG).
    - Example with Next.js:
        ```bash
        npx create-next-app my-nextjs-app
        cd my-nextjs-app
        npm run dev
        ```

    Next.js automatically handles SSR, making your React app SEO-friendly.

2. **Static Site Generation (SSG)**
   :

    - SSG generates static HTML at build time, which can be served to users and crawlers.
    - **_Next.js_** also supports SSG using `getStaticProps`.
    - Example:
        ```jsx
        export async function getStaticProps() {
            const data = await fetch('https://api.example.com/data').then(
                (res) => res.json()
            );
            return {
                props: { data },
            };
        }
        export default function Home({ data }) {
            return <div>{data.title}</div>;
        }
        ```

3. **React Helmet**
   :

    - **_React Helmet_** allows you to manage the document head (e.g., meta tags, title) in React components.
    - Installation:

        ```bash
        npm install react-helmet
        ```

    - Usage:

        ```jsx
        import { Helmet } from 'react-helmet';

        function MyComponent() {
            return (
                <div>
                    <Helmet>
                        <title>My Page Title</title>
                        <meta
                            name='description'
                            content='My page description'
                        />
                    </Helmet>
                    <h1>Welcome to My Page</h1>
                </div>
            );
        }
        ```

4. **Canonical Links**
   :

    - Canonical links help search engines understand the preferred URL for a page.
    - You can set canonical links using React Helmet.

    ```jsx
    <Helmet>
        <link
            rel='canonical'
            href='https://www.example.com/my-page'
        />
    </Helmet>
    ```

5. **Structured Data**
   :

    - Adding _structured data_ (JSON-LD) helps search engines better understand your content.
    - You can use React Helmet to include JSON-LD scripts.

    ```jsx
    <Helmet>
        <script type='application/ld+json'>
            {JSON.stringify({
                '@context': 'https://schema.org',
                '@type': 'WebPage',
                name: 'My Page',
                url: 'https://www.example.com/my-page',
            })}
        </script>
    </Helmet>
    ```

6. **Sitemap and Robots.txt**
   :

    - _Sitemaps_ help search engines find and index all pages of your site.
    - _robots.txt_ guides search engines on which pages to crawl.
    - You can generate a sitemap using tools or manually, and host it on your server.
    - Example robots.txt:

        ```plaintext
        User-agent: \*
        Disallow: /private/
        ```

7. **Performance Optimization**
   :

    - _Fast-loading_ pages improve user experience and SEO.
    - Techniques:
        - Code splitting and lazy loading.
        - Optimizing images.
        - Using a CDN.

8. **Meta Tags and Content**
   :

    - Ensure each page has unique and descriptive meta tags (`title`, `description`, `keywords`).
    - Use meaningful and descriptive content, including keywords relevant to your content.

---

### [<p style='color:rgb(189, 195, 199);'>React Hooks</p>](#hooks)

React Hooks are a new addition to React that allows you to use state and other React features without writing a class. They are a way to reuse stateful logic without changing your component hierarchy.

### [<p style='color:rgb(189, 195, 199);'>Props</p>](#props)

Props are the data passed into a component from its parent component. They are used to customize the component's behavior and appearance.

---

# Getting Started with React

### System Configuration

The `create-react-app` tool can be used as it provides a modern build setup allowing to create and run React applications with minimal configuration. The create-react-app is a command-line interface (CLI).

To install create-react-app, following are the steps:

1. Install node.js with version 14+ from Software House or Node.js official site.

You can check the node version installed in your machine by running the following command that displays the node version as follows:

node -v
(The expected output should be similar to v17.2.0)

2. Install create-react-app by running the following command:

npm install -g create-react-app 3. Once the installation is done, create a React app using the below command:

create-react-app my-app

The above command creates a project my-app with the below folder structure:

​​​​​​​​​​​​​​If you do not want to install create-react-app then you can use the below command to create a React application

D:\>npx create-react-app my-app
npx is a tool to run node packages without installing binaries
