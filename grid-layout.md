# **CSS Grid Layout — Step-by-Step Examples**

---

## **Example 1 — The Simplest Grid**

### Concept:

Turn a container into a grid and define columns.

```html
<!DOCTYPE html>
<html>
<head>
<style>
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px; /* 3 columns */
  gap: 10px;
  background-color: #f0f0f0;
  padding: 10px;
}
.item {
  background-color: lightblue;
  border: 2px solid #333;
  text-align: center;
  padding: 20px;
}
</style>
</head>
<body>
  <div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
  </div>
</body>
</html>
```

**Result:**
3 columns per row, 6 boxes total.
`gap: 10px` adds spacing between boxes.

---

## **Example 2 — Responsive Grid Using `fr` Units**

### Concept:

Use fractional units (`fr`) to make columns flexible.

```html
<style>
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  gap: 15px;
}
.item {
  background: lightgreen;
  text-align: center;
  padding: 20px;
  border: 2px solid darkgreen;
}
</style>

<div class="container">
  <div class="item">1fr</div>
  <div class="item">2fr (double width)</div>
  <div class="item">1fr</div>
</div>
```

**Result:**
Middle column takes **twice** as much space as the others — fully responsive.

---

## **Example 3 — Defining Rows**

### Concept:

Set specific heights for rows.

```html
<style>
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 100px 200px;
  gap: 10px;
}
.item {
  background: lightcoral;
  text-align: center;
  border: 2px solid #900;
}
</style>

<div class="container">
  <div class="item">A</div>
  <div class="item">B</div>
  <div class="item">C</div>
  <div class="item">D</div>
  <div class="item">E</div>
  <div class="item">F</div>
</div>
```

**Result:**
Two rows: first row 100px, second 200px.
Grid auto-fills cells row by row.

---

## **Example 4 — Positioning Items (Spanning Rows/Columns)**

### Concept:

Use `grid-column` and `grid-row` to make items span multiple cells.

```html
<style>
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
.item {
  background: lightseagreen;
  color: white;
  padding: 20px;
  text-align: center;
}
.item1 {
  grid-column: 1 / 3; /* spans 2 columns */
}
.item2 {
  grid-row: 2 / 4; /* spans 2 rows */
}
</style>

<div class="container">
  <div class="item item1">1 (span 2 columns)</div>
  <div class="item">2</div>
  <div class="item item2">3 (span 2 rows)</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
</div>
```

**Result:**
Item 1 stretches horizontally across two columns,
Item 3 stretches vertically across two rows.

---

## **Example 5 — Using Named Grid Areas**

### Concept:

Create a **page layout** (header, sidebar, main, footer) using **names**.

```html
<style>
.container {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
  grid-template-columns: 1fr 3fr;
  grid-template-rows: auto 1fr auto;
  gap: 10px;
  min-height: 100vh;
}

header  { grid-area: header; background: #a2d5f2; }
aside   { grid-area: sidebar; background: #f7d6bf; }
main    { grid-area: main; background: #c5e3bf; }
footer  { grid-area: footer; background: #ffb6b9; }

.container > * {
  padding: 20px;
  font-family: Arial, sans-serif;
  border-radius: 8px;
}
</style>

<div class="container">
  <header>Header</header>
  <aside>Sidebar</aside>
  <main>Main Content</main>
  <footer>Footer</footer>
</div>
```

**Result:**
Classic 2-column layout with a header and footer — fully grid-powered.

---

## **Example 6 — Responsive Grid Using `auto-fit` and `minmax()`**

### Concept:

Automatically adjust columns based on available space.

```html
<style>
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
}
.gallery div {
  background: lightpink;
  padding: 40px;
  border-radius: 10px;
  text-align: center;
  font-weight: bold;
}
</style>

<div class="gallery">
  <div>1</div><div>2</div><div>3</div>
  <div>4</div><div>5</div><div>6</div>
</div>
```

**Result:**

* On wide screens → 3 or 4 columns
* On small screens → 1 column
  No media queries required!

---

## **Example 7 — Aligning Items**

### Concept:

Control alignment of content inside grid cells.

```html
<style>
.container {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(2, 100px);
  justify-items: center; /* horizontal alignment */
  align-items: center;   /* vertical alignment */
  gap: 10px;
}
.item {
  background: steelblue;
  color: white;
  font-weight: bold;
  text-align: center;
  padding: 20px;
}
</style>

<div class="container">
  <div class="item">A</div>
  <div class="item">B</div>
  <div class="item">C</div>
  <div class="item">D</div>
  <div class="item">E</div>
  <div class="item">F</div>
</div>
```

**Result:**
All boxes centered neatly within their grid cells.

---

## **Example 8 — Full Page Responsive Layout**

### Concept:

Combine everything — areas, responsiveness, and grid alignment.

```html
<style>
.page {
  display: grid;
  grid-template-areas:
    "header header"
    "nav main"
    "footer footer";
  grid-template-columns: 1fr 3fr;
  grid-template-rows: auto 1fr auto;
  gap: 15px;
  min-height: 100vh;
  background: #f0f2f5;
}

header  { grid-area: header; background: #457b9d; color: white; }
nav     { grid-area: nav; background: #a8dadc; }
main    { grid-area: main; background: #f1faee; }
footer  { grid-area: footer; background: #1d3557; color: white; }

.page > * {
  padding: 20px;
  font-family: 'Poppins', sans-serif;
  border-radius: 10px;
}

/* Responsive for mobile */
@media (max-width: 768px) {
  .page {
    grid-template-areas:
      "header"
      "main"
      "nav"
      "footer";
    grid-template-columns: 1fr;
  }
}
</style>

<div class="page">
  <header>Header</header>
  <nav>Navigation</nav>
  <main>Main Content</main>
  <footer>Footer</footer>
</div>
```

**Result:**

* Desktop → 2-column layout
* Mobile → stacks vertically (header → main → nav → footer)

---

# **Key Takeaways**

1. `display: grid;` → activates grid mode.
2. `grid-template-columns` / `rows` → define structure.
3. `gap` → spacing between items.
4. `grid-column` / `grid-row` → control item placement.
5. `grid-template-areas` → name layout zones.
6. `auto-fit` + `minmax()` → build responsive grids without media queries.
7. `justify-items` / `align-items` → align inside grid cells.
8. Combine Grid for structure + Flexbox for inner content.
