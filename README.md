# BlockParty
A simple SASS framework for rapid, mobile first development.

## Scaffolding

A bit quick scaffolding before we begin. Blockparty will output the following CSS scaffolding for your project:
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
## Media Queries

BlockParty handles media queries primarily through the use of the 'min-query' mixin:
```css
@include min-query($md) { /* your css here */ }
```
Simply add your CSS code and apply the breakpoint variable of your choice, and a 'min-width' media query will be created beginning at the specified breakpoint. Skip ahead to the next section to find out more about the preset breakpoints included with BlockParty, or how to establish new, custom breakpoints for use in your project.

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
As with the defaults, the pixel value passed to the function should represent a minimum value. This framework is designed primarily to be used with pixels, so if you exclude the unit it will be automatically added.

## The Grid

The first component of the grid system is the 'container' mixin. This concept should be familiar to anyone who has used a responsive framework in the past. Simply pass the mixin a value, and it will create a div with a maximum width property. If no width is specified, the default value of 1200px will be used.
```css
@include container(1200px);
```

The second necessary component of our grid system is the 'row' mixin. This will apply clearfixes, and avoid layout issues caused by floats. Again, like the 'container' mixin, this should be a familiar concept for those familiar with responsive design, and the Bootstrap system in particular. Apply this mixin to any parent element that contains floated elements. There is no styling applied to row element itself, but the clearfix is handled by a pseudo element.
```css
@include row();
```

In coordination with the 'container' and 'row' mixins, BlockParty creates a float based grid system by utilizing the 'columns' mixin. Simply specify a number of columns that the element should span, out of the total number of columns within the row, as well as a gutter value in pixels, which will be applied as a 'margin-right' property.
```css
@include columns(6 of 12 20px);
```
If you want to create a different column layout at a different screen size, simply use the media query functionality described above and use the 'columns' mixin within the media query.

## The Part Where I Explain Things...
I intentionally created BlockParty in such a way that it avoids creating a global default number of columns, or specifying a number of columns for each media breakpoint like some other SASS frameworks. Doing so is convenient, but only until it isn't. You end up with a mess of default values, which can then be overridden by properties passed to the column mixin on a per use basis. Yes, it's not particularly DRY to specify a total number of columns and a gutter value for each use of the 'columns' mixin, but ultimately, it provides more flexibility.

BlockParty utilizes a gutter between grid elements that is applied as a 'margin-right' CSS property. Because we assume that all layouts will be coded left to right, the last element in the grid has its margin-right property removed, and that gutter width is then redistributed accordingly and applied in equal parts to widths of the elements in the row using a little math. The result is a gutter between each element, but content that aligns nicely and fills the full width of the containing element.

But wait! What if you want an element to span a different number of columns at different resolutions? Consider the following example:
```css
.foo {
	@include columns(6 of 12 20px);
	@include min-query($md) {
		@include columns(3 of 12 30px);
	}
}
```
In the above example, the '.foo' class would span one half (50%) up to the '$md' breakpoint, and then then span one fourth (25%). If you had only negated the 'margin-right' property of the last child within the row, you would be left with an awkward margin-right value on the second element prior to the '$md' breakpoint. Blockparty addresses this issue by calculating the final element visually at the given breakpoint, and removing the 'margin-right' from that element, as well as the final element within the row.

It's important to note that your elements within the same row should use the same gutter value. Unfortunately this is an unavoidable limitation. Using a different gutter value for elements within the same row will result in issues at this time.

## Pushing and Pulling
Blockparty has support for re-ordering columns using the 'push' and 'pull' mixins. Simply specify a number of columns and maximum number of columns, similar to the 'columns' mixin. 'Push' moves elements to the right, while 'Pull' moves elements to the left. This becomes quite useful for re-ordering content when used in combination with the media query mixins.
```css
@include push(6 of 12);
```
```css
@include pull(6 of 12);
```

## Known Issues

right now if you try to use a different gutter for different elements within a row... it breaks. Fuck.

I wonder if there's a way to output the media queries at the end of the file? Right now if you use the column mixin multiple times, it will only obey the last one in the file.




