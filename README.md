# BlockParty
A simple SASS framework for rapid, mobile first development.

After years of toying with SASS frameworks such as Susy and Bourbon (+Neat), I've finally followed through on my threats to create my own simplistic SASS based framework, in a way that better suits my development style. In time I hope to grow this project into a full-featured, but minimal suite for like minded developers.

## Scaffolding

Let's be honest, when was the last time you used anything but the 'border-box' attribute of the 'box-sizing' property? As such, BlockParty is going to set the <html> tag to use border-box by default. It also will remove any padding and margin applied to the <body> or <html> tag by browser stylesheets. That's all we really need to get started, so enough said about the basic setup.

## Media Queries

BlockParty handles media queries primarily through the use of the 'min-query' mixin:
```css
@include min-query($md) { /* your css here */ }
```
Simply add your CSS code, and a 'min-width' media query will be created beginning at the specified breakpoint. Skip ahead to the next section to find out more about the preset breakpoints included with BlockParty, or how to establish new, custom breakpoints for use in your project.

If you are truly developing mobile first, the 'min-query' mixin should handle 99% of your use cases. But for the sake of completion, I've also included a 'max-query' mixin:
```css
@include max-query($lg) { /* your css here */ }
```
The 'max-query' mixin will subtract 1px from the minimum threshold of the established breakpoint, establishing a 'max-width' media query up to the specified breakpoint.

Note that I have intentionally excluded a mixin for creating media rules that only apply between a minimum and maximum value at this time. You should try to write cleaner code to avoid the need for these, but if you absolutely must, you could always nest the 'min-query' and 'max-query' mixins like so:

## Breakpoints

The default breakpoints for BlockParty are as follows:
```css
$sm: 768px;
$md: 992px;
$lg: 1200px;
$xl: 1400px;
```
If you've ever used the Bootstrap CSS framework, these should look familiar. The established breakpoints represent a minimum threshold, meaning that each breakpoint includes everything upwards. All of these can be used with the included media query mixins out of the box. Feel free to override these default variables in your project if you wish.

Creating additional breakpoints is as simple as using the 'custom-breakpoint' function:
```css
$custom: custom-breakpoint(400px);
```
As with the defaults, the pixel value passed to the function should represent a minimum value. It's also OK if you forget to add the unit -- BlockParty will handle that for you.
## The Grid

BlockParty creates a float based grid system by using the included 'columns' mixin. Simply specify a number of columns that the element should span, out of the total number of columns within the row.
```css
@include columns(6 of 12);
```
Make sure to always wrap any columns within an element that utilizes the 'row' mixin described in the first section. This will apply clearfixes, and avoid layout issues caused by floats.

I've intentionally created BlockParty in such a way that it avoids creating a global default number of columns, or specifying a number of columns for each media breakpoint like some other SASS frameworks. Doing so is convenient, only until it isn't. You end up with a default value, which gets overridden by a column value unique to that breakpoint, which can then be overridden by properties passed to the column mixin. The result is code that becomes difficult to interpret, especially when collaborating with other developers.

So how does it work? BlockParty utilizes a gutter between grid elements that is applied as a margin-left CSS property. Because we assume that all layouts will be coded left to right, the left-most element in the grid has its margin-left property removed, and that grid width is then redistributed accordingly and applied in equal parts to widths of the elements in the row. The result is a gutter between each element, but content that aligns nicely and fills the full width of the containing element.

