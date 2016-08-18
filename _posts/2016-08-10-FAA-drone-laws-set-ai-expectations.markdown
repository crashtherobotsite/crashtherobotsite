---
layout: post
title:  "FAA Drone Laws: Holding AI to the Human Pilot Standards"
date:   2016-08-10 21:10:58 -0400
categories: drones robots autonomy testing government-policy faa part-107
author: AMB
---
*TL;DR: The new Part 107 rules released by the FAA spell out the requirements and test a human must pass to pilot a small drone. They also allow AI to fly the drone as long as a human pilot maintains control and supervision. We measure the state of AI in 2016 against what the FAA expects of its human pilots. In some places, AI comes out on top. In others, the field has a long way to go. *

## Where the Specs Come From ## 
 The predictions made in this article come from 3 places:
 
  - The *actual* laws on the books for small UAVs, known from here on out as [Part 107](https://www.faa.gov/uas/media/part_107_summary.pdf).   After ignoring any laws about pilots or pilot line-of-sight, the remaining laws set a baseline for how a safe AI pilot needs to fly. 
  - [FAA-provided sample pilot test questions](http://www.faa.gov/training_testing/testing/test_questions/media/uag_sample_exam.pdf)  that cover what a commercial human pilot must know to pilot a drone with Line-of-sight. This knowledge not only has to be available to a drone, but made part of the AI's decision making process.
  - A [legal and pilot-perspective analysis from Rupprecht Law](http://jrupprechtlaw.com/part-107-knowledge-test)  of the test questions which. The analysis covers the background science and working knowledge of physics and aviation necessary to become an airman, which an autonomous drone would have to incorporate into its control algorithms. 

The rules are sometimes too vague, and will require much clarification as truly autonomous AI drone flight gets closer to reality, but it's not the FAA's job to provide software specifications for safe drones. That responsibility falls on engineers instead, so let's get to it. 

## The Simple: Robots can do it! 

 If we use very conservative specifications and algorithms, much of Part 107 can be navigated (pun intended) by  existing AI pilots.  Part 107 specified where (400 above ground or building) and when (daylight) a drone can fly. Existing toy drones with geo-fencing apps can already fly routes in allowed fly zones
 {% include image name="shark-drone-big.png" caption="Geofencing AI navigation: so simple even Sharknado here can do it." %}


## The Hard: Robots might do it... but can't yet. ##

## The Superior: Robots are better than Humans. ##
 
## The Unthinkable: Handling Emergencies and Morally Gray Areas  ##

