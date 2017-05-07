# BlockParty
A simple SASS framework for rapid, mobile first development.

## Scaffolding

A bit of quick setup before we begin. Blockparty will output the following CSS scaffolding for your project:
```css
*, *:after, *:before {
	box-sizing: inherit;
}

body, html {
	margin: 0;
	padding: 0;
}

html {
	box-sizing: border-box;
}
```
## Grid Settings
The default settings for the grid system are as follows:
```css
$columns: 12;
$container: 1200px;
$gutter: 2em;
```
Feel free to override any of these variables to suit your own needs in your project file.
## The Grid System
The first component of the grid system is the 'container' mixin. This concept should be familiar to anyone who has used a responsive framework in the past. Simply pass the mixin a number value, and it will create a centered div with a maximum width property. If no width is specified, the default value will be used.
```css
@include container(1200px);
```

The second necessary component of the grid system is the 'row' mixin. This will apply clearfixes, and avoid layout issues caused by floats. Again, like the 'container' mixin, this should be a familiar concept for those familiar with responsive design, and the Bootstrap system in particular. Apply this mixin to any parent element that contains floated elements. There is no styling applied to row element itself, but the clearfix is handled by a pseudo element.
```css
@include row();
```

In coordination with the 'container' and 'row' mixins, BlockParty creates a float based grid system by utilizing the 'columns' mixin. Simply specify a number of columns that the element should span relative to the number of columns in the layout. If you are using the 'columns' mixin outside of the 'grid' mixin, the default value for number of columns will be utilized.
```css
@include columns(6);
```
If you want to create a different column layout at a different screen size, continue reading to learn more about the media query functionality included with BlockParty.

## Pushing and Pulling Columns
BlockParty has support for re-ordering columns using the 'push' and 'pull' mixins. Simply specify a number of columns, similar to the 'columns' mixin. 'Push' moves elements to the right, while 'Pull' moves elements to the left. This becomes quite useful for re-ordering content when used in combination with the media query mixins.
```css
@include push(6);
```
```css
@include pull(6);
```
## Offsetting Columns
In some situations, you'll want to offset a column.
```css
@include offset(6);
```
This will create a 'margin-left' property, offsetting the column in our left to right layout.

## Media Queries
BlockParty handles media queries primarily through the use of the 'min-query' mixin:
```css
@include min-query($md) { /* your css here */ }
```
Simply add your CSS code and apply the breakpoint variable of your choice, and a 'min-width' media query will be created beginning at the specified breakpoint. Skip ahead to the next section to find out more about the preset breakpoints included with BlockParty, or how to establish new, custom breakpoints.

If you are truly developing mobile first, the 'min-query' mixin above should handle 99% of your use cases. But for the sake of inclusion, I've also included a 'max-query' mixin:
```css
@include max-query($lg) { /* your css here */ }
```
The 'max-query' mixin will subtract 1px from the minimum threshold of the established breakpoint, establishing a 'max-width' media query up to, but not including, the specified breakpoint.

I have intentionally excluded a mixin for creating media rules that only apply between a minimum and maximum value at this time. You should try to write cleaner code to avoid the need for these, but if you absolutely must, you could always nest the 'min-query' and 'max-query' mixins to achieve this.

## Breakpoints
The default breakpoints for BlockParty are as follows:
```css
$sm: 768px;
$md: 992px;
$lg: 1200px;
$xl: 1400px;
```
The established breakpoints represent a minimum threshold, meaning that each breakpoint includes everything upwards, and has no upper limit. Each of the breakpoints above can be used with the included media query mixins out of the box, and of course you may override these default variables in your own project should you desire to.

Creating additional breakpoints is as simple as using the 'custom-breakpoint' function:
```css
$custom: custom-breakpoint(400px);
```
As with the defaults, the pixel value passed to the function should represent a minimum value.
## Custom Grids
In some situations, you'll want to alter the default grid settings to adjust the container size, number of columns, or gutter size. This can be done using the 'layout' mixin. Any use of the 'columns,' 'push,' 'pull,' or 'offset' mixin within a custom layout will inherit the settings of the layout.

Begin by defining the layout using the 'custom-layout' function:

```css
$my_layout: custom-layout();
```

To utilize a previously defined custom layout, simply use the 'layout' mixin:
```css
@include layout($my_layout) { /* your css here */ }
```
## Why BlockParty?/How Does It Work?
The goal was to design something lightweight and minimal, but functional. The grid system is float based, and utilizes the 'margin-right' CSS property to create gutters. By default, the final element inside of a row will have a 'margin-right' of zero, and the width of the gutter will be equally distributed among the components of the row so that the width of the columns is accurate, but the entire width of the row is filled. Some grid systems would simply exclude the gutter of the final element and add it back to the width of the div, resulting layouts with uneven or innacturate widths. As an added benefit, BlockParty also will find the last visual element within a row at any given breakpoint, and attempt to remove the 'margin-right' attribute of that element, again redistributing the extra space equally. This allows you to vary the final element visually. Consider the following example:
```css
.foo {
	@include columns(6);
	@include min-query($md) {
		@include columns(3);
	}
}
```
In the example above, a the div '.foo' would span 50% of the row (assuming we are using the default 12 column grid), but at the '$md' breakpoint would span 25% of the row. Assuming there are 4 divs with the class 'foo', many grid systems would leave you with an awkward gutter after the second element leading up to the '$md' breakpoint.


