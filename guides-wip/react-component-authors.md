---
description: How to optimize your external React components for usage in Framer.
---

# React Component Authors \(WIP\_

* How we render components on the canvas
  * Container `Frame`
  * The `width` and `height` props.
* Limitations
  * iframes on the canvas are blocked
  * limited execution time for render methods
  * other planned limitations \(sandboxing\)
* Framer X experience for component consumers
  * Expose props directly in the interface with controlTypes: string, number, color \(optionally with HoC\).
* Specific topics
  * Events
    * Blocked on the canvas, working in the preview
    * Should account for preview scale \(css transform\)
  * Styling
    * Inline styling preferred, but everything else should work, we might limit inserting arbitrary css \(glamour, styled components\) in the future.
* Publishing existing components to our store
  * Anatomy of a package \(zipped js project with package.json\)
  * Add your components as a dependency
  * Expose components you'd like to expose
  * Optionally add interface \(see above\)
  * ES6 vs TypeScript \(and optional types\)



