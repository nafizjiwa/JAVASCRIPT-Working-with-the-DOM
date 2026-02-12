# JAVASCRIPT-Working-with-the-DOM

---

# **querySelectorAll() — Summary **

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

---

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
Whenever you need to **select and manipulate multiple elements at once** based on shared CSS characteristics (tags, classes, attributes, or nested relationships).

---
