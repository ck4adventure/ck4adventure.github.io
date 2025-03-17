---
layout: post
title: Web Form Review
category: html
---

After looking at a few different template libraries yesterday, I realized I could use a quick refresher on html elements. I have not ever had to implement anything with regards to accessibiiliy technology, but it is something to consider, and the mozilla docs do a great job of explaining. 

> One of the first things to remember is to always take a moment to actually tab through and `listen` to the final form to see if it actually makes sense.

The first couple of helpers in forms that I don't always think of are `<fieldset>` and `<legend>`. Fieldsets are for grouping logically related fields, such as a set of radio buttons for choosing a drink size. The legend is a label for the entire fieldset, in this case maybe "drink size". Assistive technology will read the legend in front of each input choice, such as "small" to create the verbal label of "drink size: small". `<section>` is another tool for grouping functionality together.

An example of a simple form with radio buttons.
```html
<form>
  <fieldset>
    <legend>Fruit juice size</legend>
    <p>
      <input type="radio" name="size" id="size_1" value="small" />
      <label for="size_1">Small</label>
    </p>
	<p>
      <input type="radio" name="size" id="size_2" value="medium" />
      <label for="size_2">Medium</label>
    </p>
  </fieldset>
</form>
```
The `<label>` is the most single important thing. Not only is it useful to sighted users, it is read aloud before each input field.

Alternatively, a label can wrap the input and be linked implicitly, although it is still recommended to use the `"for"` attribute of the label to link to the `id` of the input.

For aria labels, this is best practice
```html
<div>
  <label for="username">Name: <span aria-label="required">*</span></label>
  <input id="username" type="text" name="username" required />
</div>
```

The moz docs link to this very much still appropriate article from 2005 on [Sensible Forms](https://alistapart.com/article/sensibleforms/)

And wow there are a lot of available elements for html now. I feel my age, I grew up with the basics, having learned tables in 1999.