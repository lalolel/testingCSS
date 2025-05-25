# Advanced CSS Techniques - Part 2

A comprehensive guide to advanced CSS features, techniques, and modern approaches for experienced developers looking to master the cutting edge of CSS.

## Table of Contents

1. [CSS Custom Properties (Variables)](#css-custom-properties-variables)
2. [Advanced Selectors & Pseudo-classes](#advanced-selectors--pseudo-classes)
3. [Advanced Pseudo-elements](#advanced-pseudo-elements)
4. [CSS Transforms & 3D Effects](#css-transforms--3d-effects)
5. [Advanced Layout Techniques](#advanced-layout-techniques)
6. [Advanced Color Techniques](#advanced-color-techniques)
7. [CSS Shapes & Clipping](#css-shapes--clipping)
8. [Container Queries](#container-queries)
9. [Advanced Animation Techniques](#advanced-animation-techniques)
10. [Modern CSS Features](#modern-css-features)
11. [CSS Preprocessors](#css-preprocessors)

---

## CSS Custom Properties (Variables)

Custom properties provide powerful theming and dynamic styling capabilities.

### Global Variables

```css
:root {
  /* Color system */
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
  --danger-color: #e74c3c;
  
  /* Typography scale */
  --font-size-base: 16px;
  --font-family-primary: 'Helvetica Neue', Arial, sans-serif;
  
  /* Spacing system */
  --space-xs: 0.25rem;
  --space-sm: 0.5rem;
  --space-md: 1rem;
  --space-lg: 2rem;
  --space-xl: 4rem;
  
  /* Layout */
  --max-width: 1200px;
  --border-radius: 8px;
  --box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  --transition-speed: 0.3s;
}
```

### Dynamic Variables with calc()

```css
.responsive-element {
  --scale-factor: 1;
  --base-size: 20px;
  font-size: calc(var(--base-size) * var(--scale-factor));
  margin: calc(var(--space-md) / 2);
  padding: calc(var(--space-sm) + 5px);
}

/* Context-aware spacing */
.card {
  --card-padding: var(--space-md);
  padding: var(--card-padding);
}

.card--large {
  --card-padding: var(--space-lg);
}
```

### Theme Switching

```css
[data-theme="dark"] {
  --bg-color: #1a1a1a;
  --text-color: #ffffff;
  --border-color: #444;
  --shadow-color: rgba(255, 255, 255, 0.1);
}

[data-theme="light"] {
  --bg-color: #ffffff;
  --text-color: #333333;
  --border-color: #ddd;
  --shadow-color: rgba(0, 0, 0, 0.1);
}

.themed-component {
  background-color: var(--bg-color);
  color: var(--text-color);
  border: 1px solid var(--border-color);
  box-shadow: 0 2px 10px var(--shadow-color);
  transition: all var(--transition-speed) ease;
}
```

---

## Advanced Selectors & Pseudo-classes

### Complex Structural Selectors

```css
/* Every 3rd element starting from the 2nd */
.grid-item:nth-child(3n+2) {
  background-color: var(--accent-color);
}

/* Last 3 items */
.menu-item:nth-last-child(-n+3) {
  border-bottom: none;
}

/* Elements with exactly 3 siblings */
.tab:first-child:nth-last-child(3),
.tab:first-child:nth-last-child(3) ~ .tab {
  width: 33.333%;
}

/* Only child with specific conditions */
.card:only-child {
  max-width: 100%;
  margin: 0 auto;
}
```

### Advanced Form Selectors

```css
/* Form validation states */
input:required {
  border-left: 3px solid var(--warning-color);
}

input:valid {
  border-left-color: var(--success-color);
}

input:invalid:not(:placeholder-shown) {
  border-left-color: var(--danger-color);
}

input:in-range {
  background-color: rgba(46, 204, 113, 0.1);
}

input:out-of-range {
  background-color: rgba(231, 76, 60, 0.1);
}

/* Interactive states */
input:read-only {
  background-color: var(--gray-100);
  cursor: not-allowed;
}

input:read-write:focus {
  outline: 2px solid var(--primary-color);
  outline-offset: 2px;
}
```

### Language and Direction Selectors

```css
:lang(en) { quotes: '"' '"' "'" "'"; }
:lang(fr) { quotes: "«" "»" "‹" "›"; }
:lang(de) { quotes: "„" """ "‚" "'"; }

:dir(ltr) { text-align: left; }
:dir(rtl) { text-align: right; }

/* Target-based styling */
.section:target {
  background-color: var(--highlight-bg);
  border-left: 4px solid var(--primary-color);
  animation: highlight 0.6s ease-in-out;
}
```

---

## Advanced Pseudo-elements

### Decorative Elements

```css
.decorative-heading {
  position: relative;
  text-align: center;
  margin: 2rem 0;
}

.decorative-heading::before,
.decorative-heading::after {
  content: '';
  position: absolute;
  top: 50%;
  width: 30%;
  height: 2px;
  background: linear-gradient(to right, transparent, var(--primary-color), transparent);
}

.decorative-heading::before { left: 0; }
.decorative-heading::after { right: 0; }
```

### Dynamic Tooltips

```css
.tooltip {
  position: relative;
  cursor: help;
}

.tooltip::before {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 125%;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.9);
  color: white;
  padding: 0.5rem 0.75rem;
  border-radius: 4px;
  font-size: 0.875rem;
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s, transform 0.3s;
  z-index: 1000;
}

.tooltip::after {
  content: '';
  position: absolute;
  bottom: 115%;
  left: 50%;
  transform: translateX(-50%);
  border: 5px solid transparent;
  border-top-color: rgba(0, 0, 0, 0.9);
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip:hover::before,
.tooltip:hover::after {
  opacity: 1;
}

.tooltip:hover::before {
  transform: translateX(-50%) translateY(-5px);
}
```

### Custom List Styling

```css
.custom-list {
  list-style: none;
  padding-left: 0;
}

.custom-list li {
  position: relative;
  padding-left: 2rem;
  margin-bottom: 0.75rem;
}

.custom-list li::before {
  content: counter(list-counter);
  counter-increment: list-counter;
  position: absolute;
  left: 0;
  top: 0;
  width: 1.5rem;
  height: 1.5rem;
  background: var(--primary-color);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.75rem;
  font-weight: bold;
}

.custom-list {
  counter-reset: list-counter;
}
```

---

## CSS Transforms & 3D Effects

### 3D Card Flip

```css
.flip-card {
  background-color: transparent;
  width: 300px;
  height: 200px;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
}

.flip-card-back {
  transform: rotateY(180deg);
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
}
```

### 3D Rotating Cube

```css
.cube-container {
  perspective: 1000px;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 400px;
}

.cube {
  position: relative;
  width: 200px;
  height: 200px;
  transform-style: preserve-3d;
  animation: rotateCube 10s infinite linear;
}

.cube-face {
  position: absolute;
  width: 200px;
  height: 200px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  font-weight: bold;
  color: white;
}

.cube-face.front   { background: #ff6b6b; transform: translateZ(100px); }
.cube-face.back    { background: #4ecdc4; transform: translateZ(-100px) rotateY(180deg); }
.cube-face.right   { background: #45b7d1; transform: rotateY(90deg) translateZ(100px); }
.cube-face.left    { background: #96ceb4; transform: rotateY(-90deg) translateZ(100px); }
.cube-face.top     { background: #feca57; transform: rotateX(90deg) translateZ(100px); }
.cube-face.bottom  { background: #ff9ff3; transform: rotateX(-90deg) translateZ(100px); }

@keyframes rotateCube {
  0% { transform: rotateX(0deg) rotateY(0deg); }
  100% { transform: rotateX(360deg) rotateY(360deg); }
}
```

---

## Advanced Layout Techniques

### CSS Grid Masonry Layout

```css
.masonry-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  grid-auto-rows: 20px;
  gap: 20px;
  padding: 20px;
}

.masonry-item {
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.masonry-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.masonry-item.small  { grid-row-end: span 8; }
.masonry-item.medium { grid-row-end: span 12; }
.masonry-item.large  { grid-row-end: span 16; }
.masonry-item.xl     { grid-row-end: span 20; }
```

### Holy Grail Layout

```css
.holy-grail {
  display: grid;
  grid-template: 
    "header header header" auto
    "nav main aside" 1fr
    "footer footer footer" auto
    / 250px 1fr 250px;
  min-height: 100vh;
  gap: 1rem;
  max-width: 1400px;
  margin: 0 auto;
}

.header { grid-area: header; background: var(--primary-color); }
.nav    { grid-area: nav; background: var(--gray-100); }
.main   { grid-area: main; background: white; }
.aside  { grid-area: aside; background: var(--gray-100); }
.footer { grid-area: footer; background: var(--gray-800); }

@media (max-width: 1024px) {
  .holy-grail {
    grid-template: 
      "header" auto
      "nav" auto
      "main" 1fr
      "aside" auto
      "footer" auto
      / 1fr;
  }
}
```

### Modern Aspect Ratio

```css
/* Legacy approach */
.aspect-ratio-legacy {
  position: relative;
  width: 100%;
  padding-bottom: 56.25%; /* 16:9 */
}

.aspect-ratio-legacy > * {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Modern approach */
.aspect-ratio-modern {
  aspect-ratio: 16 / 9;
  width: 100%;
  object-fit: cover;
}

.aspect-ratio-square { aspect-ratio: 1; }
.aspect-ratio-portrait { aspect-ratio: 3 / 4; }
.aspect-ratio-golden { aspect-ratio: 1.618; }
```

---

## Advanced Color Techniques

### Complex Gradients

```css
.mesh-gradient {
  background: 
    radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.4) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.4) 0%, transparent 50%),
    radial-gradient(circle at 40% 40%, rgba(120, 198, 120, 0.4) 0%, transparent 50%),
    linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.animated-gradient {
  background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
  background-size: 400% 400%;
  animation: gradientShift 15s ease infinite;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}
```

### Advanced Filters

```css
.filter-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.filter-item {
  transition: filter 0.3s ease;
}

.filter-item.vintage {
  filter: sepia(100%) contrast(120%) brightness(90%) saturate(80%);
}

.filter-item.cool {
  filter: hue-rotate(180deg) saturate(120%) brightness(110%);
}

.filter-item.dramatic {
  filter: contrast(150%) brightness(80%) saturate(130%) drop-shadow(0 0 20px rgba(0,0,0,0.5));
}

.filter-item.neon {
  filter: brightness(150%) contrast(150%) saturate(200%) hue-rotate(90deg) drop-shadow(0 0 10px currentColor);
}
```

### Glassmorphism Effect

```css
.glass-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 16px;
  padding: 2rem;
  box-shadow: 
    0 8px 32px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
}

.glass-navigation {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(15px) saturate(150%);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  z-index: 1000;
}
```

---

## CSS Shapes & Clipping

### Complex Clip Paths

```css
.clip-path-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
  padding: 2rem;
}

.shape {
  width: 200px;
  height: 200px;
  background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
}

.shape.triangle {
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
}

.shape.hexagon {
  clip-path: polygon(30% 0%, 70% 0%, 100% 50%, 70% 100%, 30% 100%, 0% 50%);
}

.shape.star {
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}

.shape.heart {
  clip-path: path('M12,21.35l-1.45-1.32C5.4,15.36,2,12.28,2,8.5 C2,5.42,4.42,3,7.5,3c1.74,0,3.41,0.81,4.5,2.09C13.09,3.81,14.76,3,16.5,3 C19.58,3,22,5.42,22,8.5c0,3.78-3.4,6.86-8.55,11.54L12,21.35z');
}
```

### Morphing Animations

```css
.morph-shape {
  width: 200px;
  height: 200px;
  background: var(--gradient-primary);
  animation: morphAnimation 4s ease-in-out infinite;
}

@keyframes morphAnimation {
  0%, 100% {
    clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
    border-radius: 0;
  }
  25% {
    clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%);
    border-radius: 25%;
  }
  50% {
    clip-path: circle(50%);
    border-radius: 50%;
  }
  75% {
    clip-path: polygon(30% 0%, 70% 0%, 100% 50%, 70% 100%, 30% 100%, 0% 50%);
    border-radius: 15%;
  }
}
```

---

## Container Queries

Container queries enable truly component-based responsive design.

```css
.card-container {
  container-type: inline-size;
  container-name: card;
  padding: 1rem;
}

.card {
  background: white;
  border-radius: 12px;
  padding: 1rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* Small container */
@container card (min-width: 300px) {
  .card {
    padding: 1.5rem;
  }
  
  .card__title {
    font-size: 1.25rem;
  }
}

/* Medium container */
@container card (min-width: 500px) {
  .card {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: 2rem;
    padding: 2rem;
  }
  
  .card__title {
    font-size: 1.5rem;
  }
}

/* Large container */
@container card (min-width: 700px) {
  .card {
    grid-template-columns: 1fr 1fr 1fr;
    padding: 3rem;
  }
  
  .card__title {
    font-size: 2rem;
  }
}

/* Container query units */
.responsive-element {
  font-size: 4cqw; /* 4% of container width */
  padding: 2cqh 3cqw; /* Container-relative units */
  margin: 1cqi; /* Container inline size */
}
```

---

## Advanced Animation Techniques

### Physics-Based Animations

```css
@keyframes springBounce {
  0% {
    transform: scale(0) rotate(0deg);
    animation-timing-function: cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
  50% {
    transform: scale(1.1) rotate(180deg);
    animation-timing-function: cubic-bezier(0.25, 0.46, 0.45, 0.94);
  }
  100% {
    transform: scale(1) rotate(360deg);
  }
}

.spring-element {
  animation: springBounce 0.8s ease-out;
}
```

### Staggered Animations

```css
.stagger-container {
  --stagger-delay: 0.1s;
}

.stagger-item {
  opacity: 0;
  transform: translateY(30px) scale(0.9);
  animation: staggerFadeIn 0.6s ease forwards;
}

.stagger-item:nth-child(1) { animation-delay: calc(1 * var(--stagger-delay)); }
.stagger-item:nth-child(2) { animation-delay: calc(2 * var(--stagger-delay)); }
.stagger-item:nth-child(3) { animation-delay: calc(3 * var(--stagger-delay)); }
.stagger-item:nth-child(4) { animation-delay: calc(4 * var(--stagger-delay)); }
.stagger-item:nth-child(5) { animation-delay: calc(5 * var(--stagger-delay)); }

@keyframes staggerFadeIn {
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
```

### Scroll-Driven Animations

```css
/* Progress bar that fills based on scroll */
.scroll-progress {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: linear-gradient(to right, var(--primary-color), var(--secondary-color));
  transform-origin: left;
  transform: scaleX(0);
  z-index: 1000;
}

/* Using experimental scroll timeline */
@keyframes scroll-progress {
  0% { transform: scaleX(0); }
  100% { transform: scaleX(1); }
}

.scroll-progress {
  animation: scroll-progress linear;
  animation-timeline: scroll(root);
}

/* Parallax effect */
.parallax-element {
  transform: translateZ(0); /* Hardware acceleration */
  will-change: transform;
}

/* JavaScript typically handles this, but CSS can provide the smooth transition */
.parallax-slow {
  transition: transform 0.1s ease-out;
}
```

---

## Modern CSS Features

### Logical Properties

```css
.logical-layout {
  /* Instead of margin-left/right */
  margin-inline-start: 1rem;
  margin-inline-end: 2rem;
  margin-inline: 1rem 2rem; /* shorthand */
  
  /* Instead of margin-top/bottom */
  margin-block-start: 1rem;
  margin-block-end: 2rem;
  margin-block: 1rem 2rem; /* shorthand */
  
  /* Padding equivalents */
  padding-inline: 1rem 2rem;
  padding-block: 0.5rem 1rem;
  
  /* Border equivalents */
  border-inline-start: 2px solid var(--primary-color);
  border-block-end: 1px solid var(--gray-300);
  
  /* Text alignment */
  text-align: start; /* Instead of left */
  text-align: end;   /* Instead of right */
}
```

### CSS Cascade Layers

```css
@layer reset, base, components, utilities;

@layer reset {
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
}

@layer base {
  body {
    font-family: system-ui, sans-serif;
    line-height: 1.6;
    color: var(--text-color);
  }
  
  h1, h2, h3 {
    line-height: 1.2;
  }
}

@layer components {
  .btn {
    padding: 0.5rem 1rem;
    border-radius: 0.25rem;
    border: none;
    cursor: pointer;
  }
  
  .card {
    background: white;
    border-radius: 0.5rem;
    padding: 1rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
}

@layer utilities {
  .text-center { text-align: center; }
  .hidden { display: none; }
  .sr-only { 
    position: absolute;
    width: 1px;
    height: 1px;
    clip: rect(0, 0, 0, 0);
  }
}
```

### Advanced Math Functions

```css
.math-layout {
  /* Responsive sizing with boundaries */
  width: clamp(300px, 50vw, 800px);
  font-size: clamp(1rem, 4vw, 2.5rem);
  
  /* Complex calculations */
  margin: calc(var(--base-margin) * 2);
  padding: calc(100% / var(--grid-columns) - var(--gap));
  
  /* Grid with dynamic columns */
  grid-template-columns: repeat(
    auto-fit, 
    minmax(
      clamp(250px, 20vw, 400px), 
      1fr
    )
  );
  
  /* Responsive spacing */
  gap: max(1rem, min(5vw, 3rem));
}
```

### Future CSS Features

```css
/* CSS Nesting (when supported) */
.nested-component {
  color: var(--text-color);
  
  &:hover {
    color: var(--primary-color);
  }
  
  & .nested-child {
    font-size: 0.875rem;
    
    &:focus {
      outline: 2px solid var(--focus-color);
    }
  }
  
  @media (max-width: 768px) {
    font-size: 0.8rem;
  }
}

/* Color functions (experimental) */
.future-colors {
  /* Perceptually uniform color space */
  color: oklch(70% 0.25 180);
  
  /* Device-independent colors */
  background: lab(50% 20 -30);
  
  /* Relative color syntax */
  border-color: hsl(from var(--brand-color) h s calc(l * 0.8));
}

/* Subgrid */
.subgrid-layout {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}

.subgrid-item {
  display: grid;
  grid-column: span 2;
  grid-template-columns: subgrid;
  gap: inherit;
}
```

---

## CSS Preprocessors

### Sass/SCSS Advanced Features

```scss
// Variables and Maps
$breakpoints: (
  'small': 480px,
  'medium': 768px,
  'large': 1024px,
  'xl': 1200px
);

$colors: (
  'primary': #3498db,
  'secondary': #2ecc71,
  'danger': #e74c3c,
  'warning': #f39c12
);

// Functions
@function color($name) {
  @return map-get($colors, $name);
}

@function breakpoint($name) {
  @return map-get($breakpoints, $name);
}

// Mixins
@mixin respond-to($breakpoint) {
  @media (min-width: breakpoint($breakpoint)) {
    @content;
  }
}

@mixin button-variant($bg-color, $text-color: white) {
  background-color: $bg-color;
  color: $text-color;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 0.25rem;
  cursor: pointer;
  transition: all 0.3s ease;
  
  &:hover {
    background-color: darken($bg-color, 10%);
    transform: translateY(-2px);
  }
  
  &:active {
    transform: translateY(0);
  }
}

// Usage
.btn {
  &--primary {
    @include button-variant(color('primary'));
  }
  
  &--secondary {
    @include button-variant(color('secondary'));
  }
  
  &--danger {
    @include button-variant(color('danger'));
  }
}

// Responsive grid system
.grid {
  display: grid;
  gap: 1rem;
  
  @include respond-to('medium') {
    grid-template-columns: repeat(2, 1fr);
  }
  
  @include respond-to('large') {
    grid-template-columns: repeat(3, 1fr);
  }
  
  @include respond-to('xl') {
    grid-template-columns: repeat
