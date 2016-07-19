---
layout: post
title:  "What the Tesla Autopilot Fatality Can Teach Us About Testing Robots"
date:   2016-07-18 21:10:58 -0400
categories: tesla robots self-driving-cars autonomy testing government-policy
author: AMB
---


On May 7 2016, a motorist named Joshua Brown became the first traffic fatality in an incident involving the Tesla Model S "Autopilot" feature. While not a true autopilot, Tesla touted the ambitiously-named feature as a landmark step towards self-driving cars.  By accounts presently available from Tesla, the system did not explicitly malfunction during the accident. At time of writing, this accident is not a case of broken equipment, dead batteries, or backed-out screws. Instead, the Tesla Model S Autopilot system failed to live up to the expectations of the driver, prompting new questions about how to best design technology to work with the humans we want the technology to keep safe. 

The problem is not hopeless.  It is true that the failure of technology to live up to expectations is a kind of safety problem that we (and by "we" I mean academics, roboticists, engineers, entreprenuers, techno-futurists, lawmakers, public safety officials, and anyone who ever hopes to own a self-driving car) aren't equipped to deal with yet. However, now that the initial media frenzy has died down, along with the more abstract philosophical arguments about whether to blame the technology for doing as it's programmed or the humans who make the roads unsafe or the driver for having the wrong expectations from the system, I think it's time to ask two important questions: "How did this event happen?" and "How can we keep it from ever happening again?" (Spoiler: the answers are not so easy as to be immediately solved in a blog post). 

How did this crash happen? We do not have full technical details yet. Tesla submitted crash report details to the U.S. National Highway Traffic Safety Administration (https://www.teslamotors.com/blog/tragic-loss), which is still in the process of investigating the crash at the time of writing.  The main available facts at present are: 

	1. A high-riding, white tractor trailer pulled across the highway perpendicular to the Model S. The Tesla Model S drove or slid completely underneath the trailer, shearing off the roof of the Model S. The Model S continued moving after it came out the other side of the trailer, veered off the highway, and crashed into a fence post. (http://electrek.co/2016/07/01/understanding-fatal-tesla-accident-autopilot-nhtsa-probe/)
	
	2. Tesla's "Autopilot" was active, but the camera-based visual detection system did not detect the white tractor trailer against a bright sky in time to stop the car. Neither did the driver.
	
	3. The Model S is also equipped with low-pointing, front facing [ultrasonic sensors](https://forums.teslamotors.com/forum/forums/model-s-will-be-able-autosteer-will-require-more-sensors-semiautonomous-driving) that could not detect a potential collision because they pointed underneath the tractor trailer.  According to Elon Musk, this is because pointing the sensors higher presents false positives when bouncing off highway signs (https://twitter.com/elonmusk/status/748625979271045121). The specs available from the Model S website also only give the sensors a range of 16 feet.

Leaving aside Tesla's numerous warnings about how Autopilot is in beta and should not be used as a replacement for safe and attentive driving, the incident is still a technological system failure that demonstrates some of the challenges facing today's state-of-the-art robotics systems. The driver expected the Model S to see a trailer in front of it. Without assigning blame (because for a safe system, all the problems will have to be solved regardless of which one, if any, caused this accident), we can break this down into several separate possible failures, each with different solutions:  

 
A. Communication FAIL. 
The failure of Tesla the company, and of the Model S during operation, to adequately convey Autopilot's limitations to the driver. Alternately, if we were lawyers for Tesla, we could call this the failure of the driver to comprehend Autopilot's limitations. The practical problem from our point of view is actually the same regardless of responsibility, though responsibility has very real consequences. 

Solutions to this issue could come from the medical device field, where robots and software have been responsible for human lives for much longer than self-driving cars. The solution as far as Tesla is concerned is already complete: Tesla maintains that it warns the driver enough already about how Autopilot is and is not to be used. Future regulatory agencies, tasked with keeping human lives safe from corporate profits, may disagree. One model for how this kind of responsibility might be handled for robotic systems comes from the European Union's Medical Device Directive, already in place for things like surgical robots, wheel chairs, and other medical devices. (http://www.fda.gov/ohrms/dockets/98fr/992075bk.pdf)



B. The failure of a road system that should not have tall tractor trailers stuck at a dead stop across highways. 

C. The failre of a crashing Model S to protect the driver. 

D. The failure of the Model S to see the trailer.



B. Highway safety and system failure 
Multiple posters on Elon Musk's Twitter account pointed out that the tragedy might have been avoided if the tractor trailer had had large side guards, like the kind designed to protect bicyclists from trailers (http://bikeportland.org/2008/06/30/trucks-now-rolling-with-side-underrun-guards-8077). 

-----------------------
Ethics write up: ends do not justify the means. http://spectrum.ieee.org/cars-that-think/transportation/self-driving/tesla-autopilot-crash-why-we-should-worry-about-a-single-death
