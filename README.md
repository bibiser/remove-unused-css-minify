# remove-unused-css-minify
## Process of Removing Unused CSS and Minification

### Overview

This project involves two main processes: removing unused CSS and minifying the CSS code. Below is a breakdown of each step of the process.

### Step 1: Remove Unused CSS

1. **Parsing HTML and CSS**
    - The process begins by parsing the HTML and CSS code to identify all selectors.

2. **Identifying Selectors**
   - All types of selectors are identified, including:
   
   - **`element` selectors**, e.g., `div`
   - **`class` selectors**, e.g., `.className`
   - **`id` selectors**, e.g., `#idName`
   - **`pseudo-classes`**, e.g., `:hover`
   - **`pseudo-elements`**, e.g., `::before`
   - **`combined selectors`**, e.g., `div.class[attr="value"]`
   - **`descendant selectors`**, e.g., `div p`
   - **`grouped selectors`**, e.g., `div, .class, #id`
   - **`sibling combinators`**, including:
     - **Adjacent Sibling Combinator (`+`)**: Selects the element immediately following a specified element.
       - Example: `div + p { color: red; }`
     - **General Sibling Combinator (`~`)**: Selects any sibling element, not necessarily the immediate one.
       - Example: `div ~ p { color: blue; }`
   - **`attribute selectors`**, including:
     - **Simple Attribute Selector (`[attr]`)**: Selects elements with the specified attribute.
       - Example: `[type] { border: 1px solid red; }`
     - **Attribute Equals Selector (`[attr="value"]`)**: Selects elements with a specific attribute value.
       - Example: `[type="text"] { background-color: yellow; }`
     - **Attribute Contains Word Selector (`[attr~="value"]`)**: Selects elements whose attribute value contains a specific word.
       - Example: `[class~="featured"] { font-weight: bold; }`
     - **Attribute Prefix Selector (`[attr^="value"]`)**: Selects elements whose attribute value starts with a specified value.
       - Example: `[href^="https://"] { color: green; }`
     - **Attribute Suffix Selector (`[attr$="value"]`)**: Selects elements whose attribute value ends with a specified value.
       - Example: `[src$=".png"] { border: 2px solid blue; }`
     - **Attribute Substring Selector (`[attr*="value"]`)**: Selects elements whose attribute value contains the specified substring.
       - Example: `[title*="tutorial"] { color: purple; }`

3. **Supporting Modern CSS Rules**
    - Modern CSS rules such as `:has()`, `:is()`, `:where()` are supported, as well as `@media` queries for mobile responsiveness.
4. **Matching and Removal of Unused CSS Rules**
    - The process of removing unused CSS involves matching the identified selectors to the elements in the HTML document.
    - **Matching**: Selectors from the CSS are compared against the HTML elements to check if they are actually used. This is done by:
      - Scanning the HTML for matching elements or attributes.
      - Checking if any pseudo-classes or pseudo-elements apply to the selected elements.
      - Verifying if any specific combinations of selectors (e.g., `div.class[attr="value"]`) are present.
    - **Removal**: After identifying unused rules, they are removed from the CSS file to reduce the size and increase performance. The process ensures that only the necessary and used rules remain, optimizing the overall CSS for the project.
    - The removal process accounts for edge cases like dynamically added content or JavaScript-driven styles to ensure comprehensive detection.
### Step 2: Minification Process

1. **Removing Invalid Rules**
    - Any CSS rules that are invalid, redundant, or not used within the parsed HTML are removed.

2. **Removing Extra Spaces**
    - Spaces, line breaks, and indentation that are not necessary for the CSS to function are removed to reduce file size.

3. **Shortening Rules**
    - Properties that can be shortened are condensed to minimize the size, for example:
    ```css
    background-color: #ffffff; /* shortened to */
    background: #fff;
    ```
### Example removing unused css

### **Before Removing Unused CSS**

#### HTML:
```html
<div class="container">
    <h1 class="underlined">Welcome to My Website</h1>
    <p>This is a paragraph.</p>
<h2>Say Hello</h2>
    <span class="highlight">Highlighted Text</span>
</div>

<div class="footer">
    <p>Footer text</p>
</div> 
```
### CSS:

```css
/* Combined Selectors */
h1, h2, h3, h4 {
    color: blue;
}
.container p {
    font-size: 1.2em;
    color: green;
}
.container.highlight {
    background-color: yellow;
}
/* Grouped Selectors */
h1, p {
    font-family: Arial, sans-serif;
}
/* Sibling Selectors */
.container p ~ .highlight {
    color: red;
}
/* Attribute Selectors */
.footer [data-type="footer-text"] {
    color: gray;
}
/* Unused Selectors (will be removed) */
.footer .unused-class {
    font-style: italic;
}
.unrelated-class {
    display: block;
}
```
### Cleaned CSS from Unused selectors:
```css
/* Combined Selectors */
h1, h2 {
    color: blue;
}
.container p {
    font-size: 1.2em;
    color: green;
}
/* Grouped Selectors */
h1.underlined {
    font-family: Arial, sans-serif;
}
/* Sibling Selectors */
.container p ~ .highlight {
    color: red;
}
```
### Example Minify

The following shows an example before and after minification:

```css
/* Before */
body { color: red; padding: 10px; margin: 0; }
.container { width: 100%; height: 100px; }

/* After Minification */
body{color:red;padding:10px;margin:0;}.container{width:100%;height:100px;}
