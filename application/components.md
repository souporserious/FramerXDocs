# Components

## Conceptual

Components are like legos for your interface. They are small building blocks that you can compose into larger ones, making up entire screens, interfaces and apps.

As a designer, you might have different definitions of components as most visual tools treat components as pictures of real components. In Framer X, the components are all real. They scroll, click, move and handle input, all backed by the popular React JavaScript framework for building interfaces.

_PS: Please Lego don't sue me for this analogy._

## Types of Components

Framer X has two types of components, which it treats the same because they ultimately are the same under the hood: React components:

* **Design components** – components that you draw on the canvas consisting of visual and basic interaction that you can express on the canvas. Everyone can build these. Design components are fully editable on the canvas.
* **Code components** – components that are backed by code with React. They can be anything from simple HTML and CSS all the way to advanced JavaScript, optionally building on other libraries again. Code component are only editable from code, but they can display other Frames from the canvas via the children prop or canvas imports \(more below\).

Any component can be displayed on the canvas, but interactive components \(like scroll or something with a click\) only work in the Preview. Both design and code components can be composed into any hierarchy on the canvas, design components can even contain code components, and every component has the same automatic layout options as any Frame.

A Framer X project lists all components in that specific project under the Components tab on the left. The components can origin from:

* Your project canvas \(design components\).
* Your project code \(code components\).
* Installed packages \(either types\).

The rest of this page will focus on creating your own code components.

## Requirements

Before you begin writing components, make sure you have an editor installed as Framer X does not come with a built in editor. Any editor that supports TypeScript will do, but we really like VSCode.

[Read more about setting up your code editor.](./#setup-and-workflow)

_Note: Framer X Beta 1 only supports TypeScript but the general release will support plain ES6 too._

## React Components

As code components are just [React](https://reactjs.org/) components, it is useful to understand the bare basics of React, but not truly needed. As React components use [JSX](https://reactjs.org/docs/introducing-jsx.html) \(an HTML like markup language\) you can already write a component with just basic web development skills. Let's look at an example.

```typescript
import * as React from "react";
​
export class Example extends React.Component {
  render() {
    return <div style={{color: "blue"}}>Hello World!</div>
  }
}
```

This is the most basic React component. If you squint and look past the boilerplate \(like import and class\) you'll notice the render\(\) method returning something that looks a lot like HTML and CSS. Let's make it a bit more advanced and see if you can still recognize it.

```typescript
import * as React from "react";

export class Example extends React.Component {
  render() {
    return (
      <div style={{ color: "blue" }}>
        <h1>Hello World</h1>
        <p>
          Lorem ipsum
          <span onClick={() => alert("Hi")}>Click Me</span>
        </p>
      </div>
    );
  }
}
```

This should look very familiar if you have done web development before, and it's a full blown React component. From here, I would recommend to continue to learn React from their [excellent documentation](http://reactjs.com).

## Creating a Code Component

To create a new code component, go to the Components panel \(left side of the window\) and click "Create Component". Then, select "from Code", pick a name \(no spaces\) and click create.

If you have an editor installed, it should now open up with a new boilerplate component which is purple and says "hello world". Go back to the Components panel in Framer X and drag a few onto the canvas. Note that they can have different positions and sizes. Every component on the canvas is an _instance_ of the code component.

Go back to your editor and change anything like the CSS or the hello world text. When you save the code file, you'll see that Framer automatically updates every instance to reflect the changes.

## Canvas Behavior

Components fully behave like you would expect in the Preview, but a bit different on the canvas. For example, scrolling and click handlers don't do anything on the canvas, as that would not mix well with manipulating and tools.

### Layout and Sizing

Every component rendered on the canvas or preview is wrapped in a Frame so they have the same layout rules as anything else on the canvas. Both the width and height are passed to the code component as props so you can use them.

```typescript
import * as React from "react";

export class Example extends React.Component<{width:number, height: number}> {
  render() {
    return (
      <div>
        {this.props.width} x {this.props.height}
      </div>
    );
  }
}
```

_Note: the TypeScript type annotations \(width, height\) are optional, but nice._

### Displaying Canvas Elements

Because the code determines the contents of code components, you cannot directly edit code component contents on the canvas. But often you'd like a code component to display something else from your canvas. For example, a Card component could render an image with some overlay that is somewhere else on your canvas. You can accomplish this in two ways.

#### Using props.children

React props are basically the attributes for a component to display, and one of those is a list of children, or it's contents \(like in the DOM or you see in the layer panel\). Normally these are determined from your code, but in Framer you can set any Frame on your canvas as children for your component. Let's look at an example.

```typescript
import * as React from "react";

export class Example extends React.Component<{width:number, height: number}> {
  render() {
    return (
      <div style={{width: this.props.width, height: this.props.height}}>
        <h1>Hello</h1>
        {this.props.children}
      </div>
    );
  }
}
```

Framer detects you are using the props.children property in your render method and automatically adds a connector to each instance of the component on your canvas \(a purple dot on the right side, like the scroll tool\). You can drag a connection from this connector to any Frame on the canvas and it will use it as its children to render.

_Hint: you can even override the props for the children by using React.Children.Map and React.Children.cloneElement methods._

#### Using canvas imports

WIP: not in Beta 1. Basically import any design component from code by name.

## Adding Framer Interface for Props

You can describe a custom interface for your components so component consumers can configure them on the canvas. The only thing you have to do is add a static `propertyControls` method to your class with a descriptor. It will use `defaultProps` for the defaults and try to type check your descriptors if you added type annotations for your props.

The example below is an excerpt of our iOS Alert component using a color, string and boolean control.

```typescript
import * as React from "react"
import { PropertyControls, ControlType } from "framer"

interface Props {
    title: string
    tintColor: string
    dimOverlay: boolean
}

export class Example extends React.Component<Partial<Props>> {

    static defaultProps = {
        title: "A short description of the actions goes here.",
        tintColor: "#007AFF",
        dimOverlay: true,
    }

    static propertyControls: PropertyControls<Props> = {
        title: { type: ControlType.String, title: "Title" },
        tintColor: { type: ControlType.Color, title: "Tint" },
        dimOverlay: { type: ControlType.Boolean, disabled: "Hide", enabled: "Show", title: "DimOverlay" },
    }

    render() { ... }
}
```

## Using the Framer Library

React components can do pretty much anything, but React itself is purely focused on composing interfaces from components. To do anything else, from managing application state to drawing graphs, it is very common to leverage other libraries.

The main use case of Framer X is prototyping, which typically includes flows, scrolling, animations and gestures. Framer X includes an optional library of helpers called Framer.js for these tasks. Using these is not required, you can use anything you like, but they should make interactive prototyping more enjoyable in most cases.

[Learn more about how to use the Framer.js library.](framer.js-library/animation.md)

## Using External Libraries

WIP, not in Beta 1. But you can find hints in the package guide.

## Using Asset from Components

WIP, not in Beta 1.

## Editing Components from Packages

WIP, not in Beta 1.
