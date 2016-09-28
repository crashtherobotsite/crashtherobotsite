---
layout: post
title:  "Give up the Security Blanket! PID Controller Alternatives for Software."
date:   2016-09-27 21:10:58 -0400
categories: robots control pid control-theory
author: AMB
published: false
---
*TL;DR: Despite literally hundreds of alternate proposed control schema for different kinds of robots and machines, most engineers and roboticists are still using the PID controller somewhere in their code, tool-chain, and mobile robots. We discuss the strengths, weaknesses, and alternatives to the vaunted PID controller.*  

# Background: What Is a PID Controller?
*Note to EE and controls engineers- feel free to skip this section.*

Let's define some terms.  In the engineering discipline of control theory, a  **controller** is a device or design for altering the output of any physical, electrical or mechanical system. A **process** or **plant** is the piece of the system that can't be changed, only reacted to. Control is an attempt to acheive a specific goal given a pre-existing process.  An example goal of a controller is to hold an output constant even when the input varies, like maintaining a specific temperature in a room even when it's hot or cold outside.  A controller may be implemented physically with hardware, with mechanical dampers, with sofware or even some other way. [[1]](https://en.wikipedia.org/wiki/Controller_(control_theory))  

{% include ext_image.html url="http://www.controlglobal.com/assets/00_images/2012/1205/CG1205-ATE1.jpg" description="A PID controller implemented completely mechanically."}

A **Proportional-Integral-Derivative Controller** (PID for short) is common type of controller used to achieve a goal output with [negative feedback](https://en.wikipedia.org/wiki/Negative_feedback). The system measures the error between a desired input and the real output at a given time, performs a calculation and uses this calculation to change its output in hopes of getting closer to its goal.[[2]](https://en.wikipedia.org/wiki/PID_controller).   The calculation used by a PID, as shown in the figure below, is a sum of the three terms. 

{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/PID_en.svg/971px-PID_en.svg.png" description="A block diagram of the canonical PID controller." %} 
  
The **proportional** term is of a PID is the error multiplied by a scale factor *Kp*.  *Kp* is the term of the controller that keeps us close to where we want to be: if we measure a small error, we make a small correction, but measuring big error results in a big correction.  For example, let us say that a self-driving car is trying follow a lane-marked line on the ground. The further the car is from the lane line, the more it should turn its wheels to get back on track quickly.  This is the essence of proportional control. 

The **integral** term of a PID is the sum of the steady-state error of a system over time, multiplied by *Ki*.  Integral control is a coping mechanism for a common problem with proportional control:  in order to apply an output, there has to be an error in the first place to multiply by *Kp*.  In the presence of a plant, we may never actually achieve our goal.   In our car example as we get closer and closer to steering right on the lane-line, our steering changes will get smaller and smaller, until, at some point, they are so small that the constant friction in our car and the road will keep the changes from actually taking place. We will never *actually* achieve our goal of being perfectly aligned in our lane.  This is known as steady-state error, and integral control can make it disappear by accounting for it over time. 
 
A PI controller is often good enough for a steady-state process input- if the marked lane our self-driving care is following is always a straight line, then 2 terms might well be good enough. The **derivative** term of a PID controller becomes most useful when your input changes very quickly.  The derivative term is a scale factor *Kd* multiplied by the calculus derivative (also known as the rate of change or instantaneous slope) of the error.  It biases the controller to react more quickly if an error jumps suddenly.

 In our car example, lets say that the lane markers on the road suddenly jump 4 feet to the left. A PI controller would eventually minimize the error, but the PID controller will do it *faster*: it will add a component to the car's steering equal to (*Kd* * the distance of the lane jump).    It's worth a note that this performance bonus comes with a drawback- if a signal is noisy, (or our lane markers jump alot) the output will be a very bumpy ride as well. 



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
http://www.controlglobal.com/articles/2012/liptak-tuning-interacting-controllers/
http://www.ni.com/white-paper/3782/en/
