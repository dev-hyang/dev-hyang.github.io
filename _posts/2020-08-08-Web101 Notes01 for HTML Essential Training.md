---
layout:     post
title:      2020-08-08-Web101 Notes01 for HTML Essential Training
subtitle:   Web Developer Path 01
date:       2020-08-08
author:     BY Elon
header-img: img/post-bg-loses.jpg
catalog: true
tags:
    - Web Development
    - HTML
---
><h2>S1</h2>
Three Gangs for Web Development: HTML + CSS + JavaScript.
HTML-HyperText Markup Language, is a declarative language which is simple, no programming logic, no loops or functions. If something goes wrong with HTML, if something is missing or mis-spelled, it just guess what it means and fix it. It will display the page anyway.

CSS-Cascading Style Sheet. A bit more computer structure in it which makes it more powerful. When something goes wrong, the browser will skip just the section of code and not apply that styling. But it will go on to apply the rest.

JS-THe most powerful, also most fragile. The browser could stop if something wrong.

><h2>S2</h2>
- Document Object Model(DOM) tree, the hierarchy and structure of HTML elements, often used for targeting elements in CSS and JavaScript.

Note: *Follow the code guidelines for HTML headlines user cases.* We should use the level of headline that makes sense, based on the semantic meaning of content.
- Paragraphs(p)
- Headlines(h1,h2,h3...,h6)
- Bold and Italics
	- tag-italic: i or em. i: means visual-only, while em means emphasis italic.
	- tag-bold: strong means importance, seriousness, urgency. b is for bold.

- Lists: Three types of lists: unordered list, ordered list and definition list. "li" "ul-li" "ol-li" "dl-dt-dd"

- Quotes: "blockquote" for large block use. While "q" stands for quote inline use.

	- inline tags vs block-level tags
		- inline: q, strong, em, b, i
		- block: blockqote, ul, p
- Dates and times(time): ..time datetime="YYYY-MM-DD"..text..time

- Code and pre and br(code): pre tag is to get the spacing into the content itself because it's inherent to the content. Pre and code are ferquently combined to provide a way to show a block of code with indentation.

- HTML entities: &lt;< &gt;>
- Subscripts and Superscripts, and small(sub, sup and small): like H<sub>2</sub>O, 2<sup>3</sup>=8, MathML: a kind of markup language for maths. We don't use small because we can use CSS to adjust the size.

><h2>S3</h2>
Four most important global attributes: Class, ID, Lang and Dir.

There are several instances where it’s hard to convey certain characters. For example, < and > are hard to type as content in HTML, so we can use the Character Entities FOO and BAR to represent them.

ARIA is used to clarify to the accessibility tree what is happening with a particular element, set of elements, or interface. If something is broken, ARIA can be a way to fix it.
 <q>It's especially bad if these compromises make a site hard or impossible for a person with a disability to use it. In fact, in many places it's illegal to make a website inaccessible to people with disabilities. Yeah, HTML can be a human rights issue. This is where ARIA Roles come in. The layer of information conveyed by ARIA tells screen readers, braille displays, magnifiers and other assistive technology things they need to know to make a site fully accessible. ARIA was invented right around the time more and more of the web started to replace native applications. And it's especially useful in making sure the functionality of a complex interface in an app is fully usable by everyone. Let's look at a design.</q>
