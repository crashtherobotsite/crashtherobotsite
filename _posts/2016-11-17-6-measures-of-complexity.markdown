---
layout: post
title:  "3 Kinds of 'Complicated' Software Projects, How They Cost You Money, and Tools to Fight Back"
date:   2016-11-17 00:00:00 -0400
categories: uncertainty autonomy testing software
author: AMB
robots_rating: 1
published: false
---

*TL;DR: "Modern software is complicated, but not all complications are the same. More importantly, not all complications cost the same amount of time and money when something goes wrong. We break down 3 different kinds of complexity, explain coping strategies, and detail what it's going to cost you (as a developer or as a manager) down the line if you don't pick the right weapon for combatting your specific problems.*

# Assumptions 
This article assumes your team has the following things already: 
    - A halfway-decent [customer specification](). Because complications from what people want cannot be solved with software tools.  
    - At least one software engineer. Because software tools are useless if nobody actually uses them.
    - [Source control]. Because it's 2016. 

If your team is missing these things, you need to look elsewhere for [stronger medicine](Joel Spolsky essay). 

# Background: 'It's Complicated'

The customer hates you. The project is already 6 months late.  The manager asks the software engineers "What's wrong?" She/he gets answers like  "It's complicated..." or "The system is old and broken and will take a complete overhaul and 1 MILLION (or BILLION) dollars to fix."  Developers work desperately to get something, anything, working, and everyone hates their job. But wait! There's hope!  **Not all giant, late, legacy, broken, horrible projects need a "complete rewrite" to save them.** Some complicated software projects just need a little love... and disciplined, targeted investment in better tools. Here are some common, real-life reasons behind 'complicated', and how to cope with them. 


# 1. Your CODE BASE is Enormous

>"Every program attempts to expand until it can read mail. Those programs which cannot so expand are replaced by ones which can." -[Zawinski's Law of Software Development](http://softwareengineering.stackexchange.com/questions/150254/what-does-jamie-zawinskis-law-mean)

**The Complication**

What started as a 200 line script to highlight certain words has ballooned into a 50,000 lines-of-code word processor that can launch a space shuttle while Tweeting about your startup culture. Any request from a customer will take a year to implement, even though your development team has 50 people on it.   You probably have some metric of how large your source code is- in numbers of files, lines of code, or how long it takes to download from source control. Either way, finding a bug will take you days.

**The Cost** 
Most software developers and business managers already know about the number one cost of a system with thousands of lines of source code: paid software developer time. The more lines of code your system has, so the thinking goes, the more expensive it will be to fix a problem without breaking something else. In addition, many software engineers would rather spend their time building new features than reading old code, and customers would rather pay them to do that, so the problem often compounds over time. 

**How to Fix it On A Budget**
a.[Coding Standards](http://codeahoy.com/2016/05/22/effective-coding-standards/) capture efficient ways of reading lots of code at a time. Design standards like [modularity](https://netbeans.org/project_downloads/usersguide/rcp-book-ch2.pdf) can make it manageable to look at small, 100 line functions at a time, so that you can see a whole function or method on your screen at once.  

Coding standards are free in money, but not in time or social cost:
If you already *have* a giant legacy system, your most sensible path forward is still coding standards- but implement them as you go along instead of making your team spend time modifying your whole codebase. Stick to a solid rule: no *new* code or *changes* to old files go into the software without following your standards. If you have to make smaller classes, so be it.  

b. [Indexed Source Code Search Tools] make looking through all that code *fast*. If it takes a developer 30 minutes to find a file, that is wasted time. Throwing a little money at this problem goes a long way- good IDEs often provide this functionality as part of them. 

c. [Remove dead code with Static Analysis]. The odds are good that your code base has more than 2 string formatting libraries. One of the is probably not even used. Static analysis tools like [Lint]() and [python zombie code]() can find dead code and dependencies so that you aren't looking through code that isn't even used. 


#2. Your END TO END BUILD PROCESS has more than 1 Step. 
**The Complication**
A trial customer finds a critical bug that must be patched within a week or they will refuse to pay you. Developers fix the bug, only to find that they have *no way* of patching the bug fix (and only the bug fix) into the customer's code- the customer's software executable was from a special version on Carla's computer, and she's on vacation in Japan.  

If this is you, your source code is not the problem: how you ship it is.  

**The Cost** 
The cost of this problem is death by ten thousand paper cuts. Some examples:  

If there is no source control copy that *exactly matches* your deployed server or executable, each engineer spends extra time on every bug trying to figure out whether the latest code they are looking at even *has* a certain problem. 

If it takes an engineer a day to build the shipping code (instead of an automated process), that's a day lost at every critical transfer stage- development to test, test to beta, beta to shipping, and one for every patch too.   

If every team member can't build the code *the exact same way* and get the same output, opportunities for more bugs are introduced in the mismatch. 

If an engineer can't build a whole product before committing code, bugs that could have been caught early on won't be caught until later in the process, costing money.

The papercuts are endless. 


**How to Fix it On A Budget**
a. First, get the most out of your existing [Build Tools].  If you use 
[make]() or [automake](), consider adding pre and post build hooks for building a shipping executable that work for all your developers. If you deploy code to servers, all your developers should be running a [Docker]() or local server of your code that *matches what you would ship to customers*. 

b. [Automated Builds]. Once you have code that can be built by computer, you should make a computer build the code all the time. Source control hooks to kick off automated builds are really not optional in 2016. You can tie it into a manual process, but there are also lots of tools to help you out: [Jenkins], ....


#3. Your SPECIAL SAUCE is Not Documented Outside the Code
**The Complication**
Your software does something special or intelligent, like recommends movies, trades stocks, or searches the entire Internet for baby armadillo photos using a secret algorithm.  And only 1 person knows how it works. And maybe they just quit. Since everyone is afraid of breaking the magical secret sauce, any change to any part of the code requires going through the Special Sauce Engineer.

**The Cost** 
If your Special Sauce Engineer quits, their replacement is going to have to reverse engineer all the code (and the undocumented design that went with it) for your company to survive. If your Special Sauce Engineer stays, at some point they will want to invent something else or get promoted- leaving the sustaining engineering team with the same problem. Meanwhile, *all the other smart, expensive engineers on the team are afraid to innovate.*  More heads are better than one, but only if they are actually able to contribute useful work. 

**How to Fix it On A Budget**
a.  Pizza! Seriously! If the Special Sauce Engineer is still with your company ask them to present a "lunch and learn" series about their work. $100 in Pizza and a cell phone video recording will result in a set of slides that should be annotated and archived FOREVER in an easily accessible place for the whole team. Once there, it should be required viewing for new hires. If the engineer protests or claims it's too complicated, send them this cartoon:

(xkcd cartoon of teaching)

It's important that the Special Sauce presentations are *really* about the Special Sauce. They should *not* be about the spaghetti code implementation of the Special Sauce. If your product is a movie recommendation algorithm that uses linear regression, then the talk should be about linear regression, not about the 15 Python libraries, the GUI, and the OpenCV binding used to build the prototype. ss  

b. External experts. If the Special Sauce Engineer is gone from the company and cannot be persuaded to return to give a (paid) set of talks, you still need the base knowledge of that Special Sauce to permeate through your team, and you should pay an expert for a 3-6 set of weekly lunches. If nothing else, it will tell your team what to Google as they reverse engineer the code. 


