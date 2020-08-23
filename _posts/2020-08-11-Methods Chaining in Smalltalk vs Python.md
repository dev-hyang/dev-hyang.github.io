---
layout:     post
title:      2020-08-11-Methods Chaining in Smalltalk vs Python
subtitle:   Method Chaining or Message cascading
date:       2020-08-11
author:     BY Elon
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - OOP
    - Function Programming
---
- <h1>What's Message Cascading/Methods Chaining?</h1>
	* Methods Chaining is also known as named parameter idiom, is a common syntax for invoking multiple calls in object-oriented programming. Each method returns an object, allowing the calls to be chained together in a single statement without requiring variables to store the intermediate results.

	* Similar syntax is **message/method cascading**, where after the method call, the expression evaluates to the current project, not the return value of the method. Cascading can be implemented using method chaining by having the method ***return the current object itself***. Cascading is a key tech in fluent interfaces.

		+ A cascade sends multiple messages to the same receiver
		+ As far as we see, ruby has no direct way to support cascading method calls
		+ If a series of messages are sent to the same receiver, they can also be written as a cascade with individual messages separated by semicolons in Smalltalk.
- Take an example: How would you implement the following code? # one().plus().two().equals() #=> 3
> Python version1 - Method Chaining
	# To simplify, only implement the numbers 1 and 2 and the operations "equals" and "plus"
<pre>
	<code>
		class one:
			def __init__(self):
			    self.val = 1

			def plus(self):
			    return plus(self.val)

		class plus:
		    
		    def __init__(self, a):
		        self.a = a
		    
		    def two(self):
		        return two(self.a)

		class two:
		    
		    def __init__(self, val):
		        self.orig = 2
		        self.val = val
		    
		    def equals(self):
		        
		        return self.orig + self.val
	</code>
</pre>
> Python version2 - Message/Method Cascading
<pre>
	<code>
		class number:
			def __init__(self):
				self.val = None

			def one(self):
				return self

			def plus(self):

				return self

			def two(self):

				return self

			def equals(self):

				return 	1 + 2
	</code>
</pre>
> SmallTalk Version - Can we pass blocks while sending messages?


