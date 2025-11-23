	TTFB - time to first byte

## Navigation

- DNS lookup
- TCP handshake
- TLS negotiation

## Response

Once we have an established connection to a web server, the browser sends an initial [HTTP `GET` request](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods) on behalf of the user, which for websites is most often an HTML file. Once the server receives the request, it will reply with relevant response headers and the contents of the HTML.

This response for this initial request contains the first byte of data received. [Time to First Byte](https://developer.mozilla.org/en-US/docs/Glossary/Time_to_first_byte) (TTFB) is the time between when the user made the request — say by clicking on a link — and the receipt of this first packet of HTML. The first chunk of content is usually 14KB of data.

TCP packets are split into segments during transmission. Because TCP guarantees the sequence of packets, the server must receive an acknowledgment from the client in the form of an ACK packet after sending a certain number of segments.
## Parsing

[Parsing](https://developer.mozilla.org/en-US/docs/Glossary/Parse) is the step the browser takes to turn the data it receives over the network into the [DOM](https://developer.mozilla.org/en-US/docs/Glossary/DOM) and [CSSOM](https://developer.mozilla.org/en-US/docs/Glossary/CSSOM), which is used by the renderer to paint a page to the screen.

Even if the requested page's HTML is larger than **the initial 14KB packet**, the browser will begin parsing and attempting to render an experience based on the data it has. This is why it's important for web performance optimization to include everything the browser needs to start rendering a page, or at least a template of the page — the CSS and HTML needed for the first render — **in the first 14KB**. But before anything is rendered to the screen, the HTML, CSS, and JavaScript have to be parsed.

### Building the DOM Tree

**The first step is processing the HTML markup and building the DOM tree**. HTML parsing involves **[tokenization](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList) and tree construction**. HTML tokens include start and end tags, as well as attribute names and values. If the document is well-formed, parsing it is straightforward and faster. The parser parses tokenized input into the document, building up the document tree.
### Preload Scanner

While the browser builds the DOM tree, this process occupies the main thread. As this happens, **the _preload scanner_ will parse through the content available and request high-priority resources** like CSS, JavaScript, and web fonts. Thanks to the preload scanner, we don't have to wait until the parser finds a reference to an external resource to request it. It will retrieve resources in the background so that by the time the main HTML parser reaches the requested assets, they may already be in flight or have been downloaded. The optimizations the preload scanner provides reduce blockages.
### Building CSSOM Tree

The second step in the critical rendering path is **processing CSS and building the CSSOM tree**. The CSS object model is similar to the DOM. The DOM and CSSOM are both trees. They are independent data structures. The browser converts the CSS rules into a map of styles it can understand and work with. The browser goes through each rule set in the CSS, creating a tree of nodes with parent, child, and sibling relationships based on the CSS selectors.

Building the CSSOM is very, very fast, and **this build time information is not displayed in the developer tools**. Rather, the "Recalculate Style" in developer tools shows the total time it takes to parse CSS, construct the CSSOM tree, and recursively calculate computed styles. In terms of web performance, there are many better ways to invest optimization effort, as **the total time to create the CSSOM is generally less than the time it takes for one DNS lookup**.

### JavaScript Compilation

**While the CSS is being parsed and the CSSOM created**, other assets, including JavaScript files, are downloading (thanks to the preload scanner). **JavaScript is parsed, compiled, and interpreted**. The scripts are parsed into abstract syntax trees. Some browser engines take the [abstract syntax trees](https://en.wikipedia.org/wiki/Abstract_Syntax_Tree) and pass them into a compiler, outputting bytecode. This is known as JavaScript compilation. **Most of the code is interpreted on the main thread, but there are exceptions such as code run in [web workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)**.

### Building the Accessibility Tree

The browser also builds an [accessibility](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility) tree that assistive devices use to parse and interpret content. The accessibility object model (AOM) is like a semantic version of the DOM. **The browser updates the accessibility tree when the DOM is updated**. The accessibility tree is not modifiable by assistive technologies themselves.

## Render

Rendering steps include **style, layout, paint, and in some cases compositing**. The CSSOM and DOM trees created in the parsing step are combined into a render tree which is then used to compute the layout of every visible element, which is then painted to the screen. In some cases, content can be promoted to its own layer and composited, improving performance by painting portions of the screen on the GPU instead of the CPU, freeing up the main thread.

### Style

The third step in the critical rendering path is combining the DOM and CSSOM into a render tree. The **computed style tree**, or **render tree**, construction starts with the root of the DOM tree, traversing each visible node.

Each visible node has its CSSOM rules applied to it. The render tree holds all the visible nodes with content and computed styles — matching up all the relevant styles to every visible node in the DOM tree, and determining, based on the [CSS cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_cascade/Cascade), what the computed styles are for each node.

### Layout

_Layout_ is the process by which **the dimensions and location of all the nodes in the render tree are determined, plus the determination of the size and position of each object on the page**. **_Reflow_** is any subsequent size and position determination of any part of the page or the entire document.

Once the render tree is built, layout commences. **The render tree identified which nodes are displayed (even if invisible) along with their computed styles, but not the dimensions or location of each node**. To determine the exact size and position of each object, the browser starts at the root of the render tree and traverses it.

The first time the size and position of each node is determined is called _layout_. Subsequent recalculations of are called **_reflows_**. In our example, suppose the initial layout occurs before the image is returned. Since we didn't declare the dimensions of our image, there will be a reflow once the image dimensions are known.

### Paint

**The last step in the critical rendering path is painting the individual nodes to the screen, the first occurrence of which is called the [first Meaningful Paint](https://developer.mozilla.org/en-US/docs/Glossary/First_meaningful_paint)**. In the **painting or rasterization** phase, the browser converts each box calculated in the layout phase to actual pixels on the screen. Painting involves drawing every visual part of an element to the screen, including text, colors, borders, shadows, and replaced elements like buttons and images. The browser needs to do this super quickly.

To ensure smooth scrolling and animation, everything occupying the main thread, including calculating styles, along with reflow and paint, must take the browser less than 16.67ms to accomplish. At 2048 x 1536, the iPad has over 3,145,000 pixels to be painted to the screen. That is a lot of pixels that have to be painted very quickly. To ensure repainting can be done even faster than the initial paint, the drawing to the screen is generally broken down into several layers. If this occurs, then compositing is necessary.

Painting can **break the elements in the layout tree into layers**. Promoting content into layers on the GPU (instead of the main thread on the CPU) improves paint and repaint performance. There are specific properties and elements that instantiate a layer, including [`<video>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/video) and [`<canvas>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/canvas), and any element which has the CSS properties of [`opacity`](https://developer.mozilla.org/en-US/docs/Web/CSS/opacity), a 3D [`transform`](https://developer.mozilla.org/en-US/docs/Web/CSS/transform), [`will-change`](https://developer.mozilla.org/en-US/docs/Web/CSS/will-change), and a few others. These nodes will be painted onto their own layer, along with their descendants, unless a descendant necessitates its own layer for one (or more) of the above reasons.

**Layers do improve performance but are expensive** when it comes to memory management, so should not be overused as part of web performance optimization strategies.

### Compositing

When sections of the document are **drawn in different layers**, overlapping each other, compositing is necessary to **ensure they are drawn to the screen in the right order** and the content is rendered correctly.

As the page continues to load assets, **reflows can happen** (recall our example image that arrived late). A **reflow sparks a repaint and a re-composite**. Had we defined the dimensions of our image, no reflow would have been necessary, and only the layer that needed to be repainted would be repainted, and composited if necessary. But we didn't include the image dimensions! When the image is obtained from the server, **the rendering process goes back to the layout steps and restarts from there**.

## Interactivity

Once the main thread is done painting the page, you would think we would be "all set." That isn't necessarily the case. If the load includes JavaScript, that was correctly deferred, and only executed after the [`onload`](https://developer.mozilla.org/en-US/docs/Web/API/Window/load_event) event fires, **the main thread might be busy**, and not available for scrolling, touch, and other interactions.

[Time to Interactive](https://developer.mozilla.org/en-US/docs/Glossary/Time_to_interactive) (TTI) is the measurement of how long it took from that first request which led to the DNS lookup and TCP connection to when the page is interactive — interactive being the point in time after the [First Contentful Paint](https://developer.mozilla.org/en-US/docs/Glossary/First_contentful_paint) when the page responds to user interactions within 50ms. **If the main thread is occupied parsing, compiling, and executing JavaScript**, it is not available and therefore not able to respond to user interactions in a timely (less than 50ms) fashion.