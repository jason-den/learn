> Credit - [w3school css exercise](https://www.w3schools.com/css/exercise.asp)

## Syntax, config, and meta FAQ

![CSS selector](https://raw.githubusercontent.com/jason-den/picture-storage/master/2022-10/img_selector.gif)

### Where to place the style

1. Add an **external** style sheet with the URL: "mystyle.css".

```html
<text type="stylesheet" src="mystyle.css" /> # my answer 
<link rel="stylesheet" href="mystyle.css" /> # correct answer
```

2. Set "background-color: linen" for the page, using an **internal** style sheet.

```html
<head>
  <style>
    body {background-color: linen;}
  </style>
</head>
```

3. Set "background-color: linen" for the page, using an **inline** style.

```html
<body style="background-color: linen">
  <h1>This is a Heading</h1>
  <p>This is a paragraph.</p>
  <p>This is another paragraph.</p>
</body>
```



## Selector

1. select all **element** `p` : `p {color: red;}`

2. select **id** `para1` : `#para1 {color: red;}`

3. select all elements with class `colortext` : `.colortext {color: red;}`

4. Change the color of all <p> and <h1> elements, to "red". Group the selectors to minimize code.

   `h1, p {color: red;}`

### Combinators


- Change the color of all <p> elements, that are **descendants** of <div> elements, to "red". 

  ```css
  div p { color: red; }
  ```
  
  > note that, `div, p` selects both `div` and `p`.  Here, `div p` means `p` inside `div`.
  
- Change the color of all <p> elements, that are **immediate children** of <div> elements, to "red". 

  ```css
  div>p { color: red; }
  ```
  
- Change the color of the first <p> element that is directly **after** <div> elements, to "red". 

  ```css
  div+p { color: red; }
  ```
  
- Change the color of <p> elements, that are the siblings of a <div> element, to "red". 

  ```css
  div ~ p { color: red; }
  ```

### Attribute Selectors


- Set the background-color to "lightblue" for elements with a "target" attribute.

  ```css
  [target] { backgroud-color: lightblue; } /* my guess */
  a[target] { background-color: lightblue; } /* correct answer */
  ```

  > Note that  there is no space in `a[target]` 

- Set the background-color to "lightblue" for elements with an attribute like: target="_blank" 

  ```css
  a[target="_blank"] {background-color: lightblue;}
  ```

- Set a border with the color "red", around elements with a **"title" attribute containing the word "red"**. 

  ```css
  img[title??'red'] { border: red; } /* I don't know how to specify "containing" */ 
  img[title~="red"] { border: 5px solid red; } /* correct answer */
  ```

- Set a border with the color "red", around elements with **a "title" attribute starting with "red".** 

  ```css
  img[title^="red"] { border: 5px solid red; } /* I guess ^ from regex */ 
  /* Hooyah! It's correct! */
  ```

- Set a border with the color "red", around elements with a "title" attribute **ending** with the word "flower" (not flower**s**).

  ```css
  img[title$="flower"] { border: 5px solid red; } /* I guess $ from regex */
  /* Hooyah! It's correct! */
  ```

- Set a border with the color "red", around elements with a "title" attribute containing the value "flow". 

  ```css
  img[title~=flow] { border: 5px solid red; } /* I guess this because I simply don't know "containing the value" */
  img[title*=flow] { border: 5px solid red; } /* correct */
  ```


### Pseudo-classes


- Set the background color for visited and unvisited links to "lightblue", and the background color for the hover and active link states to "yellow". 

  ```css
  a:visited a:link { background-color: lightblue; } a:hover a:active { background-color: yellow; }
  ```
- Change the background color, when a user hovers over p elements, with the class "highlight", to "lightblue". 
  ```css
  p.highlight:hover { background-color: lightblue; } /* Hooyah! */
  ```

- Set the background color of <p> elements, that are the first child of any element, to "lightblue". 

  ```css
   p:first-child { background-color: lightblue; } 
  ```
- Set the background color of <input> elements that are in focus (clicked or active), to "lightblue". 

  ```css
  input:focus { background-color: lightblue; } 
  ```


### Pseudo-elements
- Set text color to red, for the **first line of the <p>** element. `::first-line`
  ```css
  p::first-line { color: red; }
  ```
- Set text color to "red", and the text size to "xx-large", for the **first letter** of the <p> element.
  ```css
  p::first-letter { font-size: xx-large; color: red; }
  ```
- Insert the image "smiley.gif" before, and after <p> elements, using the ::before and ::after pseudo-elements.
  ```css
  p::before { content: url(smiley.gif); }
  p::after { content: url(smiley.gif); }
  ```

## Layout

### Border

- Set a "4px", "dotted" border for` <p>`

  ```css
  p {
    border-style: dotted;
    border-width: 4px;
  }
  ```

- Set the border color for <p> to "red".

  ```css
  p {
    border-style: solid;
    border-color: red;
  }
  ```

- Change the 3 border properties, so that they only show the border on the top side.

  ```css
  p {
    border-top-style: dotted;
    border-width: 4px;
    border-color: red;
  }
  p {
    /* or */
    border-top-style: dotted;
    border-top-width: 4px;
    border-top-color: red;
  }
  ```

- With the border property: Set the border for p to "10px", "solid" and "green".

  ```html
  p { border-top-style: solid; border-color: green; border-width: 10px; }
  ```

- What happen when border-style has four/three/two/one value(s)?

  > top right, bottom, left; top, left+right, bottom; top+bottom, left+right; all

### Border Image


- Give the <div> element an image border using the image "border.png". Slice the image at 30px and repeat it.

  ```css
  div {  border-image: url("border.png") 30px repeat; } /* my try */
  div { 
    border: 10px solid transparent;
    border-image: url(border.png) 30 round;
  } /* answer */
  ```

- Give the <div> element an image border using the image "border.png". Slice the image at 30px and stretch it.

  ```css
  div { border: 10px solid transparent; border-image: url(border.png) 30 stretch; } /* answer */
  ```

### Margin

- Set the left margin of <h1> to "20px". `h1 {margin-left:20px;}`
- Set all margins for <h1> to "25px". `h1{margin:25px;}`
- Use the margin property to set the top and bottom margins for <h1> to "50px", and left and right margins to "25px". `h1 {margin: 50px 25px;}`
- Use the margin property to center align the <h1> element. `h1{margin:auto}`

### Padding

- Set the top padding of <p> to "30px". `p{padding-top:30px;}`
- Set all paddings for <p> to "50px". `p{padding:50px;}`
- Use the padding property to set the top and bottom paddings for <p> to "25px", and left and right paddings to "50px". `p{padding:25px 50px;}`

### Height/Width

- Set the height of <h1> to "100px". `h1{height:100px;}`
- Set the width of <h1> to "50%". `h1{width:50%;}`

### Box Model

- Set the width of the div to "200px". `width:200px;`

- Set the padding of the div to "25px". `padding:25px;`

- Set the border of the div to "25px solid navy". `border:solid 25px navy`

  > Full version:`{border-style:solid; border-width:25px; border-color:navy}`

- Set the margin of the div to "25px".`margin:25px;`



### Display/Visibility

- `visibility` Hide the <h1> element. It should still **take up the same space as before**. 

  ```css
  h1 { visibility: hidden; }
  ```

- Hide the <h1> element. It should **not** take up **any space**.

  ```css
  h1 { display: none; }
  ```

- Display the list items as inline elements.

  ```css
  li { display: inline;}
  ```

- Display the <strong> elements as block elements.

  ```css
  strong { display: block; }
  ```

### Positioning

- [Position css tricks](https://css-tricks.com/almanac/properties/p/position/)

- Position the <h1> element to always be 50px from the top, and 50px from the right, relative to the window/frame edges.

  ```css
  h1 { margin-top:50px; margin-right:50px; position: fixed;} /* my answer */ 
  h1 { position: fixed; top:50px; right:50px; } /* correct answer */ 
  ```

  > [CSS: Top vs Margin-top](https://stackoverflow.com/questions/4036176/css-top-vs-margin-top)
  >
  > `top` is for tweak an element with use of `position` property.
  > `margin-top` is for measuring the external distance to the element, in relation to the previous one.
  >
  > Also, `top` behavior can differ depending on the type of position, `absolute`, `relative` or `fixed`.

- Position the <h1> element 20px left, and 30px down, relative to its normal position.

  ```css
  h1 { margin: 0 0 30px 20px; } /* my answer */ 
  h1 { position: relative; top: 30px; left: -20px; } /* correct answer */ 
  ```

- Position the <h1> element 50px from the left, and 100px from the top, relative to the HTML page.

  ```css
  h1 { position: absolute; top: 100px; left: 50px; }
  ```


- Position the <img> element behind the text. 

  ```css
  img { z-index:-1; }
  ```

- Position the element with the "topleft" class 30px from the left, and 15px from the top, relative to its container. 

  ```css
  .topleft { position: relative; top: 15px; left: 30px; } /* my answer */
  .topleft { position: absolute; top: 15px; left: 30px; } /* correct answer */
  ```

  <img src="https://raw.githubusercontent.com/jason-den/picture-storage/master/2022-10/image-20210812201543383.png" alt="image-20210812201543383" style="zoom:33%; display:inline;" />    <img src="https://raw.githubusercontent.com/jason-den/picture-storage/master/2022-10/image-20210812201609786.png" alt="image-20210812201609786" style="zoom:33%; display:inline;" />

### Overflow


- Add a scrollbar to the <div> element. 

  ```css
  div {  overflow: scroll; }
  ```

- Specify that the overflowing text in the <div> element should not be visible, not even with scrolling. 

  ```css
  div { overflow: clip; } /* my guess */
  div { overflow: hidden; } /* correct answer */
  ```

- Add a horizontal scrollbar to <div>. 

  ```css
  div {
    background-color: #eee;
    width: 150px;
    height: 70px;
    border: 1px dotted black;
    white-space: nowrap;
  } /* existing style */
  div { overflow: horizontal scroll; } /* my guess */
  div { overflow-x: scroll; } /* correct answer */
  ```

### Align


- Center align the <div> element using margins. 

  ```css
  div { align: center; } /* my guess */
  div { margin-left: auto; margin-right: auto; } /* correct answer */
  ```

- Position the <div> element all the way to the right using absolute positioning. 

  ```css
  div { position: absolute; right: 0px; }
  ```





### Outline

- Set a "solid", "5px" outline for <p>. `p{outline: solid 5px;}`

- Set the outline color for <p> to "green". `p{outline:green;}`

- With the outline property: Set the outline for p to "red", "dotted" and "10px". `outline:red dotted 10px;`

  > note that, order doesn't matter. it could be `10px red dotted` as well

## General

### Opacity


- Set the transparency/opacity of the <img> element to "0.4".

  ```css
  img { opacity: 0.4; } /* my try. Hooyah! */
  ```

- Set the transparency/opacity of the <h1> element to "0.4".

  ```css
  h1 { opacity: 0.4 }
  ```

  > opacity impacts all children elements, including background. If want edit font/background only, consider something like `rgb(0,255,0, 0.3)`.

- Remove the transparency/opacity of the <img> element when the user hovers over it with the mouse pointer.

  ```css
  img:hover { opacity: 1 ; } /* my try. Hooyah! */
  ```

### Color


- Set the opacity for the background color of the <h1> element to "0.3" by using a RGBA color instead of RGB.

  ```css
  h1 { background-color: rgb(0,255,0); } /* starting point */
  h1 { background-color: rgb(0,255,0, 0.3); } /* answer */
  ```

- Set the following **HSL color** as the background of the <h1> element: Set the Hue to red (0), Saturation to 100%, and lightness to 50%.

  ```css
  h1 { background-color: hsl(0, 100%, 50%) ; } /* my try. done */
  ```
  
- Set the opacity for the background color of the <h1> element to "0.3" by using a HSLA color instead of HSL.

  ```css
  h1 { background-color: hsla(0, 100%, 50%, 0.3); } /* my try */
  ```

> `hsl(hue, saturation, lightness)`
>
> `rgba(red, green, blue [, alpha] )`

### Background-color

1. Set the background color for the page to "linen" and the background color for `<h1>` to "lightblue".

   ```html
   <style>
     body {
       background-color: linen;
     }
     h1 {
       background-color: lightblue;
     }
   </style>
   ```

2. Set "paper.gif" as the background image of the page.

   ```html
   <style>
     body {
       background-image: url('paper.gif');
     }
   </style>
   ```

   > note the `url()`

3. Set "gradient_bg_vertical.png" as the background image of the page, and repeat it vertically only.

   ```html
   <style>
     body {
       background-image: url('gradient_bg_vertical.png');
       background-repeat: repeat-y;
     }
   </style>
   ```

4. Specify that the background image should be shown once, in the top right corner.

   ```html
   <style>
     body {
       background-image: url('img_tree.png');
       background-repeat: none; /* wrong: shoud be no-repeat */
       background-position: top right;
     }
   </style>
   ```

5. Use the **shorthand** background property to set background image to `"img_tree.png"`, show it once, in the top right corner.

   > Hint: The background property contains:
   > `background-color background-image background-repeat background-attachment background-position`

   ```html
   <style>
     body {
       background: url('img_tree.png') no-repeat top right;
       /* Wow, this is quite impressive.
     Yet I don't like syntax complexity much  */
     }
   </style>
   ```

### Background

> TODO: more practice for mastery

Shorthand 

```css
background: bg-color bg-image position/bg-size bg-repeat bg-origin bg-clip bg-attachment initial|inherit;
```

> potential confusion: position and bg-origin

- Add a second background image ("img_flwr.gif") to the <body> element. Make sure that "img_flwr.gif" is displayed on top of the current background image.

  ```css
  body {background-image: url(paper.gif);} /* existing code */
  body {background-image: url(img_flwr.gif);} /* my answer, simply overwrite original img. doesn't fulfill requirement */
  body { background-image: url(img_flwr.gif), url(paper.gif); } /* correct answer */
  ```


- Change the size of the background image to: width 100px, height 80px.
  ```css
  background: url(img_flwr.gif)  no-repeat;
  background-size: 100px 80px;
  ```
  
- Change the size of the background image so it always fits the entire page.
  ```css
  background-size: cover; 
  ```
  
- Specify that the **background image position** should start from the **upper left corner of the content-box**.

  > `background-origin`

  ```css
  div { 
    border: 10px solid black;
    padding: 35px;
    background: url(img_flwr.gif);
    background-repeat: no-repeat;
  } /* start */ 
  div { background-origin: content-box; } /* answer */
  ```

- Specify that the "painting area" of the background should be to the outside edge of the padding.

  ```css
  div { 
    border: 10px dotted black;
    padding: 35px;
    background: lightblue;
  } /* start */
  div {  background-clip: padding-box; } /* answer */ 
  ```

### Gradients

> `background-image: linear-gradient(direction, color-stop1, color-stop2, ...);`
>
> - Direction - Top to Bottom (default) 


- Set a linear gradient background for the `<div>` element, going from the top to bottom, transitioning from "white" to "green".

  ```css
  div { background-image: linear-gradient white green; } /* my try */
  div { background-image: linear-gradient(white, green); } /* answer */
  ```

- Set a linear gradient background for the <div> element, going from the top left to the bottom right, transitioning from "white" to "green".

  ```css
  div { background-image: linear-gradient(to bottom right, white, green); } 
  /* my try, hooyah! */
  ```

- Set a linear gradient background for the <div> element, going at a 70 degree angle, transitioning from "white" to "green".

  ```css
  div { background-image: linear-gradient(70, white, green); }  /* my try */
  div { background-image: linear-gradient(70deg, white, green); } /* answer */
  ```

- Set a linear gradient background for the <div> element, going from the top to bottom, transitioning from "white" to "red" to "blue" to "green".

  ```css
  div { background-image: linear-gradient(white, red, blue, green); }  /* my try */
  ```

- Set a linear gradient background for the <div> element, going from the top to bottom, transitioning from "rgba(0,255,0,0.2)" to "rgba(0,255,0,1)".

  ```css
  div { background-image: linear-gradient(rgba(0,255,0,0.2), rgba(0,255,0,1)); }  /* my try */
  ```

- Set a radial gradient background for the <div> element, transitioning from "white" to "green".

  ```css
  div { background-image: radial-gradient(white, green); }  /* my try */
  ```

- Set a radial gradient background for the <div> element, with a circle shape, transitioning from "white" to "green".

  ```css
  div { background-image: radial-gradient(circle, white, green); }  /* my try */
  ```

### Shadow Effects


- Set a "2px" horizontal, and "2px" vertical, text shadow for the <h1> element. `text-shadow `

  ```css
  h1 { text-shadow : 2px 2px; } /* my try */
  ```

- Change the color of the text shadow to "green", and set a "5px" blur radius.

  > `text-shadow: h-shadow v-shadow blur-radius color`

  ```css
  h1 { text-shadow: 2px 2px 5px green; } /* my try */
  ```

- Add a new shadow (do not remove the current one) to the <h1> element with: no horizontal or vertical shadow, 10px blur, and a red color.

  ```css
  h1 { text-shadow: 2px 2px 5px green; } /* start */
  h1 { text-shadow: 2px 2px 5px green, 0 0 10px red; } /* added */
  ```

- Set a "10px" horizontal, and "10px" vertical, box shadow for the <div> element.

  ```css
  div { box-shadow: 10 10; } /* first try */
  div { box-shadow: 10px 10px; } /* second try */
  ```

- Change the color of the box shadow to "grey", and set a "5px" blur.

  ```css
  div { box-shadow: 10px 10px 5px grey; } /* my try */
  ```



### Rounded Corners


- Give the <div> element rounded corners (use the shorthand property and the value "25px").

  ```css
  div { round-corner: 25px; } /* my first try */
  div { border-radius: 25px; } /* my second try, correct */
  ```

- Give the <div> element a rounded corner (25px radius) on the bottom left side.

  ```css
  div { border-radius-bottom-left: 25px; } /* my try */
  div { border-bottom-left-radius: 25px; } /* answer */
  ```



### Text

- Set the text color for the page to "red", and the text color for <h1> to "blue". `body{color:red;} h1 {color:blue;}`

- Center align the <h1> element. `h1 {text-align: center;}`

- Remove the underline from the link. `a {text-decoration:none;}`

- Style text in <h1> to uppercase letters, and text in <p> to capitalized letters. `h1{text-transform:uppercase;} p{text-transform:capitalize;}`

  > my guess was `h1{text-transform:uppper;} p{text-transform:capitalized;}`

- Indent the first line of the <p> element with 20px. `p{text-indent:20px;}`

### Text Effect  `offten use`


- `text-overflow` Specify that the overflowed content for the <p> element should be signaled with an **ellipsis** (...)   

  ```css
  p { text-overflow: ellipsis; } /* my try */
  ```


- `word-wrap` Specify that text in the <p> element should wrap, even if it needs to split in the middle of a word. 

  ```css
  p { word-wrap: split; } /* my try */
  p { word-wrap: break-word; } /* answer */
  ```

- `word-break` Specify that text in the <p> element can break **between any two letters**.

  ```css
  p { word-break: any; } /* my try */
  p { word-break: break-all; } /* answer */
  ```

> - `text-overflow: clip|ellipsis|<string>|initial|inherit;`  `<string>` reder the given string to represent the clip text;
> - `word-wrap: normal|break-word|initial|inherit;`
> - `word-break: normal|break-all|keep-all|break-word|initial|inherit;`

### Font

- [Web safe font](https://www.w3schools.com/css/css_font_websafe.asp) and [Commonly Used Font Fallbacks](https://www.w3schools.com/css/css_font_fallbacks.asp)

- Set the font family for the page to "Courier New", and the font family for <h1> to "Verdana". `body{font-family: "Courier New";} h1{font-family: Verdana;}`

- Show <p> elements as "italic" text. `p{font-style:italic; }`

- Set the font size for the page to "20px", and the font size for <h1> to "3em". `body{font-size:20px;} h1{font-size:3em;}`

- Show <p> elements as "bold" text. ``

- With the font property: Set the <p> to "italic", "20px" and "Verdana".

  ```css
  p {
    font: italic 20px Verdana;
  }
  ```

  ```css
  /* syntax */
  body {
    font: font-style font-variant font-weight font-size/line-height font-family;
  }
  /* use case */
  body {
    font: italic small-caps normal 13px/150% Arial, Helvetica, sans-serif;
  }
  ```

### Web Fonts


- `@font-face` Add a web font with the name "sansation" and the URL "sansation_light.woff".

  ```css
  body { font-family: sansation; } /* start */
  body { web-font: sansation url("sansation_light.woff"); } /* my guess */
  @font-face { font-family: sansation; src: url(sansation_light.woff); } /* answer */
  ```

- Add another @font-face rule for bold characters of the "sansation" font. Use the URL "sansation_bold.woff".

  ```css
  @font-face { font-family: sansation; font-weight: bold; src: url(sansation_bold.woff); } /* my try. Hooyah! */
  ```

## Daily use elements 

### Link

- [css-trick](https://css-tricks.com/a-complete-guide-to-links-and-buttons/)

- four links states: `a:link a:visited a:hover a:active` ; `a:link` means unvisited.

- Set the color for links to "green". `a {color:green;}`

- Set the color for unvisited links to "red", and the color for visited links "blue".

  ```css
  /* unvisited link */
  a:link {
    text-decoration: none;
  }
  
  /* visited link */
  a:visited {
    text-decoration: none;
  }
  
  /* mouse over link */
  a:hover {
    text-decoration: underline;
  }
  
  /* selected link */
  a:active {
    text-decoration: underline;
  }
  ```

### List

- Set the list style for unordered lists to "square", and the list style for ordered lists to "upper-roman".

  ```css
  ul {list-style-type: square;}
  ol {list-style-type: upper-roman;}
  ```

- `list-style-image` Set the image "sqpurple.gif" as the list item marker for the unordered list.

  ```css
  ul {list-style-image: url("sqpurple.gif");}
  ```

- With the list-style property: Set the unordered list marker to "img_marker.png", with a backup style of "circle", and display the markers inside the content flow.

  ```css
  ul {
  	list-style-type: circle;
   	list-style-position: inside;
    list-style-image: url("img_marker.png");
  }
  /* shorthand */
  ul { list-style: circle inside url('img_marker.png');}
  ```

- Remove the bullets/markers from the list items.

  ```css
  ul { 	list-style-type: none; }
  ```



### Table

- Set the border to "2px solid green" for table, th and td elements.

  ```css
  table, th, td { border: 2px solid green; }
  ```

- ` border-collapse` Collapse the table borders into a single border.

  ```css
  table { border-collapse: collapse; }
  ```

- Set the width of the table to "100%".

  ```css
  table { width:100%; }
  ```

- Set the text alignment in `<td>` elements to "right".

  ```css
  td { text-align: right; }
  ```

- Set the padding in <th> elements to "15px".

  ```css
  th { padding:15px; }
  ```

- Set the background color of <th> elements to "lightblue".

  ```css
  th { background-color: lightblue; }
  ```

## Animation

### Keyframe

- Shorthand: `animation: name duration timing-function delay iteration-count direction fill-mode play-state;`

- Add a 2 second animation for the <div> element, which changes the color from red to blue. Call the animation "example" 

  ```css
  div { width: 100px; height: 100px; background-color: red; }  /* starting point */
  ```
  ```css
  /* answer */
  div { width: 100px; height: 100px; background-color: red; animation-name: example; animation-duration: 2s; } 
  @keyframes example { from {background-color:red; } to {background-color:blue; } }
  ```
  
  > `@keyframes`    `animation-name`    `animation-duration`
  
- Add the following 5 steps to the animation "example" (using `0%, 25%, 50%, 75%, and 100%`):

  1. 0% - Set background color to "red", left position to "0px", top position to: "0px"
  2. 25% - Set background color to "blue", left position to "0px", top position to: "200px"
  3. 50% - Set background color to "green", left position to "200px", top position to: "200px"
  4. 75% - Set background color to "yellow", left position to "200px", top position to: "0px"
  5. 100% - Set background color to "red", left position to "0px", top position to: "0px"
  > The % values represents the different stages of the animation. 0% is the start, and 100% is the end
  
  ```css
  div {
    width: 100px;
    height: 100px;
    position: relative;
    background-color: red;
    animation-name: example;
    animation-duration: 4s;
  } /* starting point */
  ```

  ```css
  @keyframes example {
    0% { background-color: red; left: 0px; top: 0px; }
    25% { background-color: blue; left: 0px; top: 200px; }
    50% { background-color: green; left: 200px; top: 200px; }
    75% { background-color: yellow; left: 200px; top: 0px; }
    100% { background-color: red; left: 0px; top: 0px; }
  } /* my try */ /* And it's correct! Hooyah! */
  ```
  
- Specify that the animation of the <div> element should have a "1" second delay before starting. 

  ```css
  @keyframes example { animation-delay: 1s; }  /* my try */ 
  div { animation-delay: 1s; }  /* correct answer */ 
  ```
  
- Specify that the animation of the <div> element should continue to loop for ever. 
  ```css
  div { animation-loop: true; } /* my try */
  div { animation-iteration-count: infinite; } /* answer */
  ```

- Specify that the animation of the <div> element should alternate between running forwards and backwards.
  ```css
  div { animation-direction: alternate; } /* my try */
  div { ; } /* answer */
  ```
  > animation-direction: reverse|alternate|alternate-reverse    (|normal|initial|inherit)
- Specify that the animation of the <div> element should have a "ease-in-out" speed curve.
  ```css
  div { animation-timing-function: ease-in-out; }
  ```
  > animation-timing-function: linear|ease|ease-in|ease-out|ease-in-out|step-start|step-end|steps(int,start|end)|cubic-bezier(n,n,n,n)|initial|inherit;
  > default is ease, good enough

### Transition

shorthand: `transition: property duration timing-function delay`
<iframe height="600" style="width: 100%;" scrolling="no" title="transition" src="https://codepen.io/jason-den/embed/PomgEPy?default-tab=css%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/jason-den/pen/PomgEPy">
  transition</a> by Jason-Den (<a href="https://codepen.io/jason-den">@jason-den</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>


- Add a 2 second transition effect for width changes of the <div> element.

  ```css
  /* start */
  div {
    width: 100px;
    height: 100px;
    background: red;
  }
  div:hover { width: 300px; }
  div { transiction: 2s; } /* my try - note the typo in "transiction"  */
  div { transition: width 2s; } /* answer */
  ```

- Specify that the transition of the <div> element should have a "ease-in-out" speed curve.

  ```css
  div { transition: width 2s; } /* starting */
  div { transition: width 2s ease-in-out; } /* my try. Hooyah! */
  ```

- Specify that the transition of the <div> element should have a "0.5" second delay before starting.

  ```css
  div { transition-delay: 0.5s;} /* my try. Hooyah! */
  ```
  
- Add a 2 second transition effect for background, and transform changes of the <div> element.

  ```css
  div { transition: background 2s, transform; } /* my try */
  div { transition: background 2s, transform 2s; } /* answer */
  ```
  
- Using the transition shorthand property, specify width changes for the <div> element should have: "2" second duration, "ease-in-out" speed curve, and a "0.5" second delay before starting.

  ```css
  div { transition: width 2s ease-in-out, 0.5s;} /* my try */
  div { transition: width 2s ease-in-out 0.5s;} /* my try */
  ```

### Transform

| [transform](https://www.w3schools.com/cssref/css3_pr_transform.asp) | Applies a 2D or 3D transformation to an element           |
| ------------------------------------------------------------ | --------------------------------------------------------- |
| [transform-origin](https://www.w3schools.com/cssref/css3_pr_transform-origin.asp) | Allows you to change the position on transformed elements |

- transform methods:`translate() rotate() scale() skew()`
  > not as important: `scaleY() scaleX() skewY() skewX() matrix()`
  >
  > - [try skewy](https://www.w3schools.com/cssref/playit.asp?filename=playcss_transform_skewy)
  >
  > - [rotateX()](https://www.w3schools.com/cssref/playit.asp?filename=playcss_transform_rotatex)
  >
  > The matrix() method combines all the 2D transform methods into one.  I think it's not friendly thus not recommend using it.

<iframe height="600" style="width: 100%;" scrolling="no" title="transition" src="https://codepen.io/jason-den/embed/mdmgpxa?default-tab=css%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/jason-den/pen/mdmgpxa">
  transition</a> by Jason-Den (<a href="https://codepen.io/jason-den">@jason-den</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>
- `translate()` With the transform property, move the <div> element 100px to the right, and 200px down.
  
  ```css
  div { transform: translate(100px, 200px); }
  ```
  
- `rotate()` With the transform property, rotate the <div> element 45 degrees.

  ```css
  div { transform: rotate(45deg); }
  ```


- `scale()` With the transform property, change the size of the <div> to half its width, but double its height.

  ```css
  div { transform: scale(0.5, 2); }
  ```


- `skew` With the transform property, skew the <div> element 20 degrees along the X-axis, and 30 degrees along the Y-axis.

  ```css
  div { transform: skew(20deg, 30deg); } /* my guess */
  ```
  
- With the transform property, rotate the <div> element 150deg around its X-axis.

  ```css
  div { transform: rotateX(150deg); }
  ```

## References

[OverAPI CSS Cheat Sheet](https://overapi.com/css)

### All Pseudo Elements

| Selector                                                     | Example         | Example description                                          |
| :----------------------------------------------------------- | :-------------- | :----------------------------------------------------------- |
| [::after](https://www.w3schools.com/cssref/sel_after.asp)    | p::after        | Insert something after the content of each <p> element       |
| [::before](https://www.w3schools.com/cssref/sel_before.asp)  | p::before       | Insert something before the content of each <p> element      |
| [::first-letter](https://www.w3schools.com/cssref/sel_firstletter.asp) | p::first-letter | Selects the first letter of each <p> element                 |
| [::first-line](https://www.w3schools.com/cssref/sel_firstline.asp) | p::first-line   | Selects the first line of each <p> element                   |
| [::marker](https://www.w3schools.com/cssref/sel_marker.asp)  | ::marker        | Selects the markers of list items                            |
| [::selection](https://www.w3schools.com/cssref/sel_selection.asp) | p::selection    | Selects the portion of an element that is selected by a user |

### All Pseudo Classes

| Selector                                                     | Example               | Example description                                          |
| :----------------------------------------------------------- | :-------------------- | :----------------------------------------------------------- |
| [:active](https://www.w3schools.com/cssref/sel_active.asp)   | a:active              | Selects the active link                                      |
| [:checked](https://www.w3schools.com/cssref/sel_checked.asp) | input:checked         | Selects every checked <input> element                        |
| [:disabled](https://www.w3schools.com/cssref/sel_disabled.asp) | input:disabled        | Selects every disabled <input> element                       |
| [:empty](https://www.w3schools.com/cssref/sel_empty.asp)     | p:empty               | Selects every <p> element that has no children               |
| [:enabled](https://www.w3schools.com/cssref/sel_enabled.asp) | input:enabled         | Selects every enabled <input> element                        |
| [:first-child](https://www.w3schools.com/cssref/sel_firstchild.asp) | p:first-child         | Selects every <p> elements that is the first child of its parent |
| [:first-of-type](https://www.w3schools.com/cssref/sel_first-of-type.asp) | p:first-of-type       | Selects every <p> element that is the first <p> element of its parent |
| [:focus](https://www.w3schools.com/cssref/sel_focus.asp)     | input:focus           | Selects the <input> element that has focus                   |
| [:hover](https://www.w3schools.com/cssref/sel_hover.asp)     | a:hover               | Selects links on mouse over                                  |
| [:in-range](https://www.w3schools.com/cssref/sel_in-range.asp) | input:in-range        | Selects <input> elements with a value within a specified range |
| [:invalid](https://www.w3schools.com/cssref/sel_invalid.asp) | input:invalid         | Selects all <input> elements with an invalid value           |
| [:lang(*language*)](https://www.w3schools.com/cssref/sel_lang.asp) | p:lang(it)            | Selects every <p> element with a lang attribute value starting with "it" |
| [:last-child](https://www.w3schools.com/cssref/sel_last-child.asp) | p:last-child          | Selects every <p> elements that is the last child of its parent |
| [:last-of-type](https://www.w3schools.com/cssref/sel_last-of-type.asp) | p:last-of-type        | Selects every <p> element that is the last <p> element of its parent |
| [:link](https://www.w3schools.com/cssref/sel_link.asp)       | a:link                | Selects all unvisited links                                  |
| [:not(selector)](https://www.w3schools.com/cssref/sel_not.asp) | :not(p)               | Selects every element that is not a <p> element              |
| [:nth-child(n)](https://www.w3schools.com/cssref/sel_nth-child.asp) | p:nth-child(2)        | Selects every <p> element that is the second child of its parent |
| [:nth-last-child(n)](https://www.w3schools.com/cssref/sel_nth-last-child.asp) | p:nth-last-child(2)   | Selects every <p> element that is the second child of its parent, counting from the last child |
| [:nth-last-of-type(n)](https://www.w3schools.com/cssref/sel_nth-last-of-type.asp) | p:nth-last-of-type(2) | Selects every <p> element that is the second <p> element of its parent, counting from the last child |
| [:nth-of-type(n)](https://www.w3schools.com/cssref/sel_nth-of-type.asp) | p:nth-of-type(2)      | Selects every <p> element that is the second <p> element of its parent |
| [:only-of-type](https://www.w3schools.com/cssref/sel_only-of-type.asp) | p:only-of-type        | Selects every <p> element that is the only <p> element of its parent |
| [:only-child](https://www.w3schools.com/cssref/sel_only-child.asp) | p:only-child          | Selects every <p> element that is the only child of its parent |
| [:optional](https://www.w3schools.com/cssref/sel_optional.asp) | input:optional        | Selects <input> elements with no "required" attribute        |
| [:out-of-range](https://www.w3schools.com/cssref/sel_out-of-range.asp) | input:out-of-range    | Selects <input> elements with a value outside a specified range |
| [:read-only](https://www.w3schools.com/cssref/sel_read-only.asp) | input:read-only       | Selects <input> elements with a "readonly" attribute specified |
| [:read-write](https://www.w3schools.com/cssref/sel_read-write.asp) | input:read-write      | Selects <input> elements with no "readonly" attribute        |
| [:required](https://www.w3schools.com/cssref/sel_required.asp) | input:required        | Selects <input> elements with a "required" attribute specified |
| [:root](https://www.w3schools.com/cssref/sel_root.asp)       | root                  | Selects the document's root element                          |
| [:target](https://www.w3schools.com/cssref/sel_target.asp)   | #news:target          | Selects the current active #news element (clicked on a URL containing that anchor name) |
| [:valid](https://www.w3schools.com/cssref/sel_valid.asp)     | input:valid           | Selects all <input> elements with a valid value              |
| [:visited](https://www.w3schools.com/cssref/sel_visited.asp) | a:visited             | Selects all visited links                                    |
