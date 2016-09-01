
---
layout: post
title:  "10 Unintentional Killer Robots"
date:   2016-08-31 18:14:00 -0400
categories: ai safety fatalities da-vinci
author: AMB
---
*TL;DR: 10 unintentionally fatal robots from the 1980s through today provide a glimpse of the safety challenges that all engineers face, but also highlight safety challenges unique to AI and robots. All engineers have to worry about broken components, material wear, human interactions, realistic testing, and potential product misuse. Roboticists have to worry about additional factors such as invisibile complexity, unproveable safety factors, expectations based on Hollywood, and others.*


Killer Robots. The stuff of Hollywood legends, most killer robots are designed that way on purpose- gun turrets, lasers, red LED eyes. Generally, they look like this: 

<img src="http://vignette2.wikia.nocookie.net/terminator/images/1/19/Terminator_robot.jpg/revision/latest?cb=20090512155233" alt="Fatal Hollywood Robot"  height="200" />
*T-850, Fatal Hollywood Robot*

Much less entertaining are robots in the real world that kill, not by design, but by accident. As a public service announcement, robots that kill you accidentally look like this:

![Fatal Real World Robot](https://hci.cs.siue.edu/NSF/Files/Semester/Week13-2/PPT-Text/images/Image3.png)
 *Therac-25, Fatal Real World Robot*

This list covers the top 10 most-accidentally-fatal robots of the modern era. To make the list, the fatality had to be due specifically to a "robotic" or "AI" feature. While there is no perfect definition for [what counts as a robot and what doesn't](http://www.crashtherobot.com/toys/robots/science-fiction/roomba/irobot/2016/07/14/your-robot-should-be-cute-and-needy.html), I've used the general definition that if an electro-mechanical device *senses* any part of the physical world,  *makes a decision* based on input data,  and *actuates* the resulting output, then it qualifies as a robot. If it *accidentally kills someone in the process*, it qualifies for our list. 

## 1. Therac-25 (1985-1987)
Topping our list is the Therac-25, one of the most infamous case studies in medical device design gone wrong. The Therac-25 was a multi-mode radiation therapy device designed to treat different kinds of cancer. Its software, reused from an older model, contained  bugs that led to the wrong kind of radiation being applied to patients, causing at least 4 deaths and several additional severe radiation burns. The Therac-25 makes our list for two reasons, one technical and one human. 

Technologically, [one of the root causes](https://en.wikipedia.org/wiki/Therac-25#Root_causes)  of the fatalities was a race condition due to concurrent programming errors: the machine needed a specific amount of time to switch modes when an operator entered a command sequence. In the lab, no operator had ever entered the sequence *fast enough* to cause the error. In a perverse twist of fate, it took several months of real life operation before *experienced technicians* could use the console fast enough to cause the problem.  The second reason the Therac-25 became a classic case study is a combination of human frailty and human arrogance.  Because the Therac-25 treated patients already dying of cancer, and because the company had sent out advertisments for the machine claiming it was 5 orders safer than previously working models, [two people died](http://www.ccnr.org/fatal_dose.html) before anyone even *thought* to blame the software. 
	
The fallout from the Therac-25 radiation disaster caused the FDA to issue the first laws [requiring hospitals to report errors with medical devices to the FDA and the manufacturer](https://computingcases.org/case_materials/therac/case_history/Case%20History.html) in an effort to close the information loop when something goes wrong. The idea is that even if a dangerous medical device gets on the market, a single failure should tip everyone in the country off to the danger.  We're smarter now, right? Which brings us to....


##2. The Da Vinci Surgical System (2000-present)
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/23/Cmglee_Cambridge_Science_Festival_2015_da_Vinci.jpg/1280px-Cmglee_Cambridge_Science_Festival_2015_da_Vinci.jpg" alt="Fatal Hollywood Robot"  height="200" />
*The Da Vinci Surgical System, Potentially Fatal Real-World Robot*

Surgery robots were linked to [144 deaths between 2000 and 2013](http://arxiv.org/ftp/arxiv/papers/1507/1507.03518.pdf) according to a recent paper. The authors of the study raise a growing concern in the medical world: *Are robots really safer surgeons, or is the human desire for a shiny new toy and a more billable surgery procedure actually making people less safe?* 

While it is not completely fair to single out Intuitive Surgical's da Vinci system for all of those deaths, the daVinci system is a marketing-juggernaut household name that deserves the singling out. In fact, [medical researchers worry](http://jama.jamanetwork.com/article.aspx?articleid=1700496)  that:  

*"Aggressive direct-to-consumer marketing and incentives associated with fee-for-service payment may promote the use of these advanced treatment technologies."*

At least [one group of doctors](http://www.acog.org/About-ACOG/News-Room/News-Releases/2013/Statement-on-Robotic-Surgery) is very disappointed in the effects that marketing robots directly to patients could have on their health as well: 

*"Aggressive direct-to-consumer marketing of the latest medical technologies may mislead the public into believing that they are the best choice."*

The expectations set for these robots are that they can perform better than human surgeons, or with less skilled operators behind the controls, and that has not proven conclusively true so far.  While the jury is still out, blanket trust in robot surgeons should not be part of any techno-futurist's arsenal. 









