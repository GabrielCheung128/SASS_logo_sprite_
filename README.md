# SASS_logo_sprite_


Maintain Logo Sprites with SASS mixins

# Background:
Using Logo Sprites can reduce the requests for access, to increase the loading speed. But to maintain it is awful. So I built a strategy to make it easier to maintain with the SASS mixin.


# About combining the images into one:
Strongly recommend to use this tool(http://responsive-css.spritegen.com/). It will combine the images into one column with the css classes. It would be like below: 

	Image:
	LOGO-1
	LOGO-2
	LOGO-3
	…

	CSS:
	.a-logo-1 {
		Background-position: 0 0;
		Width: 100px;
		Height: 100px;
	}
	...

Why it should be in one column?

Because it won’t bother to worry about the background-position-x, and it will be much easier when you add new images to the exist one, just add them at the end of the existed one.

# About the mixin function: 

	@mixin rqs-logos($index, $heights, $widths){
		width: nth($widths, $index)/2 + 0px;
		height: nth($heights, $index)/2 + 0px;
	 	$position : 0;
	 	@if $index > 1 {
	   		@for $i from 1 through ($index - 1) {
	     			$position : $position + nth($heights, $i);
	   		}
	 	}
	 	background-position: 0 -$position + 0px;
		#for Retina screens, you need to -($position/2) instead of -$position
	}

	With padding between logos:

	@mixin rqs-logos($index, $heights, $widths){
		width: nth($widths, $index)/2 + 0px;
		height: nth($heights, $index)/2 + 0px;
 		$position : 0;
	 	@if $index > 1 {
	   		@for $i from 1 through ($index - 1) {
	     			$position : $position + nth($heights, $i) + $padding;
	   		}
	 	}
	 	background-position: 0 -$position + 0px;
	}

#Usage: 
	Firstly, you need to set up two array of the height and width of all logos:

		$logo-heights: 75, 56, 98, 92, 103, 75, 70, 40, 68, 80, 69, 34, 57, 57;
		$logo-widths: 472, 354, 330, 325, 310, 248, 248, 243, 240, 236, 226, 210, 204, 194;

	Secondly, set up a base class: 
		.base {
			background-image: image-url("ofc/ofc-logos@2x.png");
			background-size: 236px auto;
		}

	Thirdly, specific class: 
		&.logo-1 {
			@include rqs-logos(3, $logo-heights, $logo-widths );
		}

	Notice that the index begins with 1 instead of 0 in SASS.


	
