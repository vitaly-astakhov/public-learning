# Rendering path

## Materials

- [The Rendering Critical Path [chromium]](https://www.chromium.org/developers/the-rendering-critical-path/)
- [Understanding the critical path [web.dev]](https://web.dev/learn/performance/understanding-the-critical-path)
- [Critical Rendering Path [web.dev]](https://web.dev/articles/critical-rendering-path)

___

The rendering path involves the following steps:

- Constructing the Document Object Model (DOM) from the HTML.
- Constructing the CSS Object Model (CSSOM) from the CSS.
- Applying any JavaScript that alters the DOM or CSSOM.
- Constructing the render tree from the DOM and CSSOM.
- Perform style and layout operations on the page to see what elements fit where.
- Paint the pixels of the elements in memory.
- Composite the pixels if any of them overlap.
- Physically draw all the resulting pixels to screen.

![Rendering path](../../assets/rendering-path.svg)
