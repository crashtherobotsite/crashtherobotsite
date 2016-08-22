---
layout: post
title: 'FAA Drone Laws: Holding AI to the Human Pilot Standards'
date: '2016-08-10 21:10:58 -0400'
categories: drones robots autonomy testing government-policy faa part-107
author: AMB
published: true
---

*TL;DR: The new Part 107 rules released by the FAA spell out the requirements and the test a human[1] must pass to pilot a small drone. The law also allows AI to perform the task of flying the drone as long as a human pilot maintains control and supervision. We measure the state of AI in 2016 against what the FAA expects of its human pilots. In some places, AI already comes out on top. In others, the field has a long way to go.*


## Introduction 

*"The FAA agrees with the commenters who pointed out that the ability for a small unmanned aircraft to fly  autonomously could add significant utility to a small UAS operation and would further encourage innovation in the industry. Accordingly, this rule will allow the autonomous flight of small unmanned aircraft."* -[Part 107, page 296](http://www.faa.gov/uas/media/RIN_2120-AJ60_Clean_Signed.pdf#page=293&zoom=auto,106,542)
-----------------------------------

## Where the Specs Come From 
 The metrics used to benchmark a human against a theoretical AI in this article come from 3 places:
 
  - The *actual* laws on the books for small UAVs, known from here on out as [Part 107](https://www.faa.gov/uas/media/part_107_summary.pdf). The [full text](http://www.faa.gov/uas/media/RIN_2120-AJ60_Clean_Signed.pdf) can be found here.  Since we're measuring against an AI, we ignore any laws about pilots themselves. This eliminates several laws about line-of-sight and direct pilot supervision of aircraft, presently in place because AI are not self-sufficient. For example, drones can only be flown in daylight because otherwise a human pilot can't maintain line of sight. The remaining laws set a baseline for how a safe AI pilot needs to fly to *be* self-sufficient. 
  - [FAA-provided sample pilot test questions](http://www.faa.gov/training_testing/testing/test_questions/media/uag_sample_exam.pdf) that cover what a human commercial pilot must know to pilot a drone with line-of-sight. This knowledge not only has to be available to a drone, but also made part of the drone AI's decision making process.
  - A [legal and pilot-perspective analysis from Rupprecht Law](http://jrupprechtlaw.com/part-107-knowledge-test) of the test questions. The analysis covers the background science and working knowledge of physics and aviation necessary to become an airman. While the article was written to help human pilots study for a test, the article's deep explanations for test answers demonstrate that an AI will have to account for far more than just the right answers to the questions to compare to a human pilot.  A successful pilot AI will have to incorporate the principles behind the questions into its control algorithms.   

The rules are sometimes vague and will require much clarification as truly autonomous AI drone flight gets closer to reality, but it's not the FAA's job to provide software specifications for safe drones. That responsibility falls on engineers instead!

## Easy does it: Slow and Careful in 2016. 

 If we use very conservative specifications and algorithms, much of Part 107 can be navigated (pun intended) by existing AI pilots.  Part 107 specifies where (400 feet above the ground or buildings) and when (daylight) a drone can fly. Existing toy drones with geo-fencing apps can already slowly fly routes in allowed zones using GPS sensing and data that keeps them well clear of designated no-fly zones. Drone controllers are also already pretty good at keeping on a pre-planned route, with a caveat for bad weather conditions. 

![Google 'Shark Drone'. Do it, I dare you.]({{site.baseurl}}/_posts/shark-drone.jpg)*Geofencing navigation on a nice day: so simple even Sharknado here can do it.*

**Encoding The Rules**

An additional set of knowledge easily encoded into an AI involves mapped out designated areas. It is the pilot's responsibility to know where the legal fly and no-fly areas are for particular aircraft. This kind of information needs to be encoded into a map for a drone to use, but again, a conservative flight plan that takes the latest legal FAA map and avoids the edges of no-fly zones can safely fly using AI. 

The pilot's test also includes a test of knowledge on radio procedures and reporting procedures on take-off, flight, and landing. A pilot must report to a radio control tower on the correct frequency. In addition, the pilot must file reports in case of certain deviations, including emergency maneuvers. These items are the *definition* of a protocol- and computers are quite good at formally defined protocols.  Drones can easily follow rules about informing a radio tower before take off. No problems here, at least on the AI front. Whether or not the *tower* can deal with 100 UAVs chirping at it will be present a different technical challenge.

**Physics is Easy for Computers** 

Finally, the pilot's test contains numerous physics calculations about drone Center of Gravity and air-speed to determine whether a flight may occur at all in high winds or with too heavy of a payload. This means a drone AI (or a different piece of hardware on the ground) will need to use sensors to learn about itself and its loads. There are two approaches here in typical robotics applications: the drone will either need to collect data to assure itself that it is safe to take off, or a drone can artifically throttle back its performance to ensure that it has extra margin to handle any unknowns that it encounters without trouble.  Since weight and power are both precious commodities in a flying drones, an entirely different, ground-based drone-checking-machine that talks to the drone's AI might well be on the table. Either way, this is known engineering territory rather than a potential impossibility. 


## The Hard and Fast: Not Quite Yet

What a drone AI can do slowly with lots of margin might not scale when more performance is demanded. Hard physical limits, like the inability to use GPS indoors or in bad weather, will necessitate future technology developments. Part 107 lists out several requirements that even the best AI, one with very expensive hardware, cannot accomplish as of 2016. Most of these requirements cover "in-flight" safety-related judgements.

**It's a Bird! It's a Plane! No... it's Superman!** 

One area that will need major advancement is having an AI using computer vision to make decisions. Part 107 forbids flying directly over "humans outside a covered structure."  To follow this rule, an AI needs to be able to tell the difference, in real time, between human, a human on a bike, a human in a shark cage, and a dog. A drone has to track multiple people separately to avoid flying over any of them, and the drone has to do this with onboard data (from a camera or other sensors) while moving. While beyond the scope of this article, this level of both object tracking and recognition is on the far cusp of what present computer vision systems can accomplish. Research in the field of self-driving cars is propelling this kind of research forward, but self-driving cars, can carry many more high-powered sensors and processing chips than a drone. As of 2016, throwing sensors at the problem is still not good enough to completely solve the problem of identifying "humans" from a top down view point. Such software is not on the commercial market yet [2].

**Know Thyself**

In addition to identifying objects in range, AI advancements in ongoing self-evaluation and self-calibration are also needed. Many of the questions on the pilot's exam are about [evaluating weather conditions while flying](http://www.faa.gov/uas/media/RIN_2120-AJ60_Clean_Signed.pdf#page=171&zoom=auto,106,720) and deciding, *during the flight,* if visibility and other sensor data has been compromised to an unsafe point. 

Most AI today still relies on the principle "garbage in, garbage out."  If fog obscures the camera, the AI may produce spurious results rather than trying to switch to some other sensor the way a human would.  AI will need to recognize when they are compromised, but not be so conservative that they land at the first hint of a cloud in the sky. 

**With Great Power comes Great Responsibility**

A final subtle legal area that will require *BIG* advancements in AI research is the set of laws directed at human pilots that require a drone *to comprehend the end effects of its actions*. To take a simple example, the FAA is requiring pilots to [report injury or damages over $500]() caused by a crash to the authorities. While we can engineer diagnostics to make an AI report damage *to itself*, if an drone scratches a mailbox on its latest delivery, to follow the spirit of the FAA rule, the drone has to be able to understand that *it scratched the mailbox*, not the neighbor's dog. A more serious example is the general law requiring a drone to [yield to manned high speed aircraft in crowded, legal airspaces](). If a human pilot isn't following rules as precisely as the drone expects, what should it do? 

Existing AI does not handle new scenarios well. To truly learn from brand new scenarios requires a kind of general strong AI that is the stuff of Hollywood movies at present.  Even a narrowed-down problem, like being able to predict what a human pilot with might do if faced with a robot collision, is a hard enough task on the ground in 2D that self-driving car promoters [have called for driverless-car-only zones](http://www.wsj.com/articles/why-cities-arent-ready-for-the-driverless-car-1461550001). The classical chess AI problem of "If I move over here, where will my adversary move?" takes on ever more importance when it has to be computed in real time at 100 miles an hour. While advancements have been made in taking on decision spaces like [the game of Go](), the real world is even more complex. 


## The Superior: Swarms of Robots are better than Single Humans. ##

**Tired Eyes**

There are some areas where an AI might already be a better choice than a human pilot. Several of the laws and processes that the FAA expects human pilots to be aware of are specific techniques for [dealing with pilot fatigue and eyesight limitations.]()  Human pilots need to adopt visual scanning techniques around their drone because they do not have eyes in all directions.  While an AI might not presently perform at the level of a human pilot when identifying a bird in the air, its algorithms for spotting the bird will work just as well no matter how long the drone has been flying. 

**Working Together**

The FAA also specs certain top speeds and altitudes for drones and forbids controlling drones while a pilot is based in a moving vehicle or aircraft. These safety rules are there because of human pilot reaction times. Drones have already been programmed to move slowly in concert with each other for some [beautiful aesthetic displays](https://www.youtube.com/watch?v=teQwViKMnxw),  but there are also more (commercial uses for coordinated swarms of drones in sensing and agriculture)[https://www.youtube.com/watch?v=ge3--1hOm1s] that may make more sense if the drones can fly faster and cover more ground safely.  The speed limits on drones at present are tied to human pilots on the ground, and a safe AI drone that can move out of sight allows for more *full use* of the potential drones already have.

 
## The Unthinkable: Handling Emergencies, Privacy, and Morally Gray Areas  ##

Because Part 107 is a law, it devotes a fair amount of space to who is responsible if a drone crashes. (Short answer: the pilot). Intertwined with the legal repercussions of drone crashes are some relevant assumptions about how a human pilot should act in case of an emergency. Part 107 itself states: "Finally, in case of an in-
flight emergency, the remote pilot in command will be permitted to deviate from any rule of part 107 to the 
extent necessary to meet that emergency."  Part 107 further documents how the FAA decided to allow emergency deviations. Excerpted testimony in Part 107 includes an example where, to avoid a collision, a drone might need to fly over people. 

*"...The FAA also emphasizes that the remote pilot in command must always prioritize the safety of human life above all other considerations..."*  -[Part 107, page 115](http://www.faa.gov/uas/media/RIN_2120-AJ60_Clean_Signed.pdf#page=111&zoom=auto,106,233)
-----------------------------------

This kind of moral relativism is easy for humans to understand, but impossible for an AI. An AI pilot might not be able to ever replicate this kind of behavior because the *desired* behavior is not what is judged: instead, the human reaction is legally considered case-by-case and *rationalized afterwards* with a report to the FAA. A human pilot has to report why a decision was made *after the fact*. If it can be rationalized by a human pilot, it's acceptable, even if the manuever is objectively more risky. If an AI pilot uses a scenario model to choose to fly over a human on the ground to avoid a manned aircraft, but then hits the human on the ground, the AI cannot rationalize its way out.  This is not a problem solveable by technology- it is endemic to the AI *not* being a human. The best an AI can do is provide a detailed output of its decision tree for review by engineers. 

**Privacy**

Part 107 makes no *laws* specifically about drones and privacy. Part 107 does [report future plans by the FAA](http://www.faa.gov/uas/media/RIN_2120-AJ60_Clean_Signed.pdf#page=526&zoom=auto,106,266) to work to encourage [best practices for privacy](https://www.ntia.doc.gov/files/ntia/publications/voluntary_best_practices_for_uas_privacy_transparency_and_accountability_0.pdf). As evidenced by the concerned citizen's groups whose comments were included in the report, it's widely believed that a drone (AI or human-piloted) can be perfectly capable of safe flying and not crashing and still be *terrible* at respecting privacy. This belief is substantiated- from unauthorized use of customer data to [plotting domestic violence safe-houses on Google Maps](http://www.ibtimes.com/google-maps-accused-revealing-secret-locations-domestic-violence-shelters-1946808), technology companies have a terrible track record when it comes to putting people before data. 

AI pilots add a wrinkle to the privacy debate. A basic observation of modern robotics research is that an AI's capacity to get better at flying is likely directly related to access to as much of the highest quality camera data it can process. Unfortunately, personal privacy is directly related to the *lack* of access to that camera data.  It's almost *inevitable* that an AI drone will not respect privacy as much as a human pilot might.  How this problem is dealt with will obviously have social and policy consequences, but it will also have technical consequences. Lack of data could make a less safe AI. The technical challenge of scrubbing out personal details and leaving in details relevant for flying may very well create demand for an entirely new kind of AI!  


## Conclusion 

The FAA Part 107 law sets the standard for human pilots, but also provides a framework for what technology will have to do to acheive autonomous drones. AI-powered drones provide benefits in the areas of length of flight time without exhaustion, the ability to swarm and accomplish complex group behaviors, and increased control performance outside human reactions times. However, realizing these benefits will require considerable additional research effort in the fields of safety, AI computer vision, object recognition, and learned models of a drone's effect on the world around it and vice versa.  The FAA is to be commended for encouraging researchers to tackle these problems with a regulatory framework that promotes human safety and allows AI-flown drones for innovation, but more concrete laws with a technical bent may be required to allow an AI pilot to be "proveably" good enough to fly with human pilots. 




**Footnotes**
[1] The FAA really said 'human.' The early release of the bill used the word 'person,' but the final release changed the wording because the legal definition of a 'person' apparently includes corporations as whole. Whether an AI or AI+human combination could ever be considered a legal 'person' is up for speculation.
[2] See my upcoming post on the promises and actuality of the state of commercial AI in 2016. 
