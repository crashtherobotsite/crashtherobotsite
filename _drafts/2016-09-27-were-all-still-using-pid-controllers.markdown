---
layout: post
title:  "Give up the Security Blanket! PID Controller Alternatives."
date:   2016-09-27 21:10:58 -0400
categories: robots control pid control-theory
author: AMB
published: false
---
*TL;DR: Despite literally hundreds of alternate proposed control schema for different kinds of robots and machines, most engineers and roboticists are still using the PID controller somewhere in their code, tool-chain, and mobile robots. We discuss the strengths, weaknesses, and alternatives to the vaunted PID controller.*  

# What Is a PID Controller?
1. Define the PROBLEM: Feedback
2. Define the Terms (Closed loop, QUICK intro and links to time/frequency domain transformation math tutorials). 
3. Example with plots

# Strengths: Why we're still using the PID
1. "Understand"-ability
2. Cheap in time and memory. 
2. Ease of Implementation in digital form.
2. Theoretical best case in absence of other information.
3. Lack of Free (As in Speech and Beer), Properly Implemented Software Alternatives

# Weaknesses: Why we shouldn't ALL still be using the PID

*"As much as three-fourths of annual power consumption in some distribution systems can be attributed solely to PID-control losses."*
		 -Thomas Harman, ['PID Control: May It Rest in Peace'](http://www.hartmanco.com/pdf/a37.pdf)

1.  When all you have is a hammer: When you shouldn't be using it AT ALL. (Open loop, slow sampling, knowing your system parameters, etc).
2. When you've added Feed forward and clamps and a million other things, it's not really PID anymore. (http://www.eng-tips.com/viewthread.cfm?qid=228364) - It's not 'designed', it's 'sculpted'- and VERY hard to model in MATLAB...
3. Theoretical limit to usefulness. 
2.  Let's talk about tuning. Seriously. 
3.  Theoretical Weaknesses when cascaded: PID controllers 'fighting' each other 
4.  Practical weaknesses when cascaded

# Alternatives: Giving up the Blanket
SIMPLER
1. The Bang Bang controller.  You may be adding in complexity and getting nothing out. 
MORE COMPLICATED 
2. Model Predictive Control (http://www.automation.com/automation-news/article/addressing-the-myths-of-model-predictive-control-mpc) 
3. 
2. Interdependent Network Control (http://www.hartmanco.com/pdf/a37.pdf)  for HVAC buildings, valves, water mains... but also robots controlled by hydraulics, and cascaded controllers where "modular" isn't really what you want. (http://hpac.com/bas-controls/Replace_PID_Relational_Control)
	4. "Think of the loads in a distribution system as clients and the pump or fan as a server interconnected through a network." 

DIFFERENT PHYSICS 
3. Pulsed Error
4. Psuedo-derivative controller http://www.openservo.com/forums/viewtopic.php?t=24  http://users.erols.com/jyavins/servo.html
5 PI+FF . http://www.openservo.com/VelocityControl
4. Fuzzy Logic 
	3. 
 
PICTURE: Flow chart 

# Resources
https://en.wikipedia.org/wiki/PID_controller
http://www.controlglobal.com/articles/2005/493/


