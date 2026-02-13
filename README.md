# JAVASCRIPT-Working-with-the-DOM

---

# **querySelectorAll() **

## **What is it?**
A DOM method that finds **all elements** matching a given **CSS selector string**.

## **What is it called on?**
- `document.querySelectorAll()` → searches the **entire page**  
- `element.querySelectorAll()` → searches **only inside that element**

---

## **How to use it**
```js
const matches = document.querySelectorAll("selector");
```

### **Complex selector example**
```js
document.querySelectorAll("ul.ingredients li");
```
Selects all `<li>` elements inside a `<ul>` with class `"ingredients"`.

---

## **Errors**
Throws a **SyntaxError** if the selector string is invalid.

---

# **What it returns (NodeList)**

A **NodeList**, which is an array‑like collection of elements.

### **Possible outputs depending on the page**

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

---

## **When should you use it?**
**select and manipulate multiple elements at once on (tags, classes, attributes, or nested relationships)**.

---

# **Creating New DOM Nodes: innerHTML or createElement()**

## **1. innerHTML**
**What it does:**  
Sets the HTML markup *inside an existing element* using a string. The browser parses the string and creates all necessary nodes.

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
**What it does:**  
Creates a **new element node** programmatically, one at a time.

**Example:**
```js
const container = document.getElementById("container");

const img = document.createElement("img");
img.src = "https://cdn.freecodecamp.org/curriculum/cat-photo-app/lasagna.jpg";
img.alt = "A slice of lasagna on a plate.";

container.appendChild(img);
```
---

# **Adding & Removing DOM Nodes**

## **1. Adding Nodes — `appendChild()`**
**What it does:**  
Adds a node to the **end** of a parent element’s list of children.

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

## **2. Removing Nodes — `removeChild()`**
**What it does:**  
Removes a **specific child node** from a parent element.

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

# **DOM Node Manipulation — Side‑by‑Side Cheat Sheet**

| Method | What It Does | Syntax | Example |
|--------|--------------|--------|---------|
| **appendChild()** | Adds a node to the **end** of a parent’s children | `parent.appendChild(node)` | `list.appendChild(li)` |
| **prepend()** | Adds a node to the **start** of a parent’s children | `parent.prepend(node)` | `list.prepend(li)` |
| **remove()** | Removes the node **itself** (no parent needed) | `node.remove()` | `li.remove()` |
| **removeChild()** | Removes a **specific child** from a parent | `parent.removeChild(child)` | `list.removeChild(li)` |
| **replaceChild()** | Replaces one child with another | `parent.replaceChild(newNode, oldNode)` | `list.replaceChild(newLi, oldLi)` |
| **insertBefore()** | Inserts a node **before** a specific child | `parent.insertBefore(newNode, referenceNode)` | `list.insertBefore(li, list.firstChild)` |

---

# **Mini Examples**

### **appendChild()**
```js
ul.appendChild(newLi);
```

### **prepend()**
```js
ul.prepend(newLi);
```

### **remove()**
```js
newLi.remove();
```

### **removeChild()**
```js
ul.removeChild(oldLi);
```

### **replaceChild()**
```js
ul.replaceChild(newLi, oldLi);
```

### **insertBefore()**
```js
ul.insertBefore(newLi, ul.children[1]);
```
---

# **Navigator, Window, and Document — Summary**

## **Navigator**
Represents **browser information**.

### What it gives you:
- Browser + OS details (`navigator.userAgent`)
- User’s preferred language (`navigator.language`)

### Examples:
```js
navigator.userAgent      // "Mozilla/5.0 … Chrome/128…"
navigator.language       // "en-US"
```

**Use it for:** browser environment, UI, features.

---

## **Window**
Represents the **browser window** itself.  
It is the **global object** in the browser.

### What it gives you:
- Window size (`innerWidth`, `innerHeight`)
- Current URL (`location`)
- Methods for opening, navigating, timers, etc.

### Examples:
```js
window.innerWidth        // width in pixels
window.location          // URL info object
location                 // same as window.location
```

**Use it for:** window info, navigation, timers, global properties.

---

## **Document**
Represents the **DOM tree** inside the window.

### What it gives you:
- Selecting elements (`querySelector`, `getElementById`)
- Creating elements (`createElement`)
- Reading/modifying content (`textContent`, `innerHTML`)
- Document structure (`document.children`)

### Example:
```js
document.children        // HTMLCollection of top-level nodes
```
---

# **Quick Comparison Table**

| Interface | Represents | Common Uses |
|----------|------------|-------------|
| **Navigator** | Browser environment | User agent, language |
| **Window** | Browser window (global object) | Size, URL, navigation, timers |
| **Document** | The DOM inside the window | Selecting, creating, editing elements |

---

# **setAttribute() — Summary**

## **What it does**
Adds a **new attribute** or **updates an existing attribute** on an HTML element.

---

## **Syntax**
```js
element.setAttribute(attributeName, value);
```

---

## **Basic Example**
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

---

## **Updating an Existing Attribute**
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

---

## **Real‑World Uses**
- Updating an image’s `src` when a user clicks a thumbnail  
- Adding form validation attributes (`required`, `minlength`)  
- Setting `data-*` attributes for dynamic UI behavior  

---

# **Event Object — Summary**

| Feature | What It Means | Example / Notes |
|--------|----------------|-----------------|
| **What it is** | A payload created when the user interacts with the page | Clicks, key presses, form submits, device motion |
| **`type`** | The kind of event that occurred | `"click"`, `"keydown"`, `"submit"` |
| **`target`** | The element (or object) that triggered the event | Usually an HTMLElement, but could be `document`, `window`, or others |
| **`preventDefault()`** | Stops the browser’s default behavior | Prevent form submission, stop link navigation |
| **`stopPropagation()`** | Stops the event from bubbling to parent elements | Useful in nested click handlers |
| **Event‑specific properties** | Extra data depending on event type | Example: `FetchEvent.request`, `KeyboardEvent.key`, `MouseEvent.clientX` |
| **How to inspect it** | Log the event to see all available properties | `console.log(event)` |

---

# **addEventListener() — Summary**

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

# **Manipulate or Change Styles with `element.style.styleName` | `element.classListadd()` — Summary**

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

# **Inline Event Handlers vs addEventListener() — Table**

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
## **innerHTML | createElement() - Summary**

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

# **innerText | textContent | innerHTML Quick Comparison Table**

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
# **Setting Attributes, Classes, and Events — Quick Table**

| Action | How You Do It | Example |
|--------|----------------|---------|
| **Set an attribute** | Use dot notation or `setAttribute()` | `img.src = "photo.jpg"`<br>`img.setAttribute("alt", "A cat")` |
| **Add/remove classes** | Use `classList` | `div.classList.add("active")`<br>`div.classList.remove("hidden")` |
| **Toggle classes** | `classList.toggle()` | `button.classList.toggle("open")` |
| **Check if a class exists** | `classList.contains()` | `div.classList.contains("error")` |
| **Add an event listener** | `addEventListener()` | `li.addEventListener("click", () => { ... })` |
| **Set inline styles** | Modify `.style` | `p.style.color = "red"` |

---

