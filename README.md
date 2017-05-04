# BlockParty
A simple SASS framework for rapid, mobile first development.

## Scaffolding

A bit quick setup before we begin. Blockparty will output the following CSS scaffolding for your project:
```css
*, *:after, *:before {
	box-sizing: inherit;
}

body, html {
	margin: 0;
	padding: 0; }

html {
	box-sizing: border-box;
}
```
## Grid Settings
The default settings for the grid system are as follows:
```css
$container: 1200px;
$columns: 12;
$gutter: 2em;
```
Feel free to override any of these variables to suit your own needs in your project file.

## Grid Usage
The first component of the grid system is the 'container' mixin. This concept should be familiar to anyone who has used a responsive framework in the past. Simply pass the mixin a number value, and it will create a centered div with a maximum width property. If no width is specified, the default value of specified in the previous section will be used.
```css
@include container(1200px);
```

The second necessary component of our grid system is the 'row' mixin. This will apply clearfixes, and avoid layout issues caused by floats. Again, like the 'container' mixin, this should be a familiar concept for those familiar with responsive design, and the Bootstrap system in particular. Apply this mixin to any parent element that contains floated elements. There is no styling applied to row element itself, but the clearfix is handled by a pseudo element.
```css
@include row();
```

In coordination with the 'container' and 'row' mixins, BlockParty creates a float based grid system by utilizing the 'columns' mixin. Simply specify a number of columns that the element should span relative to the number of columns in the layout. If you are using the 'columns' mixin outside of the 'layout' mixin, the default value for number of columns specified in the previous section will be utilized.
```css
@include columns(6);
```
If you want to create a different column layout at a different screen size, continue reading to learn more about the media query functionality included with BlockParty.

## Custom Layouts


## Pushing and Pulling
BlockParty has support for re-ordering columns using the 'push' and 'pull' mixins. Simply specify a number of columns, similar to the 'columns' mixin. 'Push' moves elements to the right, while 'Pull' moves elements to the left. This becomes quite useful for re-ordering content when used in combination with the media query mixins.
```css
@include push(6);
```
```css
@include pull(6);
```

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

Note that I have intentionally excluded a mixin for creating media rules that only apply between a minimum and maximum value at this time. You should try to write cleaner code to avoid the need for these, but if you absolutely must, you could always nest the 'min-query' and 'max-query' mixins to achieve this.

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
As with the defaults, the pixel value passed to the function should represent a minimum value.

## Why BlockParty?




