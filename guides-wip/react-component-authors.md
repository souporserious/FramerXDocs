# React Component Authors

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
    * Media queries only work well in the preview, as the canvas lives in an entire window by itself, so queries respond to the whole window instead of the root Frame \(artboard\). 
* Publishing existing components to our store
  * Anatomy of a package \(zipped js project with package.json\)
  * Add your components as a dependency
  * Expose components you'd like to expose
  * Optionally add interface \(see above\)
  * ES6 vs TypeScript \(and optional types\)



