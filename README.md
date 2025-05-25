# CSS Basics - Complete Guide

A comprehensive guide to CSS fundamentals for beginners and intermediate developers.

## Table of Contents

1. [Introduction](#introduction)
2. [CSS Syntax and Selectors](#css-syntax-and-selectors)
3. [Box Model](#box-model)
4. [Typography](#typography)
5. [Colors and Backgrounds](#colors-and-backgrounds)
6. [Layout Fundamentals](#layout-fundamentals)
7. [Flexbox](#flexbox)
8. [CSS Grid](#css-grid)
9. [Positioning](#positioning)
10. [Responsive Design](#responsive-design)
11. [Animations and Transitions](#animations-and-transitions)

## Introduction

CSS (Cascading Style Sheets) is a stylesheet language used to describe the presentation of HTML documents. It controls the visual appearance, layout, and formatting of web pages.

### Key Concepts
- **Separation of Concerns**: HTML for structure, CSS for presentation
- **Cascading**: Styles can be inherited and overridden
- **Specificity**: Determines which styles take priority
- **Responsive Design**: Adapting layouts to different screen sizes

### Ways to Include CSS

```html
<!-- External CSS (Recommended) -->
<link rel="stylesheet" href="styles.css">

<!-- Internal CSS -->
<style>
  body { background-color: #f0f0f0; }
</style>

<!-- Inline CSS (Use sparingly) -->
<p style="color: red; font-size: 16px;">Styled paragraph</p>
```

## CSS Syntax and Selectors

### Basic Syntax

```css
selector {
  property: value;
  another-property: another-value;
}
```

### Element Selectors

```css
/* Type selectors */
h1 { color: blue; }
p { margin: 10px; }
div { background-color: white; }

/* Universal selector */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

### Class and ID Selectors

```css
/* Class selector */
.highlight {
  background-color: yellow;
  padding: 5px;
}

.btn {
  display: inline-block;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* ID selector */
#header {
  background-color: #333;
  color: white;
  height: 80px;
}

#navigation {
  position: fixed;
  top: 0;
  width: 100%;
}
```

### Attribute Selectors

```css
/* Exact attribute value */
input[type="text"] {
  border: 1px solid #ccc;
  padding: 8px;
}

/* Attribute contains value */
a[href*="example"] {
  color: green;
}

/* Attribute starts with value */
a[href^="https"] {
  text-decoration: none;
}

/* Attribute ends with value */
img[src$=".jpg"] {
  border: 2px solid #000;
}

/* Attribute contains word */
div[class~="featured"] {
  background-color: #fffacd;
}
```

### Pseudo-classes and Pseudo-elements

```css
/* Pseudo-classes */
a:hover {
  color: red;
  text-decoration: underline;
}

a:visited {
  color: purple;
}

input:focus {
  outline: 2px solid blue;
  border-color: blue;
}

li:first-child {
  font-weight: bold;
}

li:last-child {
  border-bottom: none;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:nth-child(odd) {
  background-color: white;
}

/* Pseudo-elements */
p::first-line {
  font-weight: bold;
  color: #333;
}

p::first-letter {
  font-size: 2em;
  float: left;
  margin-right: 5px;
}

.quote::before {
  content: """;
  font-size: 2em;
  color: #ccc;
}

.quote::after {
  content: """;
  font-size: 2em;
  color: #ccc;
}
```

### Combinators

```css
/* Descendant combinator (space) */
article p {
  line-height: 1.6;
}

/* Child combinator (>) */
nav > ul {
  list-style: none;
}

/* Adjacent sibling combinator (+) */
h2 + p {
  margin-top: 0;
  font-weight: bold;
}

/* General sibling combinator (~) */
h2 ~ p {
  color: #666;
}
```

### Selector Specificity

```css
/* Specificity calculation: (inline, IDs, classes, elements) */

/* (0, 0, 0, 1) - Specificity: 1 */
p { color: black; }

/* (0, 0, 1, 1) - Specificity: 11 */
p.intro { color: blue; }

/* (0, 1, 0, 1) - Specificity: 101 */
#main p { color: red; }

/* (0, 1, 1, 1) - Specificity: 111 */
#main p.intro { color: green; }

/* (1, 0, 0, 0) - Specificity: 1000 */
/* style="color: purple;" */
```

## Box Model

### Understanding the Box Model

```css
.box {
  /* Content area */
  width: 200px;
  height: 100px;
  
  /* Padding (inside the element) */
  padding: 20px;
  padding-top: 10px;
  padding-right: 15px;
  padding-bottom: 10px;
  padding-left: 15px;
  /* Shorthand: padding: top right bottom left; */
  
  /* Border */
  border: 2px solid #333;
  border-width: 2px;
  border-style: solid;
  border-color: #333;
  
  /* Margin (outside the element) */
  margin: 20px;
  margin-top: 10px;
  margin-right: auto; /* Center horizontally */
  margin-bottom: 10px;
  margin-left: auto;
}
```

### Box-sizing Property

```css
/* Default box-sizing: content-box */
.default-box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* Total width: 200px + 40px + 10px = 250px */
}

/* Border-box includes padding and border in width */
.border-box {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  /* Total width: 200px */
}

/* Apply to all elements (recommended) */
*, *::before, *::after {
  box-sizing: border-box;
}
```

### Display Property

```css
/* Block elements */
.block {
  display: block;
  width: 100%;
  margin: 10px 0;
}

/* Inline elements */
.inline {
  display: inline;
  /* Width and height have no effect */
  /* Top/bottom margins have no effect */
}

/* Inline-block elements */
.inline-block {
  display: inline-block;
  width: 200px;
  height: 100px;
  vertical-align: top;
}

/* Hide elements */
.hidden {
  display: none; /* Removes from document flow */
}

.invisible {
  visibility: hidden; /* Keeps space, but invisible */
}
```

## Typography

### Font Properties

```css
.typography-example {
  /* Font family with fallbacks */
  font-family: "Helvetica Neue", Arial, sans-serif;
  
  /* Font size */
  font-size: 16px; /* Absolute */
  font-size: 1.2em; /* Relative to parent */
  font-size: 1.2rem; /* Relative to root */
  
  /* Font weight */
  font-weight: normal; /* 400 */
  font-weight: bold; /* 700 */
  font-weight: 300; /* Light */
  font-weight: 600; /* Semi-bold */
  
  /* Font style */
  font-style: normal;
  font-style: italic;
  font-style: oblique;
  
  /* Line height */
  line-height: 1.5; /* Unitless (recommended) */
  line-height: 24px; /* Fixed */
  line-height: 150%; /* Percentage */
  
  /* Letter spacing */
  letter-spacing: 0.1em;
  letter-spacing: 2px;
  
  /* Word spacing */
  word-spacing: 0.2em;
}
```

### Text Properties

```css
.text-styling {
  /* Text alignment */
  text-align: left;
  text-align: center;
  text-align: right;
  text-align: justify;
  
  /* Text decoration */
  text-decoration: none;
  text-decoration: underline;
  text-decoration: line-through;
  text-decoration: overline;
  
  /* Text transform */
  text-transform: none;
  text-transform: uppercase;
  text-transform: lowercase;
  text-transform: capitalize;
  
  /* Text indent */
  text-indent: 2em;
  
  /* White space handling */
  white-space: normal;
  white-space: nowrap;
  white-space: pre;
  white-space: pre-wrap;
  
  /* Text overflow */
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}
```

### Web Fonts

```css
/* Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

/* Custom font loading */
@font-face {
  font-family: 'CustomFont';
  src: url('fonts/customfont.woff2') format('woff2'),
       url('fonts/customfont.woff') format('woff');
  font-weight: normal;
  font-style: normal;
  font-display: swap; /* Improves loading performance */
}

.custom-text {
  font-family: 'CustomFont', Arial, sans-serif;
}
```

## Colors and Backgrounds

### Color Values

```css
.color-examples {
  /* Named colors */
  color: red;
  color: darkblue;
  color: transparent;
  
  /* Hexadecimal */
  color: #ff0000; /* Red */
  color: #00f; /* Blue (shorthand) */
  color: #ff000080; /* Red with 50% opacity (8-digit hex) */
  
  /* RGB */
  color: rgb(255, 0, 0); /* Red */
  color: rgba(255, 0, 0, 0.5); /* Red with 50% opacity */
  
  /* HSL */
  color: hsl(0, 100%, 50%); /* Red */
  color: hsla(0, 100%, 50%, 0.5); /* Red with 50% opacity */
  
  /* CSS custom properties (variables) */
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  color: var(--primary-color);
}
```

### Background Properties

```css
.background-examples {
  /* Background color */
  background-color: #f0f0f0;
  
  /* Background image */
  background-image: url('image.jpg');
  background-image: linear-gradient(45deg, #ff6b6b, #4ecdc4);
  background-image: radial-gradient(circle, #ff6b6b, #4ecdc4);
  
  /* Background repeat */
  background-repeat: no-repeat;
  background-repeat: repeat-x;
  background-repeat: repeat-y;
  
  /* Background position */
  background-position: center;
  background-position: top left;
  background-position: 50% 75%;
  background-position: 10px 20px;
  
  /* Background size */
  background-size: cover; /* Scale to cover entire container */
  background-size: contain; /* Scale to fit within container */
  background-size: 100% 50%; /* Specific dimensions */
  
  /* Background attachment */
  background-attachment: fixed; /* Fixed during scroll */
  background-attachment: scroll; /* Scrolls with content */
  
  /* Background shorthand */
  background: #f0f0f0 url('image.jpg') no-repeat center/cover;
}
```

### Gradients

```css
.gradient-examples {
  /* Linear gradients */
  background: linear-gradient(to right, #ff6b6b, #4ecdc4);
  background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1);
  background: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.7));
  
  /* Radial gradients */
  background: radial-gradient(circle, #ff6b6b, #4ecdc4);
  background: radial-gradient(ellipse at top left, #ff6b6b, #4ecdc4);
  
  /* Conic gradients */
  background: conic-gradient(#ff6b6b, #4ecdc4, #45b7d1, #ff6b6b);
  
  /* Multiple backgrounds */
  background: 
    linear-gradient(45deg, transparent 30%, rgba(255,255,255,0.1) 30%),
    linear-gradient(-45deg, transparent 30%, rgba(255,255,255,0.1) 30%),
    #3498db;
}
```

## Layout Fundamentals

### Normal Flow

```css
/* Block elements stack vertically */
.block-element {
  display: block;
  width: 100%;
  margin-bottom: 20px;
}

/* Inline elements flow horizontally */
.inline-element {
  display: inline;
  margin: 0 5px;
}

/* Inline-block combines both behaviors */
.inline-block-element {
  display: inline-block;
  width: 200px;
  height: 100px;
  margin: 10px;
  vertical-align: top;
}
```

### Float Layout (Legacy)

```css
.float-container {
  overflow: hidden; /* Clearfix */
}

.float-left {
  float: left;
  width: 30%;
  margin-right: 3%;
}

.float-right {
  float: right;
  width: 67%;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

## Flexbox

### Flex Container Properties

```css
.flex-container {
  display: flex;
  
  /* Flex direction */
  flex-direction: row; /* Default */
  flex-direction: column;
  flex-direction: row-reverse;
  flex-direction: column-reverse;
  
  /* Flex wrap */
  flex-wrap: nowrap; /* Default */
  flex-wrap: wrap;
  flex-wrap: wrap-reverse;
  
  /* Shorthand for direction and wrap */
  flex-flow: row wrap;
  
  /* Justify content (main axis) */
  justify-content: flex-start; /* Default */
  justify-content: flex-end;
  justify-content: center;
  justify-content: space-between;
  justify-content: space-around;
  justify-content: space-evenly;
  
  /* Align items (cross axis) */
  align-items: stretch; /* Default */
  align-items: flex-start;
  align-items: flex-end;
  align-items: center;
  align-items: baseline;
  
  /* Align content (multi-line) */
  align-content: stretch;
  align-content: flex-start;
  align-content: flex-end;
  align-content: center;
  align-content: space-between;
  align-content: space-around;
  
  /* Gap between items */
  gap: 20px;
  row-gap: 20px;
  column-gap: 15px;
}
```

### Flex Item Properties

```css
.flex-item {
  /* Flex grow */
  flex-grow: 0; /* Default - don't grow */
  flex-grow: 1; /* Grow to fill available space */
  flex-grow: 2; /* Grow twice as much as items with flex-grow: 1 */
  
  /* Flex shrink */
  flex-shrink: 1; /* Default - can shrink */
  flex-shrink: 0; /* Don't shrink */
  
  /* Flex basis (initial size) */
  flex-basis: auto; /* Default */
  flex-basis: 200px; /* Fixed width */
  flex-basis: 0; /* Take minimum content width */
  
  /* Shorthand */
  flex: 1; /* flex: 1 1 0% */
  flex: 0 0 200px; /* Don't grow/shrink, 200px width */
  flex: auto; /* flex: 1 1 auto */
  
  /* Align individual item */
  align-self: auto; /* Default */
  align-self: flex-start;
  align-self: flex-end;
  align-self: center;
  align-self: stretch;
  
  /* Order */
  order: 0; /* Default */
  order: 1; /* Appears after order 0 items */
  order: -1; /* Appears before order 0 items */
}
```

### Flexbox Examples

```css
/* Navigation bar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}

/* Card layout */
.card-container {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
}

.card {
  flex: 0 0 300px;
  max-width: 400px;
}

/* Centering content */
.center-content {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

/* Responsive sidebar */
.layout {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  flex: 0 0 250px;
}

.main-content {
  flex: 1;
  padding: 2rem;
}

@media (max-width: 768px) {
  .layout {
    flex-direction: column;
  }
  
  .sidebar {
    flex: none;
  }
}
```

## CSS Grid

### Grid Container Properties

```css
.grid-container {
  display: grid;
  
  /* Define columns */
  grid-template-columns: 200px 200px 200px;
  grid-template-columns: 1fr 1fr 1fr; /* Equal fractions */
  grid-template-columns: 1fr 2fr 1fr; /* Proportional */
  grid-template-columns: repeat(3, 1fr); /* Repeat pattern */
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); /* Responsive */
  
  /* Define rows */
  grid-template-rows: 100px 200px auto;
  grid-template-rows: repeat(3, 1fr);
  
  /* Named grid lines */
  grid-template-columns: [start] 1fr [middle] 1fr [end];
  grid-template-rows: [header-start] 100px [header-end main-start] 1fr [main-end];
  
  /* Grid areas */
  grid-template-areas: 
    "header header header"
    "sidebar main main"
    "footer footer footer";
  
  /* Gap between grid items */
  gap: 20px;
  row-gap: 20px;
  column-gap: 15px;
  
  /* Alignment */
  justify-items: stretch; /* Horizontal alignment of items */
  align-items: stretch; /* Vertical alignment of items */
  justify-content: start; /* Horizontal alignment of grid */
  align-content: start; /* Vertical alignment of grid */
  
  /* Shorthand */
  place-items: center; /* align-items and justify-items */
  place-content: center; /* align-content and justify-content */
  
  /* Implicit grid */
  grid-auto-columns: 1fr;
  grid-auto-rows: 100px;
  grid-auto-flow: row; /* or column, row dense, column dense */
}
```

### Grid Item Properties

```css
.grid-item {
  /* Position using line numbers */
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 4;
  
  /* Shorthand */
  grid-column: 1 / 3; /* Start / End */
  grid-row: 2 / 4;
  grid-area: 2 / 1 / 4 / 3; /* row-start / col-start / row-end / col-end */
  
  /* Span syntax */
  grid-column: span 2; /* Span 2 columns */
  grid-row: span 3; /* Span 3 rows */
  grid-column: 2 / span 2; /* Start at line 2, span 2 columns */
  
  /* Using named lines */
  grid-column: start / end;
  grid-row: header-start / main-end;
  
  /* Using named areas */
  grid-area: header;
  grid-area: sidebar;
  grid-area: main;
  
  /* Item alignment */
  justify-self: start; /* Horizontal alignment */
  align-self: center; /* Vertical alignment */
  place-self: center; /* Both alignments */
}
```

### Grid Examples

```css
/* Basic layout */
.page-layout {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main main"
    "footer footer footer";
  grid-template-rows: auto 1fr auto;
  grid-template-columns: 250px 1fr;
  min-height: 100vh;
  gap: 1rem;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }

/* Responsive card grid */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  padding: 2rem;
}

/* Complex layout */
.magazine-layout {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: repeat(10, 50px);
  gap: 1rem;
}

.article-main {
  grid-column: 1 / 8;
  grid-row: 1 / 7;
}

.article-sidebar {
  grid-column: 8 / 13;
  grid-row: 1 / 4;
}

.article-featured {
  grid-column: 8 / 13;
  grid-row: 4 / 7;
}
```

## Positioning

### Static and Relative Positioning

```css
/* Static positioning (default) */
.static-element {
  position: static; /* Cannot be moved with top, right, bottom, left */
}

/* Relative positioning */
.relative-element {
  position: relative;
  top: 10px; /* Move 10px down from normal position */
  left: 20px; /* Move 20px right from normal position */
  /* Original space is preserved */
}
```

### Absolute and Fixed Positioning

```css
/* Absolute positioning */
.absolute-element {
  position: absolute;
  top: 50px; /* 50px from top of nearest positioned ancestor */
  right: 20px; /* 20px from right edge */
  /* Removed from normal document flow */
}

/* Fixed positioning */
.fixed-element {
  position: fixed;
  top: 0; /* Fixed to top of viewport */
  left: 0;
  width: 100%;
  z-index: 1000; /* Ensure it's on top */
  /* Stays in place during scrolling */
}

/* Sticky positioning */
.sticky-element {
  position: sticky;
  top: 20px; /* Sticks when 20px from top during scroll */
  /* Behaves like relative until scroll threshold */
}
```

### Z-Index and Stacking Context

```css
.stacking-context {
  position: relative;
  z-index: 1; /* Creates new stacking context */
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 10;
}

.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 1000;
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}
```

## Responsive Design

### Media Queries

```css
/* Mobile-first approach */
.container {
  width: 100%;
  padding: 1rem;
}

/* Tablet styles */
@media screen and (min-width: 768px) {
  .container {
    max-width: 750px;
    margin: 0 auto;
    padding: 2rem;
  }
}

/* Desktop styles */
@media screen and (min-width: 1024px) {
  .container {
    max-width: 1200px;
  }
}

/* Large desktop styles */
@media screen and (min-width: 1200px) {
  .container {
    max-width: 1400px;
  }
}

/* Media query features */
@media screen and (max-width: 600px) {
  /* Styles for screens smaller than 600px */
}

@media print {
  /* Print styles */
  .no-print { display: none; }
}

@media (orientation: landscape) {
  /* Landscape orientation */
}

@media (prefers-color-scheme: dark) {
  /* Dark mode styles */
  body {
    background-color: #1a1a1a;
    color: #ffffff;
  }
}

@media (prefers-reduced-motion: reduce) {
  /* Reduce animations for accessibility */
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

### Responsive Units

```css
.responsive-units {
  /* Viewport units */
  width: 100vw; /* 100% of viewport width */
  height: 100vh; /* 100% of viewport height */
  font-size: 4vw; /* 4% of viewport width */
  padding: 2vh 2vw; /* Responsive padding */
  
  /* Minimum and maximum viewport units */
  font-size: clamp(1rem, 4vw, 3rem); /* Min 1rem, prefer 4vw, max 3rem */
  
  /* Relative units */
  font-size: 1.2em; /* Relative to parent font size */
  padding: 2rem; /* Relative to root font size */
  
  /* Percentage */
  width: 50%; /* 50% of parent width */
  height: 75%; /* 75% of parent height */
}
```

### Flexible Images and Media

```css
/* Responsive images */
img {
  max-width: 100%;
  height: auto;
}

/* Picture element with different sources */
.responsive-image {
  width: 100%;
  height: auto;
  object-fit: cover; /* or contain, fill, scale-down */
  object-position: center;
}

/* Responsive video */
.video-container {
  position: relative;
  width: 100%;
  padding-bottom: 56.25%; /* 16:9 aspect ratio */
  height: 0;
}

.video-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

/* Responsive typography */
.responsive-text {
  font-size: clamp(1rem, 2.5vw, 2rem);
  line-height: 1.5;
}
```

## Animations and Transitions

### CSS Transitions

```css
.transition-element {
  background-color: blue;
  padding: 1rem;
  border-radius: 4px;
  
  /* Transition properties */
  transition-property: background-color, transform, opacity;
  transition-duration: 0.3s, 0.5s, 0.2s;
  transition-timing-function: ease, ease-in-out, linear;
  transition-delay: 0s, 0.1s, 0.2s;
  
  /* Shorthand */
  transition: all 0.3s ease-in-out;
}

.transition-element:hover {
  background-color: red;
  transform: scale(1.1);
  opacity: 0.8;
}

/* Common transition patterns */
.button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: #2980b9;
}

.fade-in {
  opacity: 0;
  transition: opacity 0.5s ease-in;
}

.fade-in.visible {
  opacity: 1;
}
```

### CSS Animations

```css
/* Define keyframes */
@keyframes slideIn {
  0% {
    transform: translateX(-100%);
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}

@keyframes bounce {
  0%, 20%, 53%, 80%, 100% {
    animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
    transform: translate3d(0,0,0);
  }
  40%, 43% {
    animation-timing-function: cubic-bezier(0.755, 0.050, 0.855, 0.060);
    transform: translate3d(0, -30px, 0);
  }
  70% {
    animation-timing
