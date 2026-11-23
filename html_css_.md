# HTML and CSS Basics


- HTML means HyperText Markup Language; it gives structure to a web page.
- CSS means Cascading Style Sheets; it gives style (colour, size, layout) to that structure.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My Page</title>
</head>
<body>
  <h1>Hello</h1>
</body>
</html>
```

- **`<!DOCTYPE html>`** = tells the browser this is an HTML5 page
- **`<head>`** = information about the page 
- **`<body>`** = everything shown on the page

---

## Semantic HTML Tags ##
- Semantic tags are tags whose name tells what the content is, like header,footer,main,sidebar.
- These tags can help screen readers, search engines and make code easier to read.

### Page structure tags ###
- `<header>` : top part of a page or section (logo, title).
- `<nav>` : a group of navigation links.
- `<main>` : the main content of the page (use only once).
- `<section>` : a group of related content, usually with a heading.
- `<article>` : content that makes sense on its own (blog post, news story).
- `<aside>` : side content related to the main content (sidebar).
- `<footer>` : bottom part of a page or section (copyright, links).


```html
<body>
  <header>...</header>
  <nav>...</nav>
  <main>
    <article>...</article>
    <aside>...</aside>
  </main>
  <footer>...</footer>
</body>
```

---

## Box Model ##
- Every HTML element is a rectangular box made of 4 layers (inside to outside):
  - `content` : the text or image itself.
  - `padding` : space between the content and the border.
  - `border` : a line around the padding.
  - `margin` : space outside the border, between this box and other boxes.

```css
.box {
  width: 200px;
  padding: 20px;
  border: 2px solid black;
  margin: 10px;
}
```
- box-sizing: content-box : the default; width counts only the content.
- box-sizing: border-box : width includes padding and border (box stays 200px wide).
- margin: 10px 20px : 10px top and bottom, 20px left and right.

---

## Inline vs Block Elements ##
| Type | Starts on new line | Width | Examples |
|---|---|---|---|
| Block | Yes | Takes the full width | `div`, `p`, `h1`, `ul`, `section` |
| Inline | No | Only as wide as its content | `span`, `a`, `strong`, `img` |
| Inline-block | No | Can set width and height | `button`, or `display: inline-block` |

- Block elements accept `width`, `height` and vertical margin.
- Inline elements ignore `width`, `height` and vertical margin.
- `display: block | inline | inline-block | none` : changes how an element behaves (`none` hides it completely).

```html
<p>This is <span>inline</span> text inside a block.</p>
```

---

## Positioning ##
- **static** : the default; the element follows the normal page flow.
- **relative** : stays in the flow, but can be moved from its normal place using `top`, `left`, `right`, `bottom`.
- **absolute**: removed from the flow and placed relative to the nearest parent that is not `static`.
- **position: fixed** : placed relative to the browser window; does not move when scrolling.
- **sticky** : scrolls normally, then sticks at a given position (like a header).
- **z-index** : decides which overlapping element is on top (bigger number = on top).


---

## Common CSS Structural Classes ##
- **Class names** : These are declared by developers
- **.container / `.wrapper** : centres the content and limits its maximum width.
- **.grid** : a grid layout wrapper.
- **.header, .sidebar, .footer** : the main regions of a page.
- **.card** : a boxed piece of content.
- **.hidden** : hides an element.



---

## Common CSS Styling Classes ##
| Class | Does | CSS used |
|---|---|---|
| `.text-center` | Centres the text | `text-align: center` |
| `.bold` | Makes text bold | `font-weight: bold` |
| `.bg-primary` | Sets background colour | `background-color: blue` |
| `.rounded` | Rounds the corners | `border-radius: 8px` |
| `.shadow` | Adds a shadow | `box-shadow: 0 2px 5px gray` |
| `.btn` | Styles a button | `padding`, `color`, `border` |

- `:hover` : styles an element when the mouse is over it.
- `:focus` : styles an element when it is selected (like an input).

---

## CSS Specificity ##
- Specificity decides which CSS rule wins when many rules target the same element.
- From weakest to strongest:
  1. Element selector : `p`
  2. Class selector : `.classname`
  3. ID selector : `#idname`
  4. Inline style : `style="..."`
- If two rules have the same specificity, the one written **last** wins.
- **!important**:Overrides everything

---

## CSS Responsive Queries ##
- A media query applies CSS only when a condition is true (like the screen width).
- Mobile-first = write styles for small screens first, then use min-width for bigger screens.

```css
@media (min-width: 768px) {
  .menu { display: flex; }
}
```
- **min-width** : applies from this width and bigger.
- **max-width** : applies up to this width and smaller.
- **orientation: landscape**: applies when the screen is wider than tall.
- **prefers-color-scheme: dark** : applies when the user uses dark mode.
- **@media print** : applies only when printing.

---

## Flexbox and Grid ##

### Flexbox ###
- Flexbox is a layout in one direction (a row or a column); for declaring this use `display: flex`.
- `flex-direction` : row or column.
- `justify-content` : aligns items along the main direction (`center`, `space-between`).
- `align-items` : aligns items in the other direction (`center`, `stretch`).
- `flex-wrap` : lets items move to the next line.
- `gap` : space between items.

```css
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

### Grid ###
- Grid is a layout in two directions (rows and columns); turn it on with `display: grid`.
- `grid-template-columns` : defines the columns (`1fr 2fr` = one part and two parts).
- `grid-template-rows` : defines the rows.
- `gap` : space between rows and columns.
- `fr` : a fraction of the free space.

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```
- Use Flexbox for one line of items, and Grid for full page layouts.

---

## Common Header Meta Tags ##
- Meta tags live inside `<head>` and give information about the page; they are not shown.
- `<meta charset="UTF-8">` : sets the character encoding so all text shows correctly.
- `<meta name="viewport" content="width=device-width, initial-scale=1">` : makes the page fit phone screens.
- `<title>` : the page title shown in the browser tab.
- `<meta name="description" content="...">` : short summary shown by search engines.
- `<meta name="robots" content="noindex">` : tells search engines not to list the page.
- `<link rel="stylesheet" href="style.css">` : connects an external CSS file.
- `<meta property="og:title" content="...">` : title shown when the link is shared on social media.

---

### CSS units ###
- `px` : fixed size in pixels.
- `%` : percentage of the parent.
- `em` : relative to the parent font size.
- `rem` : relative to the root (page) font size.
- `vw` / `vh` : 1% of the screen width / height.

### CSS variable

- CSS variable : a reusable value, declared as `--main: blue;` and used as `var(--main)`.
- `float` : an old way to wrap text around an element; Flexbox and Grid replaced it for layouts.
- `alt` : the attribute on `<img>` that describes the image for screen readers.
- `overflow` : decides what happens when content is bigger than its box (`hidden`, `scroll`, `auto`).

### Margin sides ###
- **margin-top** : space above the element.
- **margin-right** : space to the right of the element.
- **margin-bottom** : space below the element.
- **margin-left** : space to the left of the element.
- **margin** : shorthand for all four sides.

- The shorthand order is clockwise: top, right, bottom, left.
- `margin: 10px` : all four sides are 10px.
- `margin: 10px 20px` : 10px top and bottom, 20px left and right.
- `margin: 10px 20px 30px 40px` : top 10px, right 20px, bottom 30px, left 40px.
- `margin-left: auto` : pushes the element to the right; `margin-right: auto` pushes it to the left.
- `margin: 0 auto` : centres a block element horizontally (it needs a set `width`).
