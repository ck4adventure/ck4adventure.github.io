---
layout: page
title: CSS Cheatsheet
topic: css
category: css
---
A basic css reset I got from my school and after trying a couple others, this one is still my preferred.

```css
html, body, header, nav, h1, a,
ul, li, strong, main, button, i,
section, img, div, h2, p, form,
fieldset, label, input, textarea,
span, article, footer, time, small {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  font: sans-serif;
  font-size: 100%;
  color: inherit;
  text-align: inherit;
  text-decoration: inherit;
  vertical-align: inherit;
  box-sizing: inherit;
  background: transparent;
  list-style: none;
}

/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
  display: block;
}

body {
  line-height: 1.5;
}

ol, ul {
  list-style: none;
}

/* This is useful when implementing a grid system so that all image elements
will take up 100% width of their containers */
img {
  width: 100%;
}

input[type="radio"], select, input[type="submit"] {
  cursor: pointer;
  outline: none;
}

blockquote, q {
  quotes: none;
}

blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
}

input[type="password"],
input[type="email"],
input[type="text"],
input[type="submit"],
textarea,
button {
  /*
  Get rid of native styling. Read more here:
  http://css-tricks.com/almanac/properties/a/appearance/
  */
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
}

button,
input[type="submit"] {
  cursor: pointer;
}

```