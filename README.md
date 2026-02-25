# JAVASCRIPT-Working-with-the-DOM

---

# **.querySelectorAll(string) **
A DOM method to find **all elements** matching a **CSS selector string**.

## **What is it called on?**
- `document.querySelectorAll()` → searches the **entire page**  
- `element.querySelectorAll()` → searches **only inside that element**
---

#### **Example**
```js
const matches = document.querySelectorAll("selector");
```
### **Complex selector example**
```js
document.querySelectorAll("ul.ingredients li");
```
Selects all `<li>` elements inside a `<ul>` with class `"ingredients"`.

---

# **RETURNS** A **NodeList**, which is an array‑like collection of elements.

### **OUTPUTS are based on the page**

### **1. Multiple matches**
```js
// NodeList(3)
{
  0: <li>Flour</li>,
  1: <li>Cheese</li>,
  2: <li>Water</li>,
  length: 3
}
```

### **2. One match**
```js
// NodeList(1)
{
  0: <li>Flour</li>,
  length: 1
}
```

### **3. No matches**
```js
// NodeList(0)
{
  length: 0
}
```

### **4. Matches nested deeper**
```js
// NodeList(2)
{
  0: <li><span>Salt</span></li>,
  1: <li><span>Pepper</span></li>,
  length: 2
}
```

### **5. Matches across multiple lists**
```js
// NodeList(5)
{
  0: <li>Flour</li>,
  1: <li>Cheese</li>,
  2: <li>Water</li>,
  3: <li>Sugar</li>,
  4: <li>Butter</li>,
  length: 5
}
```

# **What you can do with the NodeList**

### **Check how many were found**
```js
console.log(matches.length);
```

### **Access specific items**
```js
console.log(matches[1]);
```

### **Iterate through all items**
```js
matches.forEach(el => {
  el.style.color = "red";
});
```

### **Add event listeners to all**
```js
matches.forEach(el => {
  el.addEventListener("click", () => {
    el.style.textDecoration = "line-through";
  });
});
```

### **Convert to a real array**
```js
const arr = Array.from(matches);
```

# **How to create New DOM Nodes ⟹ innerHTML or createElement()**

## **1. innerHTML**
**Use to** set the HTML markup *inside an existing element* using a string.
**Example:**
```js
const container = document.getElementById("container");
container.innerHTML = "<ul><li>Cheese</li><li>Tomato</li></ul>";
```
**Resulting DOM:**
```html
<div id="container">
  <ul>
    <li>Cheese</li>
    <li>Tomato</li>
  </ul>
</div>
```
---

## **2. createElement()**
**Creates a new element node,** one at a time.

**Example:**
```js
const container = document.getElementById("container");

const img = document.createElement("img");
img.src = "https://cdn.freecodecamp.org/curriculum/cat-photo-app/lasagna.jpg";
img.alt = "A slice of lasagna on a plate.";

container.appendChild(img);
```
# **ADDING & REMOVING DOM NODES FROM PARENTS**

## **1. ADDING Nodes — `appendChild()`**
**Adds a node to the end** of list of children.

**Syntax:**
```js
parentNode.appendChild(newNode);
```
**Example:**
```js
const dessertsList = document.getElementById("desserts");
const li = document.createElement("li");
li.textContent = "Cookies";
dessertsList.appendChild(li);
```
**Result:**  
A new `<li>` appears at the bottom of the `<ul>`.
---

## **2. REMOVING Nodes — `removeChild()`**
**Removes a specific child node**.

**Syntax:**
```js
parentNode.removeChild(childNode);
 ```

**Example:**
```js
const sectionEl = document.getElementById("example-section");
const lastParagraph = document.querySelector("#example-section p:last-of-type");
sectionEl.removeChild(lastParagraph);
```
**Result:**  
The last `<p>` inside the section is removed.
---

# **DOM Node Manipulation**

| Method | What It Does | Syntax | Example |
|--------|--------------|--------|---------|
| **appendChild()** | Adds a node to the **end** of a parent’s children | `parent.appendChild(node)` | `list.appendChild(li)` |
| **prepend()** | Adds a node to the **start** of a parent’s children | `parent.prepend(node)` | `list.prepend(li)` |
| **remove()** | Removes the node **itself** (no parent needed) | `node.remove()` | `li.remove()` |
| **removeChild()** | Removes a **specific child** from a parent | `parent.removeChild(child)` | `list.removeChild(li)` |
| **replaceChild()** | Replaces one child with another | `parent.replaceChild(newNode, oldNode)` | `list.replaceChild(newLi, oldLi)` |
| **insertBefore()** | Inserts a node **before** a specific child | `parent.insertBefore(newNode, referenceNode)` | `list.insertBefore(li, list.firstChild)` |

---

# **Navigator, Window, and Document**

## **Navigator**
Gives informaton about **browser and device**.

### Examples:
```js
navigator.userAgent  // "Mozilla/5.0 … Chrome/128…" **Browser + OS details**
navigator.language  // "en-US" **User’s language**
```
## **Window -top level global object**
Gives info about the **browser window**.  

### Examples:
```js
window.innerWidth        // width in pixels
window.location          // URL info object
location                 // same as window.location
```
## **Document DOM the webpage within the window**

### Example:
```js
document.children        // HTMLCollection of top-level nodes
```
# **Compare Navigator, Window, and Document**
| Interface | Represents | Common Uses |
|----------|------------|-------------|
| **Navigator** | Browser environment | User agent, language |
| **Window** | Browser window (global object) | Size, URL, navigation, timers |
||Window size|(`innerWidth`, `innerHeight`)|
||Current URL|(`location`)|
||Methods for|opening, navigating, timers, etc.|
| **Document** | The DOM inside the window | Selecting, creating, editing elements |
||Document structure |(`document.children`)|
||Reading/modifying content |(`textContent`, `innerHTML`)|
||Creating elements|(`createElement`)|
||Selecting elements|(`querySelector`, `getElementById`)|
---

# **setAttribute()**
Adds or updates a **new or existing attribute** on an HTML element.
---
## **Syntax**
```js
element.setAttribute(attributeName, value);
```
## **ADD Example**
```html
<p id="para">I am a paragraph</p>
```
```js
const para = document.getElementById("para");
para.setAttribute("class", "my-class");
```
Result:
```html
<p id="para" class="my-class">I am a paragraph</p>
```
## **Update Example**
```html
<div class="my-class"></div>
```
```js
const divEl = document.querySelector(".my-class");
divEl.setAttribute("class", "example");
```
Result:
```html
<div class="example"></div>
```
## **Real‑World Uses**
- Updating an image’s `src` when a user clicks a thumbnail  
- Adding form validation attributes (`required`, `minlength`)  
- Setting `data-*` attributes for dynamic UI behavior  
---

# **Event Object**

| Feature | What It Means | Example / Notes |
|--------|----------------|-----------------|
| **What it is** | Information about the interaction with the page | Events(e): Clicks, key presses, form submits, device motion |
| **`e.type`** | The kind of event that occurred | `"click"`, `"keydown"`, `"submit"` |
|**`event.currentTarget`**|element the listener is attached to||
| **`e.target`** | The element (or object) that triggered the event | Usually an HTMLElement, but could be `document`, `window`|
| **`e.preventDefault()`** | Stops the browser’s default behavior | Prevent form submission, stop link navigation |
| **`e.stopPropagation()`** | Stops the event from bubbling to parent elements | Useful in nested click handlers |
| **Event‑specific properties** | Extra data depending on event type | Example: `FetchEvent.request`, `KeyboardEvent.key`, `MouseEvent.clientX` |
| **How to inspect it** | Log the event to see all available properties | `console.log(event)` |
|Extra properties| InputEvent |→ typing info|
|Extra properties| MouseEvent |→ mouse position, buttons|
|Extra properties| SubmitEvent |→ form submission details|
---

# ⭐ **Event Bubbling & Event Delegation**

## **Event Bubbling**
- When an event happens on an element, it **first runs on that element**, then **bubbles up** through its parent elements.
- Example: clicking a `<span>` inside a `<p>`:
  - The `<span>`’s listener fires  
  - Then the `<p>`’s listener fires  
- `event.target` always refers to the **original element clicked**, even when the parent handles the event.
- Bubbling can be stopped with:
  ```js
  event.stopPropagation();
  ```

---

## **Event Delegation**
- Instead of adding listeners to many child elements, you add **one listener to a parent** and let bubbling deliver events to it.
- The parent checks `event.target` to determine which child was clicked.
- Useful when:
  - You have many similar child elements  
  - Child elements are created dynamically  
- Example:
  ```js
  p.addEventListener("click", (event) => {
    event.target.style.color = "red";
  });
  ```
  This single listener handles clicks for **all** `<span>` elements inside `<p>`.

---

# ⭐ **One‑Line Summary**
**Bubbling** = events travel upward through ancestors.  
**Delegation** = use one parent listener to handle events from many children.


# **addEventListener()**

| Concept | Summary |
|--------|---------|
| **What it does** | Listens for an event on an element and runs a function when the event happens |
| **Syntax** | `element.addEventListener("event", listener)` |
| **Event types** | `"click"`, `"input"`, `"keydown"`, `"submit"`, etc. |
| **Listener** | A function (or object with `handleEvent()`) that runs when the event fires |
| **Inline example** | `btn.addEventListener("click", () => alert("Clicked"))` |
| **Function reference example** | `element.addEventListener("click", handleClick)` |
| **Input example** | `input.addEventListener("input", () => console.log(input.value))` |
| **Where it’s used** | Buttons, forms, inputs, mouse events, keyboard events, UI interactions |

---

# **addEventListener() vs Inline Event Handlers — Condensed Table**

| Feature | `addEventListener()` | Inline Event Handler (`onclick=`) |
|--------|------------------------|-----------------------------------|
| **Where the code lives** | In your JS file | Inside the HTML tag |
| **Syntax** | `element.addEventListener("click", handler)` | `<button onclick="handler()">` |
| **Separation of concerns** | ✔ Keeps HTML clean and JS separate | ✘ Mixes HTML and JS |
| **Multiple listeners** | ✔ Can attach many listeners to the same event | ✘ Only one handler allowed per event |
| **Easier to remove** | ✔ `element.removeEventListener(...)` | ✘ Harder to remove or manage |
| **Supports advanced options** | ✔ `{ once: true }`, capture, passive, etc. | ✘ No advanced options |
| **Recommended?** | ✔ Yes — modern best practice | ✘ Only for quick demos or legacy code |

---

# **Mini Examples**

### **addEventListener()**
```js
button.addEventListener("click", () => {
  console.log("Clicked!");
});
```

### **Inline handler**
```html
<button onclick="console.log('Clicked!')">Click me</button>
```
---

# **removeEventListener() — Summary**

| Concept | Summary |
|--------|---------|
| **What it does** | Removes an event listener previously added with `addEventListener()` |
| **Syntax** | `element.removeEventListener("event", listener)` |
| **Arguments required** | Same **event type** and **same function reference** used when adding the listener |
| **Optional 3rd argument** | `options` or `useCapture` (must match what was used when adding) |
| **When it’s useful** | Stop listening after a condition, closing modals, cleaning up UI, logging out, disabling buttons |
| **Key rule** | You **must pass the exact same function**, not an anonymous arrow function |
| **Example** | ```js\nbtn.addEventListener("click", toggleBgColor);\nbtn.removeEventListener("click", toggleBgColor);\n``` |
| **Real example from lesson** | Hovering a `<p>` triggers removal of the button’s click listener |
---

# **Manipulate or Change Styles with `element.style.styleName` | `element.classListadd()`**

| Feature | `element.style` | `element.classList` |
|--------|------------------|----------------------|
| **What it does** | Sets **inline styles** directly on the element | Adds, removes, or toggles **CSS classes** |
| **Best for** | Quick, one‑off visual changes | Applying reusable CSS rules |
| **Syntax** | `element.style.property = value` | `classList.add()`, `remove()`, `toggle()`, `contains()` |
| **Direct style example** | `el.style.backgroundColor = "red"` | N/A |
| **Multiple changes** | Must set each property individually | Add multiple classes at once: `el.classList.add("a", "b", "c")` |
| **Maintainability** | Harder to maintain; mixes JS + styling | Cleaner separation (CSS handles appearance) |
| **Dynamic UI use cases** | Temporary tweaks (e.g., hide/show quickly) | Menus, themes, animations, active states |
| **Toggle example** | N/A | `menu.classList.toggle("show")` |
---

# **DOMContentLoaded**

## **What It Is**
- Fires when the **HTML** is fully loaded and parsed**.
- **Does NOT wait** for images, stylesheets, or external resources.
- So Happens **before** the `load` event.
- Great for early DOM manipulation.

---

# **Why It’s Useful**
- Lets you run JavaScript **as soon as the DOM is ready**.
---

# **Basic Syntax**
```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM is loaded");
});
```
# **Example: Change Image After DOM Loads**
```js
function changeImg() {
  const img = document.getElementById("example-img");
  img.src = "new-image.jpg";
  img.alt = "New alt text";
}

if (document.readyState === "loading") {
  document.addEventListener("DOMContentLoaded", changeImg);
} else {
  changeImg(); // DOM already loaded
}
```
# JS **setTimeout() setInerval()** TIMING METHODS
- Both take 2 parmeters
  - A function
  - The delay in time
- id is a unique number returned by setTimeout() & setInterval()
  - id identifies **that specific timer**.
  - Store in a variable **So that timer can be cancelled later**.


| **Method** | **What It Does** | **Syntax & Parameters** | **Cancel Method** | **Detailed Example** |
|-----------|------------------|--------------------------|--------------------|-----------------------|
| **`const timeout Id = setTimeout(fn, delay time)`** | Runs a function **once** after a specified delay. Great for delayed actions, animations, notifications, staged UI changes. | ``` **fn:** function to run once.  **delay time:** in milliseconds. | ```clearTimeout(id);\n``` Stops the timeout **before** it executes. | ```const id = setTimeout(() => {  console.log('Runs after 3s');\n}, 3000);\n\n// Cancel before it fires\nclearTimeout(id);\n``` |
| **`const intervalID = setInterval()`** | Runs a function **repeatedly** at fixed intervals. Useful for clocks, auto‑refreshing data, animations, polling, counters. | ```setInterval(fn, delay time);\n``` **fn:** function to run repeatedly. **delay time:** between runs in ms. | ```clearInterval(id);\n``` Stops the repeating loop. | ```const id = setInterval(() => {\n  console.log('Every 2s');\n}, 2000);\n\n// Stop after 6 seconds\nsetTimeout(() => clearInterval(id), 6000);\n``` |
| **Via User Interaction** | Allows users to **cancel** a timeout or interval using buttons, clicks, or other events. Perfect for “Stop Timer,” “Cancel Loading,” or “Pause Animation.” | No special syntax — just call `clearTimeout()` or `clearInterval()` inside an event listener. | Same cancel methods: `clearTimeout(id)` or `clearInterval(id)` depending on what you’re stopping. | ```const id = setTimeout(() => {\n  console.log('Will run unless canceled');\n}, 5000);\n\n// User cancels it\nbutton.addEventListener('click', () => {\n  clearTimeout(id);\n  console.log('Canceled by user');\n});\n``` |
---

# **`requestAnimationFrame()` to set up Animation Loops**

## **What `requestAnimationFrame()` Does**
- Schedules your animation code to run **right before the browser’s next repaint**.
---

## **Basic Usage**
You pass a callback function that represents **one frame** of your animation:

```js
requestAnimationFrame(callback);
```

---

## **Setting Up an Animation Loop**
You create two functions:

### **1. `update()`**
- Changes the animation state (position, style, rotation, etc.).

### **2. `animate()`**
- Calls `update()`
- Requests the next animation frame

```js
function update() {
  element.style.transform = `translateX(${position}px)`;
  position += 2;
}

function animate() {
  update();
  requestAnimationFrame(animate); // loop
}
```

To Start the loop:

```js
requestAnimationFrame(animate);
```

The loop continues until you stop calling `requestAnimationFrame()`.
---

## **Example Behavior**
- A rectangle moves 2px to the right every frame.
- When it exits the screen, its position resets to the left side.

---

## **Why Use `requestAnimationFrame()` Instead of `setInterval()`**
- Smoother animations (syncs with screen refresh rate).
---

# **eb Animations API (WAAPI)**

## **What WAAPI Is**
- **Web Animations API** To create and control animations **in JavaScript**.  

---

## **How It Works**
You animate an element using:

```js
element.animate(keyframes, options);
- **keyframes** → list of style changes over time  
- **options** → duration, easing, direction, iterations, etc.
```
Example:
```js
const animation = element.animate(
  [{ transform: "translateX(0)" }, { transform: "translateX(100px)" }],
  { duration: 2000, iterations: Infinity, direction: "alternate" }
);
```
## **Animation Object Controls**
The `.animate()` method returns an **Animation object** containing animation controls:

### **Instance Methods**
- `play()`
- `pause()`
- `reverse()`
- `finish()`
- `cancel()`

### **Instance Properties**
- `playState`
- `currentTime`
- `playbackRate`
- `startTime`
- `effect`
- `timeline`
- `finished`
- `onfinish`
- `oncancel`

** These allow you to animation events**.
---

## **Example: Play / Pause**
```js
const animation = square.animate([...], { duration: 5000 });

animation.onfinish = () => console.log("Animation finished!");

playBtn.addEventListener("click", () => animation.play());
pauseBtn.addEventListener("click", () => animation.pause());
```

---
# **WAAPI vs CSS Animations**

| **CSS Animations** | **WAAPI (JavaScript)** |
|--------------------|------------------------|
| Declarative (defined in CSS) | Imperative (controlled in JS) |
| Great for simple, automatic animations | Great for interactive, dynamic animations |
| Harder to control at runtime | Easy to pause, play, reverse, change speed |
| Triggered by classes, states, or events | Controlled directly through JS methods |
| Best for hover effects, loops, transitions | Best for user‑driven or complex animations |
---

## **How They Relate**
- WAAPI can **do CSS animations**, but with **more run time control**.
- WAAPI animations is better to respond to **clicks, scrolls, input, or dynamic logic**.
---

# **Open and Close Dialog Elements with JavaScript**

| **Concept** | **Explanation** | **Code Pattern** |
|-------------|-----------------|------------------|
|**What are Dialogs?| They let you display info or actions to the user.| — |
|**How to create Dialogs? | Use the HTML Dialog element| — |
| **What the `<dialog>` element does** | The `<dialog>` element creates **modal** and **non‑modal** pop‑ups. Modal dialogs block interaction with the rest of the page. Non‑modal dialogs allow the user to keep interacting with the page. | — |
| **How dialogs are controlled in JavaScript** | Dialogs use three main methods: **`showModal()`** (opens a modal dialog with a backdrop), **`show()`** (opens a non‑modal dialog), and **`close()`** (closes the dialog). Dialogs are typically opened through button clicks and closed using a button inside the dialog. | — |
| **Common usage patterns & ideal use cases** | Common patterns: `dialog.showModal()`, `dialog.show()`, `dialog.close()`. Dialogs are ideal for confirmations, alerts, forms, and any UI that requires focused user attention. | — |
| **Dialog element** | Built‑in HTML element for pop‑ups; hidden by default. | ```html\n<dialog id="modal">...</dialog>``` |
| **Modal dialog** | Blocks interaction with the rest of the page; adds backdrop. | ```dialog.showModal();``` |
| **Non‑modal dialog** | Allows interaction with the page while open. | ```dialog.show();``` |
| **Open on page load** | Automatically displays the dialog when script runs. | ```dialog.showModal();``` |
| **Open via button** | User clicks a button to open the dialog. | ```openBtn.addEventListener('click', () => dialog.showModal());``` |
| **Open non‑modal via button** | Opens dialog without blocking the page. | ```openBtn.addEventListener('click', () => dialog.show());``` |
| **Close dialog** | Hides the dialog and removes backdrop. | ```dialog.close();``` |
| **Close via button inside dialog** | Button inside dialog triggers close. | ```closeBtn.addEventListener('click', () => dialog.close());``` |
| **Use cases** | Forms, confirmations, alerts, focused user actions. | — |


# **Inline Event Handlers vs addEventListener()**

| Feature | **Inline Event Handlers** (`onclick=""`) | **addEventListener()** (Best Practice) |
|--------|-------------------------------------------|-----------------------------------------|
| **Where code lives** | Inside the HTML attribute | In your JavaScript file |
| **Separation of concerns** | ❌ Mixes HTML + JS | ✔ Keeps HTML and JS separate |
| **Number of listeners allowed** | Only **one** per event | **Multiple** listeners allowed |
| **Maintainability** | Harder to read, harder to scale | Cleaner, organized, easier to maintain |
| **Supports advanced options** | ❌ No (`once`, `passive`, `capture`) | ✔ Yes |
| **Removing listeners** | ❌ Cannot remove easily | ✔ `removeEventListener()` works |
| **Modern best practice** | ❌ Not recommended | ✔ Recommended |
| **Example** | `<button onclick="alert('Hi')">` | `btn.addEventListener("click", handler)` |
---


# **Canvas API**

| **Concept** | **Explanation** | **Example Pattern** |
|-------------|-----------------|----------------------|
| **What the Canvas API is** | A JavaScript API for drawing text --> games a `<canvas>` element. | — |
| **How to setup** | Add a canvas html element in element set Width/height or JS. | ```html\n<canvas id="my-canvas" width="400" height="400"></canvas>``` |
| **Get the canvas + context** | Access the element, then get its **2D drawing context**. | ```const canvas = document.getElementById('my-canvas');\nconst ctx = canvas.getContext('2d');``` |
| **What context/ctx is** | `CanvasRenderingContext2D` object contains all drawing methods (colors, shapes, text, lines). | — |
| **Draw a filled rectangle** | Use `fillStyle` to set color, then `fillRect()` to draw. | ```ctx.fillStyle = 'crimson';\nctx.fillRect(1, 1, 150, 100);``` |
| **Draw text** | Set font + color, then draw text at an (x, y) position. | ```ctx.font = '30px Arial';\nctx.fillStyle = 'crimson';\nctx.fillText('Hello HTML Canvas!', 1, 50);``` |
| **Coordinates** | Canvas uses an (x, y) grid starting at the **top‑left corner**. | — |
| **Animation capability** | Combine Canvas drawing with `requestAnimationFrame()` for smooth custom animations. | ```function animate() {\n  update();\n  requestAnimationFrame(animate);\n}``` |
| **Canvas lets you build** | Shapes, charts, visual effects, particle systems, games, interactive graphics. | — |
|**Key Interfaces**|Purpose|
|**HTMLCanvasElement**| → the canvas element  |
|**CanvasRenderingContext2D** |→ drawing methods |
|**CanvasGradient**, **CanvasPattern**, **TextMetrics**| → advanced graphics tools  |
---

## **innerHTML | createElement() **

| Feature | innerHTML | createElement() |
|--------|-----------|------------------|
| Creates nodes | Yes (via HTML string) | Yes (one element at a time) |
| Safety | Risky with user input | Safe |
| Speed | Fast for large chunks | Fast for small updates |
| Control | Low (string-based) | High (node-based) |
| Replaces existing content | Yes (unless concatenated) | No |
|**Used for**|quick insertion|dynamic, user-driven content|
||Replaces all HTML and content|set attributes, classes, events|
---

# **innerText | textContent | innerHTML ** COMPARISON

| Feature | innerText | textContent | innerHTML |
|--------|-----------|-------------|-----------|
| Returns | Visible text only | All text | HTML markup |
| Includes hidden text | No | Yes | Yes |
| Triggers reflow | Yes | No | No |
| Safe for user input | Yes | Yes | **No** |
| Replaces children when set | Yes | Yes | Yes (parses HTML) |
| Best use | Visible UI text | Raw text | Insert/read HTML |

---
# **innerHTML vs createElement()**

| **innerHTML** | **createElement()** |
|---------------|----------------------|
| Uses an HTML **string** to generate all nodes at once. | Creates each node **programmatically**, one at a time. |
| Fast for inserting chunks of markup. | Safer and more controlled for dynamic content. |
| Risky with user input (XSS). | Safe for user‑generated content. |

---
# **Setting Attributes, Classes, and Events**

| Action | How You Do It | Example |
|--------|----------------|---------|
| **Set an attribute** | Use dot notation or `setAttribute()` | `img.src = "photo.jpg"`<br>`img.setAttribute("alt", "A cat")` |
| **Add/remove classes** | Use `classList` | `div.classList.add("active")`<br>`div.classList.remove("hidden")` |
| **Toggle classes** | `classList.toggle()` | `button.classList.toggle("open")` |
| **Check if a class exists** | `classList.contains()` | `div.classList.contains("error")` |
| **Add an event listener** | `addEventListener()` | `li.addEventListener("click", () => { ... })` |
| **Set inline styles** | Modify `.style` | `p.style.color = "red"` |
---

# **DOM Manipulation, Web APIs + Event Handling Table**

| **Topic** | **Condensed Explanation** | **Example** | **Example Explanation** |
|----------|----------------------------|-------------|--------------------------|
| **API** | Rules that let software communicate. | `fetch("https://api.com")` | Calls an external API to request data from a server. |
| **Web APIs** | APIs used in web development. | `document.querySelector("p")` | Uses a built‑in browser API to select a paragraph element. |
| **Browser APIs** | Built into the browser (DOM, window, navigator). | `localStorage.setItem("theme", "dark")` | Stores data in the browser using a built‑in API. |
| **Third‑Party APIs** | External services you load separately. | Google Maps API | Loads map features that are not built into the browser. |
| **DOM** | Tree structure of the webpage; JS can modify it. | `document.body.style.background = "black"` | Changes the background color of the page by modifying the DOM. |
| **DOM Structure Terms** | Root, parent, child relationships. | `<ul>` → `<li>` | The `<ul>` is the parent and each `<li>` is a child element. |
| **navigator** | Info about browser/device. | `navigator.userAgent` | Returns a string describing the browser and operating system. |
| **window** | Represents the browser window. | `window.open("https://example.com")` | Opens a new browser tab or window. |
| **getElementById()** | Selects one element by its unique ID. | `document.getElementById("header")` | Selects the element whose id is `"header"` in the DOM. |
| **querySelector()** | Selects the first matching element. | `document.querySelector("#apple")` | Selects the **first** element in the DOM with the id `"apple"`. |
| **querySelectorAll()** | Selects all matching elements. | `document.querySelectorAll("li")` | Selects **every** `<li>` element in the DOM. |
| **innerHTML** | Inserts or replaces HTML markup. | `div.innerHTML = "<p>Hello</p>"` | Replaces the inside of `div` with a new `<p>` element. |
| **innerText** | Returns visible text only. | `div.innerText` | Returns only the text the user can see inside the element. |
| **textContent** | Returns all text, even hidden. | `div.textContent` | Returns all text inside the element, including hidden text. |
| **createElement()** | Creates a new HTML element. | `document.createElement("img")` | Creates a new `<img>` element in memory (not yet on the page). |
| **appendChild()** | Adds a node as the last child. | `list.appendChild(item)` | Adds `item` to the end of the list in the DOM. |
| **removeChild()** | Removes a specific child node. | `parent.removeChild(child)` | Removes the `child` element from its parent in the DOM. |
| **setAttribute()** | Adds or updates an attribute. | `img.setAttribute("src", "photo.jpg")` | Sets the `src` attribute of the `<img>` to `"photo.jpg"`. |
| **Event Object** | Every interaction creates an Event object with details like `type` and `target`. | `e.target.value` | Reads the value of the element that triggered the event. |
| **Event Target Access** | Use `event.target` to access the exact element that fired the event. | `console.log(e.target)` | Logs the specific element the user interacted with. |
| **addEventListener()** | Attaches a function to run when an event occurs. | `btn.addEventListener("click", handler)` | Runs `handler` when the button is clicked. |
| **removeEventListener()** | Removes a previously added event listener. | `btn.removeEventListener("click", handler)` | Stops the button from running `handler` on click. |
| **Inline Event Handlers** | Old‑style event attributes in HTML; not recommended. | `<button onclick="alert('Hi')">` | Runs the alert when clicked, but mixes JS with HTML. |
| **change Event** | Fires when input values change (select, checkbox, radio). | `select.addEventListener("change", e => ...)` | Runs code when the user picks a new option. |
| **Event Bubbling** | Events bubble from the target up through parent elements. | `e.stopPropagation()` | Prevents the event from bubbling to parent elements. |
| **Event Delegation** | Listen on a parent instead of many children. | `list.addEventListener("click", e => ...)` | Handles clicks on all list items using one listener. |
|||takes advantage of this by attaching one listener to aparent instead of many listeners to individual child elements||
| **DOMContentLoaded** | Fires when HTML is fully parsed. | `document.addEventListener("DOMContentLoaded", init)` | Runs `init` once the DOM is ready. |
| **element.style** | Sets inline CSS styles directly on an element. | `el.style.color = "red"` | Changes the text color of the element to red. |
| **classList.add()** | Adds a CSS class to an element. | `el.classList.add("active")` | Adds the `"active"` class to the element. |
| **classList.remove()** | Removes a CSS class. | `el.classList.remove("hidden")` | Removes the `"hidden"` class so the element becomes visible. |
| **classList.toggle()** | Adds the class if missing, removes it if present. | `menu.classList.toggle("open")` | Shows or hides the menu depending on its current state. |
| **setTimeout()** | Runs code once after a delay. | `setTimeout(() => console.log("Hi"), 2000)` | Prints “Hi” after 2 seconds. |
| **setInterval()** | Runs code repeatedly at a set interval. | `setInterval(() => console.log("tick"), 1000)` | Prints “tick” every second. |
| **clearInterval()** | Stops a running interval. | `clearInterval(id)` | Stops the interval stored in `id`. |
| **requestAnimationFrame()** | Runs animation steps synced to screen refresh. | `requestAnimationFrame(animate)` | Schedules the next animation frame smoothly. |
| **Animation Loop Pattern** | Common pattern for smooth animations. | `function animate(){ update(); requestAnimationFrame(animate); }` | Repeats `update()` every frame for fluid animation. |


# **Web Animations, Canvas, and Dialogs**

| **Topic** | **Condensed Explanation** | **Example** | **Example Explanation** |
|----------|----------------------------|-------------|--------------------------|
| **Web Animations API** | Lets you create and control animations directly in JavaScript using keyframes + options. | ```js square.animate([{ transform:'translateX(0px)' },{ transform:'translateX(100px)' }],{ duration:2000, iterations:Infinity, direction:'alternate', easing:'ease-in-out' }); ``` | Animates the square left → right → left forever with smooth easing. |
| **Animation Keyframes** | Define the visual changes during the animation. | `{ transform: 'translateX(100px)' }` | Moves the element 100px horizontally. |
| **Animation Options** | Control timing, duration, loops, easing, direction. | `{ duration: 2000, iterations: Infinity }` | Makes the animation last 2 seconds and loop forever. |
| **Canvas API** | Provides a 2D drawing surface for shapes, text, images, and animations. | `const ctx = canvas.getContext('2d')` | Gets the 2D drawing context used to draw on the canvas. |
| **Canvas Drawing** | Use context methods to draw shapes and graphics. | `ctx.fillRect(1, 1, 150, 100)` | Draws a filled rectangle on the canvas. |
| **Canvas Styling** | Set colors, gradients, patterns before drawing. | `ctx.fillStyle = 'crimson'` | Sets the fill color for shapes drawn afterward. |
| **Dialog Element** | Built‑in HTML element for modal and non‑modal dialogs. | `<dialog id="my-modal"></dialog>` | Creates a dialog box that JS can open or close. |
| **showModal()** | Opens a modal dialog that blocks page interaction. | `dialog.showModal()` | Opens the dialog and prevents clicking outside it. |
| **show()** | Opens a non‑modal dialog. | `dialog.show()` | Opens the dialog while still allowing page interaction. |
| **close()** | Closes a dialog. | `dialog.close()` | Hides the dialog and returns control to the page. |
| **Open Modal Button** | Use events to trigger dialog actions. | `openBtn.addEventListener('click', () => dialog.showModal())` | Clicking the button opens the modal dialog. |
| **Close Modal Button** | Attach event to close the dialog. | `closeBtn.addEventListener('click', () => dialog.close())` | Clicking the button closes the dialog. |
---

# 🎧 **JavaScript Audio & Video **

| **Topic** | **Definition / Purpose** | **Example** |
|----------|---------------------------|-------------|
| **Audio() Constructor** | Creates an `HTMLAudioElement` programmatically | ```const sound = new Audio("song.mp3"); sound.play();``` |
| **Audio() Methods** | once created Use to control | const audio = document.getElementById("audio"); |
| **play()** | Starts audio/video playback | ```audio.play();``` |
| **pause()** | Pauses playback but keeps current position | ```audio.pause();``` |
| **addTextTrack()** | Adds captions/subtitles to video | ```const track = video.addTextTrack("captions","English","en");``` |
| **fastSeek()** | Jumps to a specific time in media | ```audio.fastSeek(30);``` |
| **Audio() constructor Properties** | |  |
| **currentTime** | Gets/sets playback position/time | ```audio.currentTime = 10;``` |
| **loop** | Automatically restarts audio when finished | ```audio.loop = true;``` |
| **muted** | Silences audio output | ```audio.muted = true;``` |
| **Audio() & Video Formats** | |  |
| **MIME Type** Multipurpose Internet Mail Extension| Tells browser type of file being loaded | ```<source src="song.mp3" type="audio/mpeg">``` |
| **source Element** | states type and src to allow browser to choose format | ```<video><source src="video.mp4" type="video/mp4"><source src="video.webm" type="video/webm"></video>``` |
| **MP3 Format** | Compressed digital audio format (MIME type`audio/mpeg`) | ```<audio src="track.mp3"></audio>``` |
| **MP4 Format** | figital audio + video MIME (`audio/mp4` or `video/mp4`) | ```<video src="movie.mp4"></video>``` |
| **Codecs** | algorithm to convert audio/video between analogue and digital | ```<source src="movie.mp4" type='video/mp4; codecs="avc1.42E01E"'>``` |
| **HTMLMediaElement API** | Controls audio/video behaviour of (play, pause, etc.) | ```gives access to basic methods and to events like waiting, ended, canplay, canplaythrough``` |
| What canPlayType() method help you do||Determine if a browser is likely to be able to play your specific audio format.| 
| What HTMLMediaElement event fires when playback is paused due to data buffering?||waiting| 
| Which Web Audio API interface is used to represent an audio-processing graph?||AudioContext|
| When is the ended event fired?||When the end of the media has been reached.|
| **Media Capture & Streams API** | Captures audio/video from user devices. It creates MediaStream object| ```navigator.mediaDevices.getUserMedia({audio:true, video:true}).then(stream => video.srcObject = stream);``` |
| **Screen Capture API** | Records user’s screen, call object navigator and mediaDevices| ```navigator.mediaDevices.getDisplayMedia().then(stream => video.srcObject = stream);``` |
| **MediaStream Recording API** | Records a MediaStream works with MediaStreams API | ```const recorder = new MediaRecorder(stream); recorder.start();``` |
| **Media Source Extensions API** | Pass webcam Feeds to video element with srcObject| ```video.srcObject = webcamStream;``` |
| **Web Audio API** | Audio processing on web. Objects: AudioBuffer & AudioContext| ```const ctx = new AudioContext(); const src = ctx.createBufferSource(); src.connect(ctx.destination);``` |
---

# 🔊 **Audio Constructor & HTMLMediaElement — Master Table**

## **Audio Constructor**
| Topic | Details |
|-------|---------|
| **Audio() Constructor** | A constructor that creates an `HTMLAudioElement` when used with `new` |
| Purpose | Play audio or insert into DOM for user controls |
| Argument | Optional URL to an audio file |
| Example | `const audio = new Audio("sound.mp3")` |
| Change source later | `audio.src = "newfile.mp3"` |
---

## 🎵 **Common Audio Methods**
| Category | Method | Description |
|----------|--------|-------------|
| Playback | `play()` | Starts audio playback |
| Playback | `pause()` | Pauses playback but keeps position |
| Stopping workaround | *(no `stop()`)* | Use `pause()` + `audio.currentTime = 0` |
| Format support | `canPlayType()` | Returns if browser can likely play a format |
---

## 🎧🎥 **MIME Types Overview**
| Topic | Details |
|-------|---------|
| Definition | Identifiers telling software how to handle a file |
| Purpose | Helps browsers know how to embed/play files |
| Examples | `text/html`, `application/json`, `application/microsoft-executable` |

---

## **Common Audio & Video Formats**
| Format | Type | Notes |
|--------|------|-------|
| MP3 | `audio/mpeg` | Most common audio |
| MP4 | `audio/mp4`, `video/mp4` | Audio or audio+video |
| WAV | audio | Uncompressed waveform |
| OGG | audio/video | Open format |
| MOV | video | Apple format |
| WMV | video | Windows Media Video |
| WebM | video | Web‑optimized |
| MKV | video | Supports many codecs |

---

## 🎛️ **Why Format Differences Matter**
| Reason | Explanation |
|--------|-------------|
| Compatibility | Different browsers/devices support different formats |
| User experience | Ensures smooth playback |

---

## **Using `<source>` for Compatibility**
| Element | Purpose |
|---------|----------|
| `<audio>` / `<video>` | Can contain multiple `<source>` tags |
| `<source>` attributes | File URL + MIME type |
| Browser behavior | Automatically picks the best supported format |

---

## 🎚️ **Codecs**
| Topic | Details |
|-------|---------|
| Definition | Encoder/decoder algorithm for audio/video |
| Purpose | Compress, store, and play efficiently |
| MIME syntax | `media/type; codecs="codecName"` |
| Examples | `video/webm; codecs="vp8, vorbis"`<br>`video/mp4; codecs="avc1.4d002a"` |

---

## 🎛️ **Why Codecs Matter**
| Factor | Impact |
|--------|--------|
| File size | Compression efficiency |
| Quality | Depends on codec |
| Compatibility | Browser/device support varies |
| Browser use | Browser checks codec info before playing |

---

## 🧩 **Where Codecs Are Used**
| Location | Purpose |
|----------|----------|
| `<source>` type attribute | Helps browser choose playable media |
| `MediaSource.isTypeSupported()` | Returns `true`/`false` for MIME+codec support |

---

## 🎥 **HTMLMediaElement API**
| Topic | Details |
|-------|---------|
| What it is | API controlling audio/video elements |
| Extends | `HTMLElement` |

### Common Methods
| Method | Description |
|--------|-------------|
| `play()` | Start playback |
| `pause()` | Pause playback |
| `addTextTrack()` | Add subtitles/captions |
| `fastSeek(time)` | Jump quickly to a time |

### Media Events
| Event | Meaning |
|--------|---------|
| `play` | Playback started |
| `pause` | Playback paused |
| `ended` | Media finished |
| `waiting` | Buffering |
| `canplay` | Enough data to start playing |
| `canplaythrough` | Browser expects no buffering |

---

## 📸 **MediaStream API**
| Topic | Details |
|-------|---------|
| Purpose | Capture audio/video from camera/mic |
| Part of | Media Capture and Streams API |

### Creating a MediaStream
| Method | Description |
|--------|-------------|
| `new MediaStream()` | Creates empty stream (no hardware) |
| `navigator.mediaDevices.getUserMedia()` | Requests hardware access, returns Promise |

### Constraints Object
| Property | Meaning |
|----------|---------|
| `audio: true/false` | Request audio |
| `video: true/false or object` | Request video or specify resolution |

---

## 📹 **High‑Resolution Video Example**
| Setting | Values |
|---------|--------|
| Width | min: 1280, ideal: 1920, max: 3840 |
| Height | min: 720, ideal: 1080, max: 2160 |

Code:
```js
navigator.mediaDevices.getUserMedia({
  audio: true,
  video: {
    width: { min: 1280, ideal: 1920, max: 3840 },
    height: { min: 720, ideal: 1080, max: 2160 }
  }
});
```

---

## 🎥 **Working With a Stream**
| Step | Code |
|------|------|
| Select video element | `const video = document.querySelector("video")` |
| Get stream | `const stream = await navigator.mediaDevices.getUserMedia({ video: true })` |
| Attach stream | `video.srcObject = stream` |
| Play | `await video.play()` |

---

## 🧰 **Other Video & Audio APIs**
| API | Purpose |
|------|---------|
| Screen Capture API (`getDisplayMedia()`) | Capture user’s screen |
| MediaStream Recording API | Record audio/video |
| Media Source Extensions (MSE) | Feed streams into media elements |
| Web Audio API | Process, filter, and manipulate sound |

---

## 📺 **Screen Capture Example**
```js
const stream = await navigator.mediaDevices.getDisplayMedia({
  video: true,
  audio: true
});
```


