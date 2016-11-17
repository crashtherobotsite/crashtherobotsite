---
layout: post
title:  "The 6 Kinds of 'Complicated' Software Projects, How They Cost You Money, and Weapons to Fight Back!"
date:   2016-11-17 00:00:00 -0400
categories: uncertainty autonomy testing software
author: AMB
robots_rating: 2
published: false
---

*TL;DR: "Modern software is complicated, but not all complications are the same kind. More importantly, not all complications cost the same amount of time and money when something goes wrong. We break down 6 different kinds of complexity, explain holes in classical coping strategies, and detail what it's going to cost you (as a developer or as a manager) down the line if you don't pick the right weapon for combatting it.*

# Background: The 6 Kinds of Complicated

The customer hates you. The project is already 6 months late.  The manager asks the software engineers "What's wrong?" They get answers like  "It's complicated..." or "The system is old and broken and will take a complete overhaul and 2 million dollars to fix."  Developers work desperately to get something, anything, working, and everyone hates their job. But wait! There's hope!  **Not all giant, late, legacy, broken, horrible projects need the "complete rewrite" to be saved.** Some software projects just need a little love... and targeted investment in better tools. Here are some common reasons behind 'complicated', and how to fix them. 

# 1. Your SOURCE CODE is Enormous

"Every program attempts to expand until it can read mail. Those programs which cannot so expand are replaced by ones which can." -[Zawinski's Law of Software Development](https://en.wikipedia.org/wiki/Software_bloat)

**The Complication**
Two words: legacy system.  What started as a 200 line script to highlight certain words has ballooned into a 50,000 lines-of-code word processor that can launch a space shuttle. The 'lines-of-code' metric has a few variants; some try to take into account operating system code or multiple layers of abstraction that can cause bugs you can't see, but either way, finding a bug will take you days.

**The Cost** 
Most software developers and business managers already know about this one: paid software developer time. The more lines of code your system has, so the thinking goes, the more expensive it will be to fix a problem without breaking something else. In addition, many software engineers would rather spend their time building new features, and managers would rather pay them to do that, so the problem often compounds over time. 

**The Good News**
The good news here is that this problem is completely understood already, and fixable! Basic [coding standards](http://codeahoy.com/2016/05/22/effective-coding-standards/) often capture efficient ways of reading lots of code at a time. Design standards like [modularity](https://netbeans.org/project_downloads/usersguide/rcp-book-ch2.pdf) can make it manageable to look at small, 100 line functions at a time, so that you can see a whole function or method on your screen at once.  Testing modules works well too- write unit tests for each new function/method that you build as you go along. 

So why does "giant legacy source code base" still give every engineer the shivers if (as this author believes) the problem of "lots of code" is so tractable? Most of the time it's because people confuse the *amount* of code with one of these other kinds of complexity. Read on!


#2. Your TOOL CHAIN has more than 2 Steps
**The Complication**

**The Cost** 

**The Good News**
The best news here is that the cost of this problem is so easy to quantify that making a case to pay for a solution to your boss is elementary school math: 
(1 hour build engineer time) << (1 hour developer time)x(number of team members)x(software commits per week that require team to update their code)


#3. Your SPECIAL SAUCE is Not Documented Outside the Code
**The Complication**

**The Cost** 

**The Good News**
This could either be good news or very bad news depending on whether the Special Sauce Engineer is still with your company. If they are, ask them to present a "lunch and learn" about their work. $100 in Pizza will result in a set of slides that should be annotated and archived FOREVER in an easily accessible place. 

If the Special Sauce Engineer is gone from the company, you, newcomer developer, get to host that lunch and learn!  You may have to reverse engineer their work to create the presentation, but *it can be done.* Your company's ROI in this case is the hourly rates of dozens of future engineers who have no idea why your product works.

#4. Your INTERMEDIATE OUTPUTS are Not Human Readable


#5. Your INPUT DATA is Arbitrary  


#6. Your OUTPUT has no Right Answer but lots of Wrong Ones