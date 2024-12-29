# RecipeVault

HTML-CSS  Design with a responsive layout for seamless browsing on both desktop and mobile devices.



Learnings in this project are as follows -


# **how do I paste image in readme.md file from VS code editor**

* To include an image in your `README.md` file from VS Code, follow these steps:

  ### 1. **Add the Image to Your Project Folder**
  * Place the image file in your project directory (e.g., in an `assets` or `images` folder).

  ### 2. **Reference the Image in** `README.md`
  * Use Markdown syntax to link the image. For example:

    ```markdown
    ![Alt text](relative/path/to/image.png)
    ```
  * Replace `relative/path/to/image.png` with the relative path to your image file from the location of your `README.md` file.
  * BUT MOST IMPORTANTLY YOU SHOULD TYPE IT IN CODE FILE , THEN PASTE IT ON README FILE , BECAUSE IT’S NOT EASY TO EDIT ABOVE CODE IN README . ALSO TO SEE CHANGES GOTO README FILE IN FOLDER AND RIGHT CLICK AND SELECT PREVIEW OPTION.

  Example:

  ```markdown
  ![Delicious Recipe](images/recipe-example.png)
  ```

  ### 3. **Paste Image Directly into VS Code**
  * If you have an image copied to your clipboard, you can use an extension like **"Paste Image"** in VS Code:

    
    1. Install the [Paste Image](https://marketplace.visualstudio.com/items?itemName=mushanshitiancai.vscode-paste-image) extension.
    2. In your `README.md`, position the cursor where you want the image reference.
    3. Paste the image (`Ctrl+V` or `Cmd+V`).
    4. The extension will save the image to a predefined folder (e.g., `images`) and automatically insert the Markdown syntax for the image.

  ### 4. **Preview the Markdown**
  * Right-click in your `README.md` file and select **"Open Preview"** or press `Ctrl+Shift+V` (Windows/Linux) or `Cmd+Shift+V` (Mac) to see how the image appears.

  Let me know if you need more help!


# How to create a new repository for any new project

 ![New](assets/new.png)

 ![Clone](assets/clone.png "left-50")






1. Clone this git CODE in vs code . you will see that you are working on main branch .
2. to be more practical in git , create a branch inside git and work on these branches , and keep on merging the code in the main branch. again always create a branch from main only.

# Why we often set `box-sizing: border-box ?`

### Default Behavior (`content-box`)

By default, the `box-sizing` property is set to `content-box`. In this mode:

* The **width** and **height** of an element only include the content.
* Padding and borders are added **outside** the specified width and height, which can cause elements to grow unexpectedly.

For example:

```css
div {
  width: 200px; /* Only content width */
  padding: 20px; /* Adds 40px total */
  border: 10px solid black; /* Adds 20px total */
}
```

The element's total width becomes **260px** (200 + 40 + 20), which can make layout calculations tricky.


---

### Using `border-box`

When `box-sizing: border-box` is applied:

* The **width** and **height** include content, padding, and borders.
* This means the element’s total size stays consistent with the width and height you specify.

For the same example:

```css
div {
  box-sizing: border-box;
  width: 200px; /* Includes content, padding, and border */
  padding: 20px;
  border: 10px solid black;
}
```

The total width remains **200px**, making it much easier to manage layouts.


---

### Benefits of `border-box`


1. **Predictable Layouts**: The size you set is the size you get, which reduces unexpected overflow and makes layout planning straightforward.


---

# Why do we always set `min-height: 100vh` and `width: 100%`



---

### Why `min-height: 100vh`?


1. **Viewport Relative Units for Height (**`100vh`):
   * `100vh` ensures the element’s height covers the **entire height of the viewport**, regardless of its content.
   * Using `min-height` allows the element to expand if its content exceeds the viewport height.
2. **Dynamic Content**:
   * For many layouts, vertical scrolling is more common. Using `min-height` ensures the container grows as needed for additional content.


---

### Why `width: 100%`?


1. **Percentage Units for Width (**`100%`):
   * `width: 100%` ensures the element stretches across the entire width of its parent or the viewport.
   * This works well because, unlike height, the content in most layouts naturally expands horizontally, so a **minimum width** isn't as important.
2. **No Horizontal Overflow by Default**:
   * Content doesn’t typically overflow horizontally (due to how text wraps), so `min-width` isn’t commonly needed in most layouts.


---

### Why Not Use `height: 100vh` or `min-width: 100vh`?


1. `height: 100vh`:
   * If you set `height: 100vh`, the element's height becomes **fixed** at the viewport height, even if the content overflows. This can cause issues where content gets **cut off** and scrolling is disabled unintentionally.
2. `min-width: 100vh`:
   * `vh` is a **vertical unit** and has no direct relation to the width of the viewport. Using `min-width: 100vh` can lead to unpredictable results because it bases the width on the height of the viewport instead of the width.


---

### Why Not Use `width: 100%` and `height: 100%` Together?


1. **Behavior of \`% Units**:
   * `width: 100%` works fine because it stretches the element to match its parent’s width (usually the viewport width).
   * `height: 100%`, however, depends on the **height of the parent**. If the parent doesn’t have a fixed height or a height defined, the element with `height: 100%` might collapse to `0` because percentages need a reference point.

   **Example of collapsing height**:

   ```css
   body, html {
     width: 100%;
   }
   
   div {
     width: 100%;
     height: 100%; /* May collapse without a defined parent height */
   }
   ```
2. **Viewport Units Are More Reliable for Height**:
   * `100vh` is absolute and always represents the viewport height, while `100%` depends on the parent element’s height.


---

# If `height: 100%` depends on the parent’s height and collapses to 0 when the parent has no fixed height, why does `width: 100%` work on the `<body>` tag even when the parent’s width isn’t explicitly defined?

Ah, great observation! The reason `width: 100%` works on the `<body>` tag (or similar elements) without explicitly setting the parent’s width, while `height: 100%` often fails, lies in **how browsers handle width and height differently by default**. Let’s dive into the explanation.


---

### 1. **Default Behavior of** `html` and `body` Elements

* **Width**: The `<html>` and `<body>` elements automatically stretch their width to fill the entire viewport width (even without explicitly setting `width`).
  * By default, the browser makes the `<html>` and `<body>` elements **block-level elements**, which naturally expand to match the width of their containing block (in this case, the viewport).
  * Therefore, `width: 100%` on the `<body>` simply means "take 100% of the already stretched width of the viewport."
* **Height**: The `<html>` and `<body>` elements **do not automatically stretch their height** to match the viewport unless explicitly set.
  * If no height is specified for `<html>` or `<body>`, their height is determined by the content inside. If the content is smaller than the viewport, their height collapses to the size of the content.
  * This means `height: 100%` won’t work properly unless the height of the parent (`<html>` or `<body>`) is explicitly defined (e.g., `height: 100vh` or `height: 100%` on `<html>`).


---

### 2. **Why** `width: 100%` Works Without a Set Parent Width

* **Width Cascades by Default**: Browsers treat the width of the `<html>` element as 100% of the viewport width by default. When you apply `width: 100%` to the `<body>` or its child elements, it simply inherits this width from the `<html>` element, which is already stretched to the full viewport width.
  * Even without explicitly setting `width: 100%` on `<html>`, it behaves as though `width: 100%` is applied because browsers assume that layout fills the viewport horizontally.
  * **Illustration**:

    ```css
    html, body {
      /* No width explicitly defined, but both take up full viewport width */
    }
    
    div {
      width: 100%; /* Works because it inherits from the full-width <body> */
    }
    ```


---

### **Summary of Key Differences**

| Property | Behavior for `<html>` and `<body>` | Why It Works/Fails |
|----|----|----|
| `width: 100%` | Works by default | `<html>` and `<body>` naturally stretch to viewport width. |
| `height: 100%` | Requires explicit height on parent | Without a defined parent height, height collapses to content size. |
| `100vh` | Works independently of parent size | Directly references the viewport, bypassing parent dependency. |


---

# Are `* {}` and `body {}` the same in CSS, or do they have different purposes?

Good question! Let’s break it down and clarify why `* {}` and `body {}` are used differently 


---

### Does `body {}` Apply Universally?

No, `body {}` **only applies to the** `<body>` element itself, not to all elements on the page. Any margin, padding, or other properties applied to `body` affect the body **alone**, not its child elements. For example:

```css
body {
  margin: 50px;
}
```

This will apply a **50px margin to the** `<body>`, but **not to any child elements** like `<p>`, `<div>`, `<img>`, etc.


---

### Does `* {}` Apply Universally?

Yes, `* {}` (the universal selector) applies styles to **all elements** on the page, including `<body>`, `<html>`, and every child element. For example:

```css
* {
  margin: 10px;
}
```

This will apply a **10px margin to every element**: `<body>`, `<p>`, `<h1>`, `<div>`, etc. It's like a blanket rule for the whole document.


---

### TL;DR

* `* {}` applies globally to all elements, while `body {}` only applies to the body.
* Use `* {}` for global resets or defaults, and `body {}` for specific styling of the body.


---

# Why margin: 0 auto; is used in containers ?

Breaking it Down:


1. `margin: 0 auto;`
   * `0`: Sets the top and bottom margins to `0`.
   * `auto`: Sets the left and right margins to automatically adjust, centering the element horizontally within its parent container.


---

### Key Points:

* For `margin: 0 auto;` to work:

  
  1. The element must be **block-level** (like `<div>`, `<section>`) or have `display: block` set.
  2. The element must have a defined **width** (e.g., `width: 50%` or `width: 400px`). If the width isn’t set, the element will naturally take up the full width of its parent, leaving no space to "center."


---

### Why Use `auto`?

* The `auto` value tells the browser to equally distribute any remaining horizontal space on both the left and right sides of the element, which creates the centering effect.


---

### Vertical Centering?

* `margin: 0 auto;` **only centers elements horizontally.**
* For vertical centering, other techniques like `flexbox` or `grid` are usually needed.


