---
layout:     post
title:      2020-09-17-Google Sheet/Excel CP01 - WeekDay
subtitle:   Google Sheet Functions
date:       2020-09-17
author:     Elon
header-img: img/post-bg-sheet.png
catalog: true
tags:
    - Basketball
---
## Weekday function with examples

### Syntax
	Weekday(date, [type])
- date: the date to be converted
- type: this argument is optional which allows you to start your weekday numbering from either Sunday or Monday.
	* if you use 1(by default), the weekday starts from Sunday, where Sunday is given value 1.
	* if you use 2, the weekday will start from Monday, where Monday is given value 1.
	* if you use 3, the weekday starts from Monday, but Monday is given value 0

For example, you can use Weekday("9/15/2020"), or Weekday("9/15/2020", 2) or you can reference the date from a cell. 
### Reference a cell of date
	weekday(A2)

### Combined with Date function
	weekday(Date(2020, 9, 15), 2)
### Find out a specific name for the date cell
Sometimes, we might still want to know Mon, Tue, Wed(周一，周二，周三，...)， in this case, we can combine **CHOOSE** function to get the right name.

	Choose(Weekday("9/15/2020"), 2), "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun")

### Find out if XX/01/CCYY is the first Monday of the Month
	=IF((WEEKDAY(DATE(2020,9,1),2))>1,DATE(2020,9,1)+7-(WEEKDAY(DATE(2020,9,1),2))+1,DATE(2020,9,1))