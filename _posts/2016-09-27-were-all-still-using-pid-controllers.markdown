---
layout: post
title:  "Software PID Controllers: If All You Have Is a Hammer..."
date:   2016-09-27 21:10:58 -0400
categories: robots control pid control-theory
author: AMB
published: true
robots_rating: 3
---
*TL;DR: "If all you have is a hammer, everything looks like a nail."  Despite hundreds of alternate proposed control schema for different kinds of robots and machines, most engineers and roboticists are still using the 105-year-old PID controller somewhere in their code, tool-chains, and mobile robots. We explain the strengths and weaknesses of using the analog-based PID in digital software.*

# Background: What Is a PID Controller?
*Note to EEs and controls engineers- feel free to skip this section.*

Let's define some terms.  In the engineering discipline of control theory, a  **controller** is a device or design for altering the output of any physical, electrical or mechanical system. A **process** or **plant** is the piece of the system that can't be changed, only reacted to. A plant is usually a model of the physical world: a room to be heated, a boat to steer, an ocean pushing on a submarine.  Control is an attempt to achieve a specific goal given a specific plant: a temperature for the room, a heading for the boat, a depth for a submarine.  A controller may need to hold an output constant even when the input varies, like maintaining a specific temperature in a room even when the room has lots of people in it producing heat.  A controller may be implemented  with electrical hardware, with mechanical dampers, with sofware or even some other way. [[1]](https://en.wikipedia.org/wiki/Controller_(control_theory))

{% include ext_image.html url="http://www.controlglobal.com/assets/00_images/2012/1205/CG1205-ATE1.jpg" description="A PID controller implemented completely mechanically." %}

A **Proportional-Integral-Derivative Controller** (PID for short) is common type of controller used to achieve a goal output with [negative feedback](https://en.wikipedia.org/wiki/Negative_feedback). The system measures the error *e(t)* between a desired input and the real output at a given time, performs a calculation and uses this calculation to change its output in hopes of getting closer to its goal.[[2]](https://en.wikipedia.org/wiki/PID_controller).   The calculation used by a PID, as shown in the figure below, is a sum of P, I, and D terms of the controller. 

{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/PID_en.svg/971px-PID_en.svg.png" description="A block diagram of the canonical PID controller." %} 
  
The **proportional** term is of a PID is the error *e(t)* times a scale factor *Kp*.  '*Kp*e(t)*' is the term of the controller that keeps us close to where we want to be: if we measure a small error, we make a small correction, but measuring big error results in a big correction.  Take as an example a self-driving car trying follow a painted line on the ground. The further the car is from the line, the more it should turn its wheels to get back on track quickly.  This is the essence of proportional control. 

The **integral** term of a PID is the sum of the error of a system over time, multiplied by *Ki*.  Integral control is a coping mechanism for a common problem with proportional control:  in order to apply an output = *Kp * e(t)*,  we must have an error in the first place.  In the presence of a plant, we may never actually achieve our goal of no error. To illustrate this, consider again our self-driving car on a road that isn't perfectly level.   As we get closer and closer to being perfectly on top of the desired lane-line, our steering changes will get smaller and smaller, until, at some point, they are so small that the slope of the road will balance out the amount of change we're making.  We're close to the lane marker, so we won't add more output, but we will never *actually* achieve our goal of being perfectly aligned in our lane. Instead, we'll always be the tiniest bit off as our steering wheel fights with the slope of the road. This is known as **steady-state error**, and integral control can make it disappear by accounting for it over time. 
 
A PI controller is often good enough for a steady-state process input: if the marked lane our self-driving care is following is always a straight line, then 2 terms might well be good enough. The **derivative** term of a PID controller becomes most useful when your input changes very quickly.  The derivative term is a scale factor *Kd* multiplied by the calculus derivative (also known as the rate of change or instantaneous slope) of the error.  It biases the controller to react more quickly if an error jumps suddenly.

 Once more using our self-driving car example, let's say that the lane markers on the road suddenly jump 1 meter to the left. A PI controller would eventually minimize the error, but the PID controller will do it *faster*. It will add a component to the car's steering equal to (*Kd* * the distance of the lane jump).    It's worth a note that this performance bonus comes with a drawback- if a signal is noisy, (or our lane markers jump around often) the output will be a very bumpy ride as well. 



# Strengths: Why use PID in Software?

PID controllers that were used mechanically to steer boats 100 years ago had to be implemented with physical components that accomplished the mathematical tasks of integrators, differentiators, and multipliers.  Certain mathematical operations were off the table if they didn't have a way of being physically implemented, or if the mechanical cogs and gears needed weighed too much for their task.  Software today is under no such constraints, but PID controllers live on. Why is this? Besides just the sheer number of legacy tools and software libraries available, the PID controller has numerous advantages for a software engineer.

**If You Need Simplicity**
The three knobs of a PID loop, result in physical effects that, while not independently tunable from each other, are easily explainable. Three knobs on a controller is a manageable number of parameters that can be tuned by hand or by [well-documented, 80 year old processes](https://en.wikipedia.org/wiki/Ziegler%E2%80%93Nichols_method) for a given robot or actuator. Just find a working Kp, Ki, and Kd, and continue on your way through your design. You do, after all, have a robot army that needs building. 

**If You Have Minimal Code Size and Memory**
The basic digital PID controller is *very small* in code size and memory. A [basic, discrete-time implementation](https://github.com/ivmech/ivPID/blob/master/PID.py) stores 1 input, 4 scale factors, 3 ongoing values, and takes about 10 lines of code: 

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
	#In software, Discrete time step dT models real time passing:
	wait(dT)  
```

And that's it. A PID controller is small, fast, and cheap in code space, great for microcontrollers, PLCs, FPGAs and other tiny, tiny spaces. It's hard to beat in many situations, especially when you don't know what else might be part of your design later on. 


**If You Can't Model What You're Controlling... but it's unchanging**
A PID controller is an good choice if the output variable that is under control is not easily modeled, but the system characteristics will not change over time. The numeric theory around PID controllers uses a model of the world as a [linear, time-invariant system](https://en.wikipedia.org/wiki/LTI_system_theory). 

Controller *input* can vary with time, but in a PID world, any other physical parameters that are part of the "plant" are modeled as unchanging. For our self-driving car example, that means that the line markers we're using on the road as input can vary as much as we like, but the mass of the car needs to stay the same. If we can model the car mass as unchanging (or not changing enough to affect our result), then a PID controller will likely be a good choice for our self-driving car.


# Weaknesses: When You Should NOT Use PID Control

**When Your System is Not Time Invariant**
PID controllers exist in a [mathematical world](https://en.wikipedia.org/wiki/LTI_system_theory) where the plant of a system is **time invariant**.   The system response *does not change* over time.  If we set our oven to 300 degrees,  the oven had better produce the same amount of heat no matter what time of day we are baking cookies (notice I said nothing about whether the oven is actually at 300 degrees...). 

Time Invariance is *almost never actually true* in the physical world, but most systems change slowly enough that using the assumption of constant properties doesn't hurt our controller. For example, electrical elements like resistors, inductors, and capacitors often wear out slowly enough that their physical properties can be modeled as unchanging. However, there are systems where that assumption just [can't be made](https://en.wikipedia.org/wiki/Time-variant_system), and PID controllers fail *hard* in these cases.

Let's say our self-driving car is carrying a massive liquid fuel tank, and that this tank gets used up as we drive. If we modeled our plant physics with the car carrying an empty tank, we would tune our K values to get the best result for our controller. But, if we modeled the car as having a heavy full tank of gas, then we might want *different* K values. We might even have to set our Kp, Ki, and Kd terms at full tank, half tank, and then again at empty, manually. If constant re-tuning is necessary, then more knowledge and design need to be added to the controller for any useful automation to happen. Constant re-tuning to account for changes often makes a PID controller more trouble than it is worth.

**When Your System is Not Modeleable as Linear**
In control theory, a  **linear system** satisfies a [mathematical definition](https://en.wikipedia.org/wiki/Linear_system#Definition) with a property that you as a software engineer ignore at your own peril: [superposition](https://en.wikipedia.org/wiki/Superposition_principle).  As MIT's [Larry Hardesty](http://news.mit.edu/2010/explained-linear-0226) explains it:  

> Suppose that, without much effort, you can toss a tennis ball at about 20 miles per hour. Now suppose that you’re riding a bicycle at 10 miles per hour and toss a tennis ball straight ahead. The ball will travel forward at 30 miles per hour. Linearity is, essentially, the idea that combining two inputs — like the velocity of your arm and the velocity of the bike — will yield the sum of their respective outputs — the velocity of the ball.

 If this isn't true of the inputs and outputs of your system,  then a PID controller will malfunction trying to *make* your system produce a specific output.   Let's extend this principle in our self-driving car "lane marker" example: 
 
1.  If I turn the steering wheel on the car 90 degrees (x1) , the car wheels turn 5 degrees (output F(x1)). 
2.  If I later turn the steering wheel on the car -90 degrees (x2), the car wheels turn -5 degrees (output F(x2)). 
3.  Superposition says that if I turn steering  wheel 0 degrees, then the car wheels will turn 0 degrees as well:  F(90 - 90) = 0 = F(90) + F(-90) 

This principal matches classical physics well: it certainly makes sense to anyone who has ever tried to steer a car in a straight line. But there is a common software case where this logic fails:  *when your only available outputs and inputs are digital states*.  

The base case sounds silly: you wouldn't make a PID controller flip a light switch on or off.  However, software engineers can get tripped up if they forget that *everything* is digital in software.  Imagine I've hooked a software controller up to a servo using an Arduino. I can command values between 1 and 10 for servo position. I might want the value "5.5" to steer my servo, but I can't command that value. My hardware does not allow it.  This happens all the time.  If I implement a pure PID controller, it will constantly be switching between 5 and 6, and the physical controller will vibrate.  A different kind of controller that deals better with discretization error [might get around this problem](https://learn.sparkfun.com/tutorials/pulse-width-modulation), but a pure PID controller can't solve it.   The lesson for software engineers is to be aware of the control effects of discretization error at every level of your system- not just the part you're responsible for. 


**When You Have Documented System Knowledge**
Better control can often be achieved by using what you know about a plant. If I know that commanding a certain voltage to a servo under a specific load will result in the servo moving to a certain position, I don't have to attach a sensor to the servo for feedback. I don't have to buy a sensor at all!  I can just command the voltage. I could even create a calibration table for different voltages vs position for different servo loads.   This is an example of [feed forward control](https://en.wikipedia.org/wiki/Feed_forward_(control)), because I'm commanding my servo based on information I know about it, not measuring it in real time.  

Feed forward control is commonly used *with* PID control to improve results. Ignoring feed forward control when programming for a specific application is 'leaving money on the table': your specific water tank or robot or electrical component probably comes with a datasheet that could give you a better controller, but if you don't include that information, your results will be less than optimal. 

{% include ext_image.html url="https://en.wikipedia.org/wiki/File:FeedForward.png" description="Feed forward and Feed back control combined in one system." %}


# Resources
[Linear vs Nonlinear System Examples](http://www.dspguide.com/ch5/4.htm)
[PID Control and Feed Forward Control Together](http://www.openservo.com/VelocityControl)
[Tuning A PID Controller](http://www.controlglobal.com/articles/2012/liptak-tuning-interacting-controllers/)
[More on PID Control](http://robotsforroboticists.com/pid-control/)

