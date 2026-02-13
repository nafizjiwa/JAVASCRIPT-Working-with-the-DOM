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

## **Summary Comparison**

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

# **Quick Comparison Table**

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

