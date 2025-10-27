# CSS Cheatsheet — quick, practical, and copy-paste ready

---

# Basics & syntax

```css
/* selector { property: value; } */
body { font-family: system-ui, -apple-system, "Segoe UI", Roboto, sans-serif; }
```

* Selectors: element (`p`), class (`.btn`), id (`#nav`), attribute (`a[href$=".pdf"]`), descendant (`.card p`), child (`ul > li`), adjacent (`h1 + p`), general sibling (`h1 ~ p`).
* Grouping: `h1,h2,h3 { margin:0 }`
* Comment: `/* like this */`

---

# Box model

* Content → padding → border → margin.
* `box-sizing: border-box;` preferred (includes padding & border in width/height).

```css
* { box-sizing: border-box; }
.container { width: 900px; padding: 24px; border: 1px solid #ddd; }
```

---

# Display & visibility

* `display: block | inline | inline-block | none | flex | grid | contents`
* `visibility: visible | hidden` (hidden reserves space)
* `opacity: 0–1` (affects stacking & events)

```css
.hidden { display:none; }
.inlineBlock { display:inline-block; vertical-align:middle; }
```

---

# Positioning

* `position: static | relative | absolute | fixed | sticky`
* `top/right/bottom/left` used when not static.
* `z-index` affects stacking context (only works on positioned elements or flex/grid children in some cases).

```css
.header { position: sticky; top: 0; background: white; z-index: 50; }
.modal { position: fixed; inset: 0; display:flex; align-items:center; justify-content:center; }
```

---

# Flexbox (one-dimensional)

* Container: `display:flex; flex-direction: row|column; gap: 12px;`
* Alignment: `justify-content`, `align-items`, `align-content`
* Child sizing: `flex: 1 1 auto;` shorthand for `flex-grow flex-shrink flex-basis`

```css
.row { display:flex; gap:12px; align-items:center; justify-content:space-between; }
.col { display:flex; flex-direction:column; gap:8px; }
.item { flex:1; } /* equal flexible items */
```

Common values:

* `justify-content: flex-start | center | flex-end | space-between | space-around | space-evenly`
* `align-items: flex-start | center | flex-end | stretch | baseline`

---

# Grid (two-dimensional)

* Container: `display:grid; grid-template-columns: repeat(3, 1fr); gap: 16px;`
* Named areas / auto-placement / minmax / fit-content

```css
.grid { display:grid; grid-template-columns: 200px 1fr 1fr; gap:16px; }
.grid2 { grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); }
.itemA { grid-column: 1 / -1; } /* spans full width */
```

---

# Sizing & units

* Absolute: `px`
* Relative: `em` (to font-size of parent), `rem` (to root font-size), `%` (to container)
* Responsive: `vw`, `vh`, `vmin`, `vmax`
* Fluid sizing: `clamp(min, preferred, max)` e.g. `font-size: clamp(1rem, 2vw + 0.5rem, 1.5rem);`

---

# Typography

* `font-family`, `font-size`, `line-height`, `font-weight`, `letter-spacing`, `text-transform`, `text-decoration`, `text-align`
* Readability: `line-height: 1.4–1.6` for body text.

```css
h1 { font-size: 2rem; line-height: 1.1; font-weight:700; }
p { font-size: 1rem; line-height: 1.6; }
```

---

# Colors

* Hex: `#RRGGBB` / `#RGB` / `#RRGGBBAA`
* RGB / RGBA: `rgb(255,0,0)` / `rgba(255,0,0,0.5)`
* HSL: `hsl(210 50% 40%)` and `hsl(210 50% 40% / 0.6)`
* Use CSS variables for theme colors

```css
:root {
  --brand: #0066cc;
  --muted: hsl(210 20% 90%);
}
.btn { background: var(--brand); color: white; }
```

---

# Backgrounds & borders

* `background-color`, `background-image`, `background-size`, `background-position`, `background-repeat`
* `border: 1px solid #ccc; border-radius: 8px;`
* `outline` vs `border` (outline doesn't affect layout)

```css
.card { background: linear-gradient(180deg, #fff, #f7f9ff); border-radius: 12px; padding:16px; }
```

---

# Pseudo-classes & pseudo-elements

* Pseudo-classes: `:hover`, `:focus`, `:active`, `:visited`, `:first-child`, `:nth-child(n)`, `:not()`
* Pseudo-elements: `::before`, `::after`, `::first-letter`, `::selection`

```css
a:hover { text-decoration: underline; }
.button::after { content:""; display:block; height:2px; background:var(--brand); }
```

---

# Forms & inputs

* reset default styles: `appearance: none; border: none;`
* focus visible: `:focus { outline: 2px solid #abc; }`
* placeholder: `::placeholder { color: #999; }`

```css
input { padding:8px 12px; border:1px solid #ddd; border-radius:6px; }
input:focus { border-color: var(--brand); box-shadow: 0 0 0 4px rgba(0,102,204,0.08); }
```

---

# Transitions & animations

* Transitions: `transition: property duration timing-function delay;`
* Keyframes: `@keyframes name { from { } to { } }`

```css
.btn { transition: transform .18s ease, box-shadow .18s ease; }
.btn:hover { transform: translateY(-2px); }
@keyframes pop { 0% { transform: scale(.95); } 60% { transform: scale(1.03); } 100% { transform: scale(1); } }
```

---

# CSS Variables (Custom properties)

* Define: `:root { --space: 16px; }`
* Use: `padding: var(--space);`
* Cascadeable and themeable; support fallback: `var(--x, 1rem)`

---

# Media queries & responsive

```css
/* mobile-first */
.container { padding: 16px; }
@media (min-width: 768px) {
  .container { padding: 32px; }
}
```

Common breakpoints (example):

* 480px — small phones
* 640px — larger phones
* 768px — tablets (portrait)
* 1024px — tablets (landscape) / small laptops
* 1280px — desktops

Also `@media (prefers-reduced-motion: reduce)` for accessibility.

---

# Specificity & cascade (short)

* Inline styles: highest (1000)
* IDs: 100
* Classes/attributes/pseudo-classes: 10
* Elements/pseudo-elements: 1
* Later rules override earlier if specificity equal.
* `!important` overrides but use sparingly.

---

# Useful shorthand properties

* Margin/padding: `margin: 8px 12px 8px 12px;` or `margin: 8px 12px;`
* Font: `font: italic small-caps 16px/1.4 "Inter", sans-serif;`
* Border: `border: 2px dashed #ccc;`
* Background: `background: url(img.jpg) center/cover no-repeat;`

---

# Accessibility quick tips

* Always keep focus states: `:focus-visible { outline: 3px solid ... }`
* Use sufficient color contrast (WCAG 4.5:1 for normal text — aim for 7:1 for headings)
* `prefers-reduced-motion` — disable nonessential animations
* `aria-*` attributes are set in HTML, but style focus/hover appropriately
* Use `:focus-visible` (not just :focus) to avoid styling mouse clicks

---

# Debugging tips

* `outline: 2px solid red;` temporarily show element boundaries
* Browser devtools: inspect computed styles + box model
* `display: none` to hide problematic elements
* `position: relative` + `z-index` to diagnose stacking issues

---

# Handy snippets

Centered container (both axes):

```css
.centered {
  display:flex;
  align-items:center;
  justify-content:center;
}
```

Horizontal scrollbar hide (but keep scroll):

```css
.hide-scrollbar {
  scrollbar-width: none; /* Firefox */
}
.hide-scrollbar::-webkit-scrollbar { display: none; } /* WebKit */
```

Fluid typography:

```css
h1 { font-size: clamp(1.5rem, 4vw, 3rem); }
```

Sticky footer layout:

```css
html,body { height:100%; }
.site { min-height:100%; display:flex; flex-direction:column; }
.main { flex:1; }
.footer { height:60px; }
```

---

# Common pitfalls

* Forgetting `box-sizing: border-box` → width surprises.
* Using fixed px everywhere → not responsive.
* Relying on `!important` instead of fixing specificity.
* Overusing `position:absolute` for layout — breaks flow.
* Not handling `prefers-reduced-motion`.

---

# Cheatsheet 1-liner references (copyable)

```css
/* Reset box model */
*{box-sizing:border-box;margin:0;padding:0;}
/* Flex row center */
.row{display:flex;align-items:center;justify-content:center;gap:12px;}
/* Grid auto-fit */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:16px;}
/* Button baseline */
.btn{display:inline-flex;align-items:center;gap:8px;padding:10px 14px;border-radius:8px;border:1px solid transparent;cursor:pointer;}
/* Accessible focus */
:focus-visible{outline:3px solid Highlight;outline-offset:2px;}
```
