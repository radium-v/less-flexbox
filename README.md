# less-flexbox
This is a collection of Less mixins for [CSS3 Flexbox](http://www.w3.org/TR/css3-flexbox/).

## Browser support
[Flexbox](http://caniuse.com/#feat=flexbox) is supported, in one way or another, by all major browsers. Due to the changes in the spec over time, I've decided to only include support for the "New" Flexbox spec and not for the older "Legacy" spec.

Although [Internet Explorer 10 uses different property names](http://zomigi.com/blog/flexbox-syntax-for-ie-10/) (for example, `flex-pack` instead of `justify-content`), its flexbox behavior is mostly the same as in other browsers. Also, IE10's alternate grammar doesn't include separate properties for `flex-grow`, `flex-shrink`, and `flex-basis`, so these mixins are not included in this collection.

## Usage

You can use less-flexbox by importing it into your Less project. All standard mixins are enclosed in the `#flexbox` namespace, and all mixin helpers are in the `._flex` namespace.

#### Directly call the mixins you need

The benefit to using this method is that all properties are explicitly output, which may make in-browser debugging easier.

```less
	@import (reference) "flexbox";

	.box {
		// You can explicitly reference the namespace on each mixin call
		#flexbox .display(flex);
		#flexbox .align-items(center);
	}

	.flexy-box {
		// Or you can call the namespace once and save some extra lines
		#flexbox;
			.display(inline-flex);
			.direction(column);
	}
```

See [Namespaces & Ancestors](http://lesscss.org/features/#features-overview-feature-namespaces-accessors) for more information on namespacing in Less.

#### Extend mixin helpers

The `._flex` namespace includes many of the commonly-used property-value pairs available with flexbox. If you use a [DRY approach](http://www.vanseodesign.com/css/dry-principles/), this method should be familiar.

```less
	@import (reference) "flexbox";

	.box {
		&:extend(
			._flex .display--flex,
			._flex .align-items--center
		);
	}
```

This method works well when [using Less in conjunction with Modernizr](http://lesscss.org/features/#parent-selectors-feature-changing-selector-order).

```less
	.box {
		display: block;

		.flexbox & { // .flexbox .box
			&:extend(._flex .display--flex);
			#flexbox .flex(1, 0, 50%);
		}
	}
```
