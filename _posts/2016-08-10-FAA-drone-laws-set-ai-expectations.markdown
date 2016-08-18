---
layout: post
title: 'FAA Drone Laws: Holding AI to the Human Pilot Standards'
date: '2016-08-10 21:10:58 -0400'
categories: drones robots autonomy testing government-policy faa part-107
author: AMB
published: true
---
*TL;DR: The new Part 107 rules released by the FAA spell out the requirements and test a human must pass to pilot a small drone. They also allow AI to fly the drone as long as a human pilot maintains control and supervision. We measure the state of AI in 2016 against what the FAA expects of its human pilots. In some places, AI comes out on top. In others, the field has a long way to go. *

## Where the Specs Come From ## 
 The predictions made in this article come from 3 places:
 
  - The *actual* laws on the books for small UAVs, known from here on out as [Part 107](https://www.faa.gov/uas/media/part_107_summary.pdf).   After ignoring any laws about pilots or pilot line-of-sight, the remaining laws set a baseline for how a safe AI pilot needs to fly. 
  - [FAA-provided sample pilot test questions](http://www.faa.gov/training_testing/testing/test_questions/media/uag_sample_exam.pdf)  that cover what a commercial human pilot must know to pilot a drone with Line-of-sight. This knowledge not only has to be available to a drone, but made part of the AI's decision making process.
  - A [legal and pilot-perspective analysis from Rupprecht Law](http://jrupprechtlaw.com/part-107-knowledge-test)  of the test questions which. The analysis covers the background science and working knowledge of physics and aviation necessary to become an airman, which an autonomous drone would have to incorporate into its control algorithms. 

The rules are sometimes too vague, and will require much clarification as truly autonomous AI drone flight gets closer to reality, but it's not the FAA's job to provide software specifications for safe drones. That responsibility falls on engineers instead, so let's get to it. 

## The Simple: Robots can do it carefully. 

 If we use very conservative specifications and algorithms, much of Part 107 can be navigated (pun intended) by  existing AI pilots.  Part 107 specified where (400 above ground or building) and when (daylight) a drone can fly. Existing toy drones with geo-fencing apps can already slowly fly simple, mapped out routes in allowed zones using GPS sensing and data that keeps them well clear of designated no-fly zones. Drones are also already pretty good at keeping constant altitude, with a caveat about weather conditions. 

![Google 'Shark Drone'. Do it, I dare you.]({{site.baseurl}}/_posts/shark-drone.jpg)*Geofencing AI navigation on a nice day: so simple even Sharknado here can do it.*


An additional set of knowledge that is easily encoded into an AI involves mapped out designated areas. For the FAA, it is the pilot's responsibility to know where the legal fly and no-fly areas are for particular aircraft. This kind of information needs to be encoded into a map for a drone to use, but again, a conservative flight plan that takes the latest legal FAA map and avoids the edges of no-fly zones can safely fly using AI. 

The pilot's test also includes a fair amount of requirements to make sure that a human pilot knows to follow a specific set of radio procedures and reporting procedures on take-off, flight, and landing. A pilot has to report a lot of information audibly to a radio control tower on the correct frequency. In addition, the pilot must file reports in case of certain deviations, including emergency manuevers. These items are the *definition* of a protocol- and computers are quite good at formally defined protocols. Need to tell a tower before we take off? No problems here, at least on the AI front. Whether or not the *tower* can deal with 100 UAVs chirping at it is a different problem.

## The Hard: Robots might do it... but can't yet. ##

## The Superior: Robots are better than Humans. ##
 
## The Unthinkable: Handling Emergencies and Morally Gray Areas  ##
