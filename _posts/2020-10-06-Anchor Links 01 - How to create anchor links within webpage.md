---
layout:     post
title:      2020-10-06-Anchor Links 01 - How to create anchor links within webpage
subtitle:   id or name attribute for HTML tags
date:       2020-10-06
author:     BY Elon
header-img: img/post-bg-html5css.png
catalog: true
tags:
    - HTML5
    - CSS
    - Shopify
    - Web Development
    - Frontend
---
# Problems met when develop Shopify
1.  How to create anchor links in navigation bar?
Add &lt;html&gt; content into the webpage with specific ids, then use this ids as the #id in the hyperlinks.

The solution does not work in the mobile or other narrow screen medias, but the desktop or wider screen work perfectly. Even though we tried add @media into the CSS file. The theme simply does not support such feature.

Then An idea just come to my mind. 冥想Mediation helps. Since we could not perform such actions in the navigation bar, but we could make it work within page. We simply made a specific guidelines in each page with their corresponding anchors.

2. How to make the anchors jump to the correct place if clicked from outside/other webpages. Conflicts between anchors and image lazyloading strategy.
Add JS custom code to disable lazyloading like below:


3. How to avoid anchors overlapping with sticky/fixed header?
Make anchor CSS to be padding-top, margin-top opposite values.

# How to create anchor links within webpage?

"Hash#" Symbol is the key factor. There is an easy way to create anchors in the html5 codes. We are aware of the fact that HTML5 does nothing to do with the business logic. Open the editor, write below codes in your html5 file:

	<ul id="nav">
		<li><a href="#block1" class="test-anchor-link">Block 1</a></li>
		<li><a href="#block2" class="test-anchor-link">Block 2</a></li>
		<li><a href="#block3" class="test-anchor-link">Block 3</a></li>
	</ul>
	<div id="block1" class="block">
		<h2>Block 1</h2>
		<a href="#block2" class="test-anchor-link">Flash to Block2</a>
	</div>
	<div id="block2" class="block">
		<h2>Block 2</h2>
		<a href="#block3" class="test-anchor-link">Flash to Block3</a>
	</div>
	<div id="block3" class="block">
		<h2>Block 3</h2>
		<a href="#block1" class="test-anchor-link">Flash to Block1</a>
	</div>

And write your CSS file:

	html, body {
	  margin: 0;
	  padding: 0;
	}
	* {
	  box-sizing: border-box;
	  font-family: 'Lato', sans-serif;
	  font-weight: 400;
	}
	#nav {
	  position: fixed;
	  top: 0;
	  left: 0;
	  background: #333;
	  margin: 0;
	  padding: 15px;
	  list-style: none;
	  border-radius: 0 0 10px 0;
	  box-shadow: 0 0 8px rgba(0,0,0,0.6);
	}
	#nav a {
	  display: block;
	  padding: 10px 10px;
	  color: #fff;
	}
	#nav a:hover {
	  color: #ff0;
	}
	.block {
	  height: 1000px;
	  padding: 30px 140px;
	}
	#block1 {
	  background: #eee;
	}
	#block2 {
	  background: #ddd;
	}
	#block3 {
	  background: #ccc;
	}
	h1 {
	  margin: 0 0 20px 0;
	}
	.block a {
	  color: #3399FF;
	}

Here is the JS for smoothly scrolling(most websites take the feature by default?)

	/*
	Smooth scroll functionality for anchor links (animates the scroll
	rather than a sudden jump in the page)
	*/
	$('.test-anchor-link').click(function(e){
	  e.preventDefault();
	  var target = $($(this).attr('href'));
	  if(target.length){
	    var scrollTo = target.offset().top;
	    $('body, html').animate({scrollTop: scrollTo+'px'}, 800);
	  }
	});

## Test from [Codepen Smooth Scrolling](https://codepen.io/jooleearr/pen/gpooKj)

## For [attribute selectors] in CSS(https://www.w3.org/TR/selectors-3/#attribute-selectors)

## For [All CSS selector reference](https://www.w3schools.com/cssref/css_selectors.asp)

## For [CSS Units px, em, %, etc](https://www.w3schools.com/cssref/css_units.asp)
There are two types of length units: absolute and relative.
Absolute length units are not recommended for use on screen, because screen sizes vary so much. However, they can be used if the output medium is known, such as for print layout.

* Pixels (px) are relative to the viewing device. For low-dpi devices, 1px is one device pixel (dot) of the display. For printers and high resolution screens 1px implies multiple device pixels. pixels (1px = 1/96th of 1in)

Relative length units specify a length relative to another length property. Relative length units scale better between different rendering medium. The em and rem units are practical in creating perfectly scalable layout!
* Viewport = the browser window size. If the viewport is 50cm wide, 1vw = 0.5cm.

## [Z-index in CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) 
CSS property sets the z-order of a positioned element and its descendants or flex items. Overlapping elements with a larger z-index cover those with a smaller one.

For a positioned box (that is, one with any position other than static), the z-index property specifies: The stack level of the box in the current stacking context, whether the box establishes a local stacking context.

# How to set the anchor links in the navigation menu?
It's similar to create anchor link within the webpage. Just put #id_value after the hyperlink in the navigation bar if the navigation bar is separately built.

## The difference between http://domain.name/products#kids and http://domain.name/products/#kids and http://www.domain.name/products/#kids
In my testing, The first would not refresh the webpage, just scroll to the anchor "kids". The last two ways are same and they will redirect to the page and refresh it without smooth scrolling - it is a sunden jump.

# [Anchor Links VS sticky header conflicts](https://codepen.io/jewwy0211/pen/zLNxPO)
Use CSS Class style to make up the padding-top and margin-top attribute with opposite values. Like this:
:target::before {
  content: '';
  display: block;
  height: 5rem;
  margin-top: -5rem;
}


# [:target in the anchor links](https://developer.mozilla.org/en-US/docs/Web/CSS/:target)

# ::before vs :before in CSS
The only difference is that the double colon is used in CSS3, whereas the single colon is the legacy version. Reasoning: The ::before notation was introduced in CSS 3 in order to establish a discrimination between pseudo-classes and pseudo-elements. Browsers also accept the notation :before introduced in CSS 2.