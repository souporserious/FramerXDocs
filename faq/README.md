# FAQ

## Can I buy Framer X today?

Your current [individual Framer subscription](http://framer.com/pricing) will be valid for Framer X too so you can buy a subscription today, but you will still have to be invited. People with a subscription do get it before anyone else.

## Will there be a Windows version?

We are currently working on Framer X for Windows, but it is decoupled from the beta so we can get it in your hands as fast as possible. [Sign up here](https://framer.com/forms/windows/) and we'll keep you updated.

## Can Framer X do what I did in Framer?

Yes, even better. But the current beta does [not include all functionality](introduction/beta.md#feature-overview) yet because we're still working on some code features. They will land in the next beta versions.

## Will Framer X be TypeScript based?

We aim to support both TypeScript and plain ES6 on release.

## What kind of code does Framer X generate?

The point of Framer X is not to generate code for you but use the code you \(or someone else\) wrote to compose interfaces.

## Can I beta test the private store for my company?

We're still working on the private store. If you'd like to test early, contact our enterprise team via the form on the [Framer X](https://framer.com/x) site.

## Can I use React stateless components?

You can, we just use `React.Component` in the docs not to confuse beginners by mixing the two. If you are a beginner who is now curious [read this](https://reactjs.org/docs/components-and-props.html).

## How do I style React components?

However you like. We prefer inline styles, but everything from Styled Components to Glamour should work.

## How do I see the package contents?

Framer projects are zipped JavaScript files with a `package.json` that temporarily get extracted while your project is open. You can reveal the contents with `File > Show Package`.

## How can I use external npm libraries?

This is still very fragile but you can open a Framer X project, `File > Show Package` and use the terminal to use `yarn add <package>` .

Any Framer store package lives under the `@framer` namespace. Every other package name will be proxied through to public npm.

## Can I use multiple canvas children from my code component?

You can currently only access `props.children` but we're working on better ways to mix code and canvas.

## Can I use Framer X projects with Git?

Right now, packages are binary zipped files and not great for Git. We're looking to improve that in the future and we think we can, because Git is smart.

## What will happen to Framer Studio?

We will keep supporting and updating Framer Studio once we release Framer X so that you can continue to open and edit all your previous projects, but our main focus will shift towards Framer X.



