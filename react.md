# React

# Summary
Frontend JavaScript library for building UI based on components. Primarily used
for creating *single page applications*, but can also be used for server-side
rendering applications with frameworks like Next.js.

React manages state and renders it to the DOM.

# Example Application
This is an example of the React code, written in a .jsx file:

    import React from 'react'
    import ReactDOM from 'react-dom/client'

    const HelloWorld = () => {
        return {
            <h1>Hello, World!</h1>
        }
    }

    const App = () => {
        return <HelloWorld />
    }

    ReactDOM.createRoot(document.getElementById('root')).render(
        <React.StrictMode>
            <App />
        </React.StrictMode>
    )

This document produces the following HTML output:

    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="utf-8" />
        <title>React App</title>
    </head>

    <body>
        <noscript>You need to enable JavaScript to run this app.</noscript>
        <div id="root">
            <h1>Hello, World!</h1>
        </div>
    </body>
    </html>

# Components
React apps are made of components - reusable UI elements. They are formed in the
src/ folder and are rendered to the DOM with the ReactDOM library.
Example of a component:

    import React from 'react'
    import Tool from './Tool'

    const Example = () => {
        return (
            <>
                <div>
                    <Tool name="John" />
                </div>
            </>
        )
    }

    export default Example

# Functional and Class-based components
The two primary ways of declaring components in JS are:
* Functional: `const Greeter = () => <div>Hello!</div>`
* Class-based:

    class ParentComponent extends React.Component {
        state = { color: '#00ff00' }

        render() {
            return (
                <ChildComponent color={this.state.color} />
            )
        }
    }