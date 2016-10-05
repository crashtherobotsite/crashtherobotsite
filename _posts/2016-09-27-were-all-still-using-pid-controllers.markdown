---
layout: post
title:  "Software PID Controllers: If All You Have Is a Hammer..."
date:   2016-09-27 21:10:58 -0400
categories: robots control pid control-theory
author: AMB
published: false
---
*TL;DR: "If all you have is a hammer, everything looks like a nail."  Despite literally hundreds of alternate proposed control schema for different kinds of robots and machines, most engineers and roboticists are still using the 105-year-old PID controller somewhere in their code, tool-chains, and mobile robots. We discuss the strengths and weaknesses of using PID in software, and finish off with some alternatives to the vaunted PID controller.*

# Background: What Is a PID Controller?
*Note to EEs and controls engineers- feel free to skip this section.*

Let's define some terms.  In the engineering discipline of control theory, a  **controller** is a device or design for altering the output of any physical, electrical or mechanical system. A **process** or **plant** is the piece of the system that can't be changed, only reacted to. A plant is usually a model of the physical world: a room to be heated, a boat to steer, an ocean pushing on a submarine.  Control is an attempt to acheive a specific goal given a pre-existing plant: a temperature for the room, a heading for the boat, a depth for a submarine.  A controller may need to hold an output constant even when the input varies, like maintaining a specific temperature in a room even when it's hot or cold outside.  A controller may be implemented  with electrical hardware, with mechanical dampers, with sofware or even some other way. [[1]](https://en.wikipedia.org/wiki/Controller_(control_theory))

{% include ext_image.html url="http://www.controlglobal.com/assets/00_images/2012/1205/CG1205-ATE1.jpg" description="A PID controller implemented completely mechanically." %}

A **Proportional-Integral-Derivative Controller** (PID for short) is common type of controller used to achieve a goal output with [negative feedback](https://en.wikipedia.org/wiki/Negative_feedback). The system measures the error between a desired input and the real output at a given time, performs a calculation and uses this calculation to change its output in hopes of getting closer to its goal.[[2]](https://en.wikipedia.org/wiki/PID_controller).   The calculation used by a PID, as shown in the figure below, is a sum of P, I, and D terms of the controller. 

{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/PID_en.svg/971px-PID_en.svg.png" description="A block diagram of the canonical PID controller." %} 
  
The **proportional** term is of a PID is the error multiplied by a scale factor *Kp*.  *Kp* is the term of the controller that keeps us close to where we want to be: if we measure a small error, we make a small correction, but measuring big error results in a big correction.  For example, let us say that a self-driving car is trying follow a painted line on the ground. The further the car is from the line, the more it should turn its wheels to get back on track quickly.  This is the essence of proportional control. 

The **integral** term of a PID is the sum of the steady-state error of a system over time, multiplied by *Ki*.  Integral control is a coping mechanism for a common problem with proportional control:  in order to apply an output, there has to be an error in the first place to multiply by *Kp*.  In the presence of a plant, we may never actually achieve our goal.   In our car example as we get closer and closer to steering right on the lane-line, our steering changes will get smaller and smaller, until, at some point, they are so small that the constant friction in our car and the road will keep the changes from actually taking place. We will never *actually* achieve our goal of being perfectly aligned in our lane.  This is known as steady-state error, and integral control can make it disappear by accounting for it over time. 
 
A PI controller is often good enough for a steady-state process input- if the marked lane our self-driving care is following is always a straight line, then 2 terms might well be good enough. The **derivative** term of a PID controller becomes most useful when your input changes very quickly.  The derivative term is a scale factor *Kd* multiplied by the calculus derivative (also known as the rate of change or instantaneous slope) of the error.  It biases the controller to react more quickly if an error jumps suddenly.

 In our car example, lets say that the lane markers on the road suddenly jump 1 meter to the left. A PI controller would eventually minimize the error, but the PID controller will do it *faster*: it will add a component to the car's steering equal to (*Kd* * the distance of the lane jump).    It's worth a note that this performance bonus comes with a drawback- if a signal is noisy, (or our lane markers jump around often) the output will be a very bumpy ride as well. 



# Strengths: Why use PID in Software?

PID controllers that were used mechanically to steer boats 100 years ago had to be implemented with physical analogs to integrators, differentiators, and multipliers. Software today is under no such constraints, but PID controllers live on. Why is this? Besides obvious the sheer number of legacy tools available, the PID controller has numerous positive qualities when using software to control an output. 

**If You Need Simplicity**
The three knobs of a PID loop, result in physical effects that, while not independently tunable from each other, are easily explainable. Three knobs on a controller is a manageable number of parameters that can be tuned by hand or by [well-documented, 80 year old processes](https://en.wikipedia.org/wiki/Ziegler%E2%80%93Nichols_method) for a given robot or actuator. Just find a working Kp, Ki, and Kd, and continue on your way through your design. You do, after all, have a robot army that needs building. 

**If You Have Minimal Code Size and Memory**
The basic digital PID controller is *very small* in code size and memory. A [basic, discrete-time implementation](https://github.com/ivmech/ivPID/blob/master/PID.py) stores 1 input, 4 scale factors, 3 ongoing values, and takes about 10 lines of psudeo-code: 

```python
#State Variables: last_error, error_sum, last_output
#Fixed Constants: Kp, Ki, Kd, dT

def calc_next_step_PID (sensor_input):
	#Calculate new output
	error = last_output - sensor_input
	error_sum += error*dT
	new_output = Kp * error + Ki * error_sum + Kd * (error - last_error)/dT

	#Update for next time
	last_error = error
	last_ouput = new_ouput

	return new_output

while True:
	sensor_input = read_sensor()
	new_output = calc_next_step_PID(sensor_input)
	set_output(new_output)
	wait(dT) #Discrete time span dT replaces continuous time integral.
```

And that's it. A PID controller is small, fast, and cheap in code space, great for microcontrollers, PLCs, and other tiny, tiny spaces. It's hard to beat in many situations, especially when you don't know what else might be part of your design later on. 


**If You Can't Model What You're Controlling... but it's LTI**
A PID controller is an good choice if the output variable that is under control is not easily modeled, but the system characteristics will not change over time. The numeric theory around PID controllers uses a model of the world as a [linear, time-invariant system](https://en.wikipedia.org/wiki/LTI_system_theory). 

Controller *input* can vary with time, but in a PID world, any other parameters that are part of the "plant" are modeled as unchanging. For our self-driving car example, that means that the line markers we're using on the road as input can vary as much as we like, but the mass of the car needs to stay the same. If we can model the car mass as unchanging (or not changing enough to affect our result), then a PID controller will likely be a good choice for our self-driving car.


# Weaknesses: When You Should NOT Use PID Control

**When Your System is Not Linear and Not Time Invariant**
PID controllers exist in a [mathematical world](https://en.wikipedia.org/wiki/LTI_system_theory) where the plant of a system does not change over time. This is never true in the physical world, but most systems change slowly enough that using the assumption of constant properties doesn't hurt our controller. For example, electrical elements like resistors, inductors, and capacitors often wear out slowly enough that their physical properties can be modeled as unchanging. However, there are systems where that assumption just [can't be made](https://en.wikipedia.org/wiki/Time-variant_system), and PID controllers fail *hard* in these cases.

Let's say our self-driving car is carrying a massive liquid fuel tank, and that this tank gets used up as we drive. If we modeled our plant physics with the car carrying an empty tank, we would choose a set of parameters to get the best result for our controller. But, if we modeled the car than we would choose using a full tank. We might even have to set our Kp, Ki, and Kd terms at full, and then again at mid-tank, and then again at empty, manually. If constant re-tuning is necessary for your robot actuator under PID, then more knowledge and design need to be added to the controller for any useful automation to happen. Constant re-tuning often makes a PID controller more trouble than it's worth.

**When You Have Lots of System Knowledge**
Better control can often be acheived by using what you know about a plant. If I know that commanding a certain voltage to a servo under a specific load will result in the servo moving to a certain position, I don't have to attach a sensor to the servo for feedback. I can just command the voltage. I could even create a calibration table for different voltages vs position for different servo loads.  This is an example of [feed forward control](https://en.wikipedia.org/wiki/Feed_forward_(control))because I'm commanding my servo based on information I know about it, not measuring it in real time.  Feed forward control is commonly used *with* PID control to improve results. 

{% include ext_image.html url="https://en.wikipedia.org/wiki/File:FeedForward.png" description="Feed forward and Feed back control combined in one system." %}



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
http://machinedesign.com/sensors/introduction-pid-control
http://robotsforroboticists.com/pid-control/
