# BlockParty
A simple SASS framework for rapid, mobile first development.

After years of toying with SASS frameworks such as Susy and Bourbon (+Neat), I've finally followed through on my threats to create my own simplistic SASS based framework, the way I think it should work. Care to join me?

## Grid Scaffolding

```css
```

## Media Queries

BlockParty handles media queries primarily through the use of the 'min' mixin:
```css
@include min($md) {}
```
Simply add your CSS code within the brackets, and a 'min-width' media query will be created beginning at the specified breakpoint. Skip ahead to the next section to find out about the preset breakpoints included with BlockParty, or how to establish new, custom breakpoints.

If you are truly developing mobile first, the 'min' mixin should handle 99% of your use cases. But for the sake of completion, I've also included a 'max' mixin:
```css
@include max($lg) {}
```
The 'max' mixin will subtract 1px from the minimum threshold of the established breakpoint, establishing a 'max-width' media query up to the specified breakpoint.

Note that I have intentionally excluded a mixin for creating media rules that only apply between a minimum and maximum value. You should try to write cleaner code to avoid the need for these, but if you absolutely must, you could always nest the 'min' and 'max' mixins like so:

## Breakpoints

The default breakpoints for BlockParty are as follows:
```css
$sm: 768px;
$md: 992px;
$lg: 1200px;
$xl: 1400px;
```
If you've ever used Bootstrap, these should look familiar.

Creating a custom breakpoint is as simple as using the 'custom-breakpoint' function:
```css
$custom: custom-breakpoint(400px);
```
Note that the value of the breakpoint should always represent the minimum threshold. You can also replace the existin breakpoints with your own pixel values of you desire.

## The Grid

Blockparty creates a float based grid system by using the included 'columns' mixin. Simply specify a number of columns that the element should span, out of the total number of columns within the row.
```css
@include columns(6 of 12);
```
Make sure to always wrap any columns within an element that uses the 'row' mixin described in the first section. This will apply clearfixes, and avoid layout issues caused by floats.

