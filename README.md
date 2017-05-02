# BlockParty
A simple SASS framework for rapid, mobile first development.

After years of toying with SASS frameworks such as Susy and Bourbon (+Neat), I've finally followed through on my threats to create my own simplistic SASS based framework, in a way that better suits my development style. In time I hope to grow this project into a full-featured, but minimal suite for like-minded developers.

## Scaffolding

Let's be honest, when was the last time you used anything but the 'border-box' attribute of the CSS 'box-sizing' property? Never? Yeah...That's pretty much how it should be in the modern age. As such, BlockParty is going to set the <html> tag to use border-box by default, and have all other elements inherit the 'border-box' attribute as your html cascades. BlockParty also will remove any padding and margin applied to the <body> or <html> tag by browser stylesheets. No fancy mixins or work to be done here, but rather some default CSS just applied by including BlockParty. That's all we really need to get started, so enough said about the basic setup.

## Default Config

Below are the default settings applied by the framework. Feel free to override any of these to your own custom values.

## Media Queries

BlockParty handles media queries primarily through the use of the 'min-query' mixin:
```css
@include min-query($md) { /* your css here */ }
```
Simply add your CSS code and apply the breakpoint variable of your choice, and a 'min-width' media query will be created beginning at the specified breakpoint. I'll admit that there's not a lot of special sauce here&emdash;the mixin is really just shorthand for an old-fashioned CSS media query. Skip ahead to the next section to find out more about the preset breakpoints included with BlockParty, or how to establish new, custom breakpoints for use in your project.

If you are truly developing mobile first, the 'min-query' mixin above should handle 99% of your use cases. But for the sake of inclusion, I've also included a 'max-query' mixin:
```css
@include max-query($lg) { /* your css here */ }
```
The 'max-query' mixin will subtract 1px from the minimum threshold of the established breakpoint, establishing a 'max-width' media query up to, but not including, the specified breakpoint.

Note that I have intentionally excluded a mixin for creating media rules that only apply between a minimum and maximum value at this time. You should try to write cleaner code to avoid the need for these, but if you absolutely must, you could always nest the 'min-query' and 'max-query' mixins like so:

## Breakpoints

The default breakpoints for BlockParty are as follows:
```css
$sm: 768px;
$md: 992px;
$lg: 1200px;
$xl: 1400px;
```
If you've ever used the Bootstrap CSS framework, these should look familiar. The established breakpoints represent a minimum threshold, meaning that each breakpoint includes everything upwards, and has no upper limit. Each of the breakpoints above can be used with the included media query mixins out of the box, and of course you may override these default variables in your own project should you desire to.

Creating additional breakpoints is as simple as using the 'custom-breakpoint' function:
```css
$custom: custom-breakpoint(400px);
```
As with the defaults, the pixel value passed to the function should represent a minimum value. It's also OK if you forget to add the unit -- BlockParty will handle that for you.

## The Grid

The first component of the grid system is the 'container' mixin. This concept should be familiar to anyone who has used a responsive framework in the past. Simply pass the mixin a value, and it will create a div with a maximum width property. If no width is specified, the default value will be used.
```css
@include container(1200px);
```

The second necessary component of our grid system is the 'row' mixin. This will apply clearfixes, and avoid layout issues caused by floats. Again, like the 'container' mixin, this should be a familiar concept for those familiar with responsive design. Apply this mixin to any parent element that contains floats.
```css
@include row();
```

In coordination with the 'container' and 'row' mixins, BlockParty creates a float based grid system by utilizing the 'columns' mixin. Simply specify a number of columns that the element should span, out of the total number of columns within the row, as well as a gutter value in pixels, which wil be applied as a 'margin-right' property.
```css
@include columns(6 of 12 20px);
```
Again, make sure to always wrap any columns within an element that utilizes the 'row' mixin described above in order avoid the issues characteristic of float based layouts.

I've intentionally created BlockParty in such a way that it avoids creating a global default number of columns, or specifying a number of columns for each media breakpoint like some other SASS frameworks. Doing so is convenient, but only until it isn't. You end up with a default value, which gets overridden by a column value unique to that breakpoint, which can then be overridden by properties passed to the column mixin. The result is code that becomes difficult to interpret, especially when collaborating with other developers. The same is true for the gutter property. Yes, you will have to specify a total number of columns and a gutter value for each use of the 'columns' mixin, but ultimately, it provides more flexibility.

So how does it work? BlockParty utilizes a gutter between grid elements that is applied as a 'margin-right' CSS property. Because we assume that all layouts will be coded left to right, the last element in the grid has its margin-right property removed, and that grid width is then redistributed accordingly and applied in equal parts to widths of the elements in the row. The result is a gutter between each element, but content that aligns nicely and fills the full width of the containing element. It's stupid simple. There's no 'omega' to worry about (a la Bourbon neat <= 1.8), nor do you have to create a myriad of different grid layouts (a la Bourbon Neat 2.0). If you want to create a different column layout at a different screen size, simply use the media query functionality described above and use the 'columns' mixin within the media query, like so:
```css
.foo {
	@include min-query($md) {
		@include columns(4 of 12 30px);
	}
	@include columns(6 of 12 20px);
}
```

It's important to note that your elements within the same row should use the same gutter property. Unfortunately this is an unavoidable limitation. Using a different gutter value for elements within the same row will result in issues at this time.

## Pushing and Pulling
Blockparty has support for re-ordering columns using the 'push' and 'pull' mixins. Simply specify a number of columns and maximum number of columns, similar to the 'columns' mixin.
```css
@include push(6 of 12);
```
```css
@include pull(6 of 12);
```
This can be used to reorder columns at a specified resolution when used in conjunction with the 'min-query' and 'max-query' mixins.


