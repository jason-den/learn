### Fundamental

#### Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.

All the above-mentioned technologies are key-value storage mechanisms on the client side. They are only able to store values as strings.

|                                        | `cookie`                                                 | `localStorage` | `sessionStorage` |
| -------------------------------------- | -------------------------------------------------------- | -------------- | ---------------- |
| Initiator                              | Client or server. Server can use `Set-Cookie` header     | Client         | Client           |
| Expiry                                 | Manually set                                             | Forever        | On tab close     |
| Persistent across browser sessions     | Depends on whether expiration is set                     | Yes            | No               |
| Sent to server with every HTTP request | Cookies are automatically being sent via `Cookie` header | No             | No               |
| Capacity (per domain)                  | 4kb                                                      | **5MB**        | 5MB              |
| Accessibility                          | Any window                                               | Any window     | Same tab         |

> Note: If the user decides to **clear browsing data** via whatever mechanism provided by the browser, this will clear out any `cookie`, `localStorage`, or `sessionStorage` stored. It's important to keep this in mind when designing for local persistance, especially when comparing to alternatives such as server side storing in a database or similar (which of course will persist despite user actions).

- https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
- http://tutorial.techaltum.com/local-and-session-storage.html

#### Describe the difference between `<script>`, `<script async>` and `<script defer>`.

- `<script>` - **HTML parsing is blocked**, the script is fetched and executed immediately, HTML parsing **resumes after the script is executed**.
- `<script async>` - The script will be fetched in parallel to HTML parsing and executed as soon as it is available (potentially before HTML parsing completes). Use `async` when the script is independent of any other scripts on the page, for example, analytics.
- `<script defer>` - **The script will be fetched in parallel to HTML parsing** and **executed when the page has finished parsing**. If there are multiple of them, each deferred script is executed in the order they were encoun­tered in the document. **If a script relies on a fully-parsed DOM, the `defer` attribute will be useful in ensuring that the HTML is fully parsed before executing**. **There's not much difference in putting a normal `<script>` at the end of `<body>`.** A deferred script must not contain `document.write`.

Note: The `async` and `defer` attrib­utes are ignored for scripts **that have no `src` attribute.**



- http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html
- https://stackoverflow.com/questions/10808109/script-tag-async-defer
- https://bitsofco.de/async-vs-defer/



### progressive rendering

#### What is progressive rendering?

> Concept is clear. But practice seems not have a clear boundary or checklist.

It is the name given to techniques used to improve the **performance of a webpage** (in particular, improve perceived load time) to **render content for display as quickly as possible.**

It used to be much more prevalent in the days before broadband internet but it is still used in modern development as mobile data connections are becoming increasingly popular (and unreliable)!

Examples of such techniques:

- **Lazy loading of images** - Images on the page are not loaded all at once. JavaScript will be used to load an image when the user scrolls into the part of the page that displays the image.
- **Prioritizing visible content** (or above-the-fold rendering) - Include only the minimum CSS/content/scripts necessary for the amount of page that would be rendered in the users browser first to display as quickly as possible, you can then use deferred scripts or listen for the `DOMContentLoaded`/`load` event to load in other resources and content.
- **Async HTML fragments** - Flushing parts of the HTML to the browser as the page is constructed on the back end. More details on the technique can be found [here](http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/).



- https://stackoverflow.com/questions/33651166/what-is-progressive-rendering
- http://www.ebaytechblog.com/2014/12/08/async-fragments-rediscovering-progressive-html-rendering-with-marko/



#### Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?

**Placing `<link>`s in the `<head>`**

> Good practice. Basically no excaption.

Putting `<link>`s in the `<head>` is part of proper specification in building an optimized website. When a page first loads, HTML and CSS are being parsed simultaneously; HTML creates the DOM (Document Object Model) and CSS creates the CSSOM (CSS Object Model). Both are needed to create the visuals in a website, allowing for a quick "**first meaningful paint**" timing. This **progressive rendering** is a category optimization sites are measured in their performance scores. Putting stylesheets near the bottom of the document is what prohibits progressive rendering in many browsers. Some browsers block rendering to avoid having to repaint elements of the page if their styles change. The user is then stuck viewing a blank white page. Other times there can be **flashes of unstyled content (FOUC)**, which show a webpage with no styling applied.

**Placing `<script>`s just before `</body>`**

> Depends on whether the script need to `document.write()`. 
>
> > but these days it's not a good practice to use `document.write()`

`<script>`  tags block HTML parsing while they are being downloaded and executed which can slow down your page. Placing the scripts at the bottom will allow the HTML to be parsed and displayed to the user first.

An exception for positioning of `<script>`s at the bottom is when your script contains `document.write()`, but these days it's not a good practice to use `document.write()`. 

Also, placing `<script>`s at the bottom means that the browser cannot start downloading the scripts until the entire document is parsed. This ensures your code that needs to manipulate DOM elements will not throw an error and halt the entire script. If you need to put `<script>` in the `<head>`, use the `defer` attribute, which will **achieve the same effect of downloading and running the script only after the HTML is parsed**.

Keep in mind that putting scripts just before the closing `</body>` tag will create the **illusion that the page loads faster on an empty cache** (since the scripts won't block downloading the rest of the document). However, if you have some code you want to run during page load, it will only start executing after the entire page has loaded. If you put those scripts in the `<head>` tag, they would start executing before - so on a primed cache the page would actually appear to load faster.



### Server side rendering

#### Have you used different HTML templating languages before?

Yes, Pug (with express), Jinja (with Django). 

In my opinion, they are more or less the same and provide similar functionality of escaping content and helpful filters for manipulating the data to be displayed. Most templating engines will also allow you to inject your own filters in the event you need custom processing before display.





### Tags / elements



#### What are empty elements in HTML? [Ref](https://developer.mozilla.org/en-US/docs/Glossary/Empty_element)

An **empty element** is an [element](https://developer.mozilla.org/en-US/docs/Glossary/Element) from HTML, SVG, or MathML that **cannot** have any child nodes (i.e., nested elements or text nodes).

> The [HTML](https://html.spec.whatwg.org/multipage/), [SVG](https://www.w3.org/TR/SVG2/), and [MathML](https://www.w3.org/TR/MathML3/) specifications define very precisely what each element can contain. 
>
> Many combinations have no semantic meaning, for example an `audio` element nested inside an `<hr>` element
>
> In HTML, using a closing tag on an empty element is usually invalid. For example, `<input type="text"></input>` is invalid HTML.



#### `<img/>` - Why you would use a `srcset` attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.

You would use the `srcset` attribute when you want to serve different images to users depending on their device display width - serve higher quality images to devices with retina display enhances the user experience while serving lower resolution images to low-end devices increase performance and decrease data wastage (because serving a larger image will not have any visible difference). For example: `<img srcset="small.jpg 500w, medium.jpg 1000w, large.jpg 2000w" src="..." alt="">` tells the browser to display the small, medium or large `.jpg` graphic depending on the client's resolution. The first value is the image name and the second is the width of the image in pixels. For a device width of 320px, the following calculations are made:

- 500 / 320 = 1.5625
- 1000 / 320 = 3.125
- 2000 / 320 = 6.25

If the client's resolution is 1x, 1.5625 is the closest, and `500w` corresponding to `small.jpg` will be selected by the browser.

If the resolution is retina (2x), the browser will use the closest resolution above the minimum. Meaning it will not choose the 500w (1.5625) because it is greater than 1 and the image might look bad. The browser would then choose the image with a resulting ratio closer to 2 which is 1000w (3.125).

`srcset`s solve the problem whereby you want to serve smaller image files to narrow screen devices, as they don't need huge images like desktop displays do — and also optionally that you want to serve different resolution images to high density/low-density screens.

###### 

- https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images
- https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/



### HTML5, HTML

#### What does a `doctype` do?

first try:

I think it’s a declaration of HTML version (protocol) and thus what feature it requires.

feedback back based on Example Answer:

Exactly, The DOCTYPE declaration for the HTML5 standards is `<!DOCTYPE html>`. And nowadays it’s the only option that we normally care about. 

> **DOCTYPE** is an abbreviation for **DOCument TYPE**. A DOCTYPE is always associated to a **DTD** - for **Document Type Definition**.
>
> A DTD defines how documents of a certain type should be structured (i.e. a `button` can contain a `span` but not a `div`), whereas a DOCTYPE declares what DTD a document *supposedly* respects (i.e. this document respects the HTML DTD).
>
> For webpages, the DOCTYPE declaration is required. It is used to tell user agents what version of the HTML specifications your document respects. Once a user agent has recognized a correct DOCTYPE, it will trigger the **no-quirks mode** matching this DOCTYPE for reading the document. If a user agent doesn't recognize a correct DOCTYPE, it will trigger the **quirks mode**.
>
> > **quirks mode** is “backward compatibility with older webpages”

#### Consider HTML5 as an open web platform. What are the building blocks of HTML5?

- Semantics - Allowing you to describe more precisely what your content is.
- Connectivity - Allowing you to communicate with the server in new and innovative ways.
- **Offline and storage** - Allowing webpages to store data on the client-side locally and operate offline more efficiently.
- Multimedia - Making **video and audio first-class citizens** in the Open Web.
- 2D/3D graphics and effects - Allowing a much more diverse range of presentation options.
- Performance and integration - Providing greater speed optimization and better usage of computer hardware.
- Device access - Allowing for the usage of various input and output devices.
- Styling - Letting authors write more sophisticated themes.

- https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5



#### Others

##### Open Web?



### Advanced features

#### `canvas` and `svg`?

> Ref:  [css-tricks](https://css-tricks.com/when-to-use-svg-vs-when-to-use-canvas/),  [stackoverflow](https://stackoverflow.com/questions/5882716/html5-canvas-vs-svg-vs-div)
>
> [SVG is the default choice; canvas is the backup](https://twitter.com/bdc/status/1179509488803434496?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1179509488803434496%7Ctwgr%5E%7Ctwcon%5Es1_c10&ref_url=https%3A%2F%2Fcss-tricks.com%2Fwhen-to-use-svg-vs-when-to-use-canvas%2F)

##### The short answer

SVG would be *easier* for you, since **selection** and **moving** it around **is already built in**. SVG objects are DOM objects, so they have "click" handlers, etc.

DIVs are okay but clunky and have *awful* performance loading at large numbers.

Canvas has the best performance hands-down, but you have to implement all concepts of managed state (object selection, etc) yourself, or use a library.

- SVG is probably better for applications and apps with few items (less than 1000? Depends really)
- Canvas is better for thousands of objects and careful manipulation, but a lot more code (or a library) is needed to get it off the ground.
- HTML Divs are clunky and do not scale, making a circle is only possible with rounded corners, making complex shapes is possible but involves hundreds of tiny tiny pixel-wide divs. Madness ensues.

##### The long answer:

HTML5 Canvas is simply a drawing surface for a bit-map. You set up to draw (Say with a color and line thickness), draw that thing, and then the Canvas has no knowledge of that thing: It doesn't know where it is or what it is that you've just drawn, it's just pixels. If you want to draw rectangles and have them move around or be selectable then you have to code all of that from scratch, **including** the code to remember that you drew them.

SVG on the other hand must maintain references to each object that it renders. Every SVG/VML element you create is a real element in the DOM. By default this allows you to keep much better track of the elements you create and makes dealing with things like mouse events easier by default, but it slows down significantly when there are a large number of objects

…….

### Duplicated 

#### What are `data-` attributes good for?

Before JavaScript frameworks became popular, front end developers used `data-` attributes to store extra data within the DOM itself, without other hacks such as non-standard attributes, extra properties on the DOM. It is intended to store custom data private to the page or application, for which there are no more appropriate attributes or elements.

These days, using `data-` attributes is generally **not encouraged**. One reason is that users can modify the data attribute easily by using inspect element in the browser. **The data model is better stored within JavaScript itself and stay updated with the DOM via data binding possibly through a library or a framework**.

However, **one perfectly valid use of data attributes, is to add a hook for *end to end* testing frameworks such as Selenium and Capybara without having to create a meaningless classes or ID attributes.** The element needs a way to be found by a particular Selenium spec and something like `data-selector='the-thing'` is a valid way to do so without convoluting the semantic markup otherwise.

References

- http://html5doctor.com/html5-custom-data-attributes/
- https://www.w3.org/TR/html5/dom.html#embedding-custom-non-visible-data-with-the-data-*-attributes




### multilingual sites

#### How do you serve a page with content in multiple languages?

> I will assume that it is asking about the most common case, which is how to serve a page with content available in multiple languages, but the content within the page should be displayed only in one consistent language.

When an HTTP request is made to a server, the requesting user agent usually sends information about language preferences, such as in the `Accept-Language` header. 

The server can then use this information to return a version of the document in the appropriate language if such an alternative is available. The returned HTML document should also declare the `lang` attribute in the `<html>` tag, such as `<html lang="en">...</html>`.

> But this only apply for server side redering? Alright, we can trigger that by a switch on language.

Of course this is useless for letting a search engine know that the same content is available in different languages, and so you must also make use of the **`hreflang` attribute in the `<head>`.** Eg. `<link rel="alternate" hreflang="de" href="http://de.example.com/page.html" />`

In the back end, the HTML markup will contain `i18n` placeholders and content for the specific language stored in YML or JSON formats. The **server then dynamically generates the HTML page with content in that particular language**, usually with the help of a back end framework.

#### What kind of things must you be wary of when designing or developing for multilingual sites?

