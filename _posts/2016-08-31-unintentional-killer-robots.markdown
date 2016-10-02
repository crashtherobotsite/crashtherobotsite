---
layout: post
title:  "Five Unintentional Killer Robots"
date:   2016-08-31 18:14:00 -0400
categories: ai safety fatalities da-vinci
author: AMB
robots_rating: 1
---

*TL;DR: 5 unintentionally fatal robots from the 1970s through today provide a glimpse of the safety challenges all engineers face, but also highlight safety challenges unique to AI and robots. All engineers have to worry about broken components, material wear, human interactions, realistic testing, and potential product misuse. Roboticists have to worry about additional factors such as invisibile complexity, unproveable safety factors, expectations based on Hollywood, and human boredom.  These challenges, if not met, can prove fatal.*


Killer Robots. The stuff of Hollywood legends, most killer robots are designed to be killers- gun turrets, lasers, red LED eyes. Generally, they look like this: 

{% include ext_image.html url="http://vignette2.wikia.nocookie.net/terminator/images/1/19/Terminator_robot.jpg/revision/latest?cb=20090512155233" description="T-850, Fatal Hollywood Robot." %}


Much less entertaining are robots in the real world that kill, not by design, but by accident. As a public service announcement, robots that kill you accidentally look like this:


{% include ext_image.html url="https://hci.cs.siue.edu/NSF/Files/Semester/Week13-2/PPT-Text/images/Image3.png" description="Therac-25, Fatal Real World Robot." %}


This list covers 5 accidentally-fatal robots of the modern era.  To make the list, the fatality had to be due specifically to a "robotic" or "AI" feature...but the fatality did NOT have to be due to the feature *malfunctioning*. 

 While there is no perfect definition for [what counts as a robot and what doesn't](http://www.crashtherobot.com/toys/robots/science-fiction/roomba/irobot/2016/07/14/your-robot-should-be-cute-and-needy.html), I've used this general definition: 

 If an electro-mechanical device *senses* any part of the physical world,  *makes a decision* based on input data,  and *actuates* the resulting output, then it qualifies as a robot. If it *accidentally kills someone in the process*, it qualifies for our list.  

*Author's note- Since the author is American, and much of the available data on workplace fatalities comes from OSHA, this list is also very United-States-and-Euro-centric. Robotics safety standards across the world will be a different post.*

## 1. Therac-25 (1985-1987)
Topping our list is the Therac-25, one of the most infamous case studies in medical device design gone wrong. The Therac-25 was a multi-mode radiation therapy device designed to treat different kinds of cancer. Its software, reused from an older model, contained bugs that led to the wrong kind of radiation being applied to patients, causing at least 4 deaths and several additional severe radiation burns. The Therac-25 makes our list for two reasons, one technical and one human. 

Technologically, [one of the root causes](https://en.wikipedia.org/wiki/Therac-25#Root_causes)  of the fatalities was a race condition due to concurrent programming errors: the machine needed a specific amount of time to switch modes when an operator entered a command sequence. In the lab, no operator had ever entered the sequence *fast enough* to cause the error. In a perverse twist of fate, it took several months of real life operation before *experienced technicians* could use the console fast enough to cause the problem.  The second reason the Therac-25 became a classic case study is a combination of human frailty and human arrogance.  Because the Therac-25 treated patients already dying of cancer, and because the company had sent out advertisments for the machine claiming it was 5 orders safer than previously working models, [two people died](http://www.ccnr.org/fatal_dose.html) before anyone even *thought* to blame the software. 
  
The fallout from the Therac-25 radiation disaster caused the FDA to issue the first laws [requiring hospitals to report errors with medical devices to the FDA and the manufacturer](https://computingcases.org/case_materials/therac/case_history/Case%20History.html) in an effort to close the information loop when something goes wrong. The idea is that even if a dangerous medical device gets on the market, a single failure should tip everyone in the country off to the danger.  We're smarter now, right? Which brings us to....


## 2. The Da Vinci Surgical System (2000-present)


{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/thumb/2/23/Cmglee_Cambridge_Science_Festival_2015_da_Vinci.jpg/1280px-Cmglee_Cambridge_Science_Festival_2015_da_Vinci.jpg" description="The Da Vinci Surgical System, Potentially Fatal Real-World Robot" %}


Surgery robots were linked to [144 deaths between 2000 and 2013](http://arxiv.org/ftp/arxiv/papers/1507/1507.03518.pdf) according to a recent paper. The authors of the study raise a growing concern in the medical world: *Are robots really safer surgeons, or is the human desire for a shiny new toy and a more billable surgery procedure actually making people less safe?* 

While it is not completely fair to single out Intuitive Surgical's da Vinci system for all of those deaths, the daVinci system is a marketing juggernaut. Marketing has turned daVinci into a household name that deserves the singling out. In fact, [medical researchers worry](http://jama.jamanetwork.com/article.aspx?articleid=1700496)  that:  

*"Aggressive direct-to-consumer marketing and incentives associated with fee-for-service payment may promote the use of these advanced treatment technologies."*

At least [one group of doctors](http://www.acog.org/About-ACOG/News-Room/News-Releases/2013/Statement-on-Robotic-Surgery) is very disappointed in the effects of marketing robots directly to patients: 

*"Aggressive direct-to-consumer marketing of the latest medical technologies may mislead the public into believing that they are the best choice."*

The expectations set for these robots are high. Consumers want to believe the robots can perform better than human surgeons, or with less skilled operators behind the controls. This belief has not proven conclusively true so far.  While the jury is still out, blanket trust in robot surgeons should not be part of any techno-futurist's arsenal. 

## 3. The Self-Propelled Combine Harvester (1911-Present)
The last 100 years of technological advancement in gigantic farm equipment means a single farmer now manages 1000 acres of crop land. This is a marvelous technological acheivement, but farming in 2016 is still the [6th most fatal occupation](http://www.bankrate.com/finance/personal-finance/10-most-dangerous-jobs-us-1.aspx) in the United States. This danger is due largely to long hours around big heavy machinery,  like the ever-dangerous tractor ([not yet robotic enough](http://herald-review.com/news/opinion/editorial/columnists/ellis/stu-ellis-autonomous-tractors-take-center-stage-at-farm-progress/article_08b6b1bd-0370-5e54-89a4-c1c5cbffe2c0.html)  to make this list) and the self-propelling combine-harvester. 


{% include ext_image.html url="http://westernreservepublicmedia.org/countrycrush/images/cc_gah_3.jpg" description="An event called the Country Crush Demolition Derby can only spring from the safest and gentlest of automated machinery, right?" %}

While giant spinning blades of death on motorized vehicle aren't enough to name something a killer robot, the combine-harvester makes our list in 2016 because the modern robotic features that let it harvest and thresh crops are part of the continued *cause* of accidents. 

A 2014 article in [Modern Farmer](http://modernfarmer.com/2014/06/farm-deaths/)  points out that 1000 acres of land per worker means that when an automated blade pulls in the clothing of a farmer, the farmer is alone and far from help when an accident happens.   A machine will also continue operating even if the tired human supervisor falls asleep after long hours, another source of accidents. 

The UK government has released a [safety guide](http://www.hse.gov.uk/pubns/ais6.pdf) for working with combine harvesters. The document describes injuries from "being pulled into the cutting mechanism" or "being injured by the drive mechanisms or trapped when automatic sensors operate."   

The safe way to operate or repair a temporary blockage on a combine involves completely shutting the machine down, a process that farmers often do not follow in favor of speeding through a [stressful, time critical](http://nasdonline.org/static_content/documents/1241/d001045.pdf)  phase of farming.   A farmer may make the wrong risk assessment despite manufacturers' warning labels.  

The combine harvester is an excellent example of powerful automation that isn't 'human aware enough'. To operate a combine safely requires several steps of a safety process that slows down work and therefore sometimes is skipped by the tired, overworked, or in-a-hurry farmer.  'Smart' farming equipment, like the previous era's medical devices, will need to step up its game. The lives of future farmers depend on it. 

## 4. The Autopilot of Colgan Air Flight 3407 (2009)


{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Continental_Connection_Bombardier_Q400.jpg/1920px-Continental_Connection_Bombardier_Q400.jpg" description="A Bombadier Dash 8 Q400, the same type of plane  that crashed in flight 3407." %}


Increased automation or semi-automation is supposed to free up humans for more difficult cognitive tasks. In modern aviation, a human pilot acts as a lifeguard, standing by for when a robot finds a task too difficult or doesn't know what to do.  Or so goes the theory, [reports Maria Konnikova of the New Yorker](http://www.newyorker.com/science/maria-konnikova/hazards-automation).  In the cold reality of the crash of Colgan Air Flight 3407, it became clear that an [autopilot alerting its human supervisor as designed is not enough to prevent a crash.](https://en.wikipedia.org/wiki/Colgan_Air_Flight_3407)

Airplane crashes are expensive, terrifying, involve the latest technology, and (in the USA) are all thoroughly investigated by the National Transportation Safety Board. As with all other crashes since the 1970s, the NTSB investigated the crash and produced [a crash investigation summary of the February 2009 incident.](http://www.ntsb.gov/investigations/AccidentReports/Reports/AAR1001.pdf) The NTSB concluded that 

*Contributing  to  the  accident  were (1) the flight crew’s failure to monitor airspeed in relation to the rising position of the low-speed  cue,  (2)  the  flight  crew’s  failure  to  adhere  to  sterile  cockpit  procedures,  (3)  the  captain’s  failure to effectively manage the flight, and (4) Colgan Air’s inadequate procedures for airspeed selection and management during approaches in icing conditions.*

Note that nothing on this list reports an autopilot failure.  The autopilot worked as designed.  The "low speed cue" in the report is an alarm reported by the plane's autopilot system.  The job of this indicator is to warn the pilot of how long they have before control is switching to manual piloting.  By the time this warning was noticed by the pilot, it was too late. The manual switchover surprised the pilot, he reacted "consistent with startle and confusion," and the plane crashed, killing all 49 people on board and 1 person in the house the plane crashed into. 


{% include ext_image.html url="https://flyawaysimulation.com/images/downloadshots/9991-dhc8-q400-xzip-11-dh8-q400-panel-doc.jpg" description="Illustration of the many cockpit instruments of the Q400 aircraft." %}

This 'surprise' from a functioning autopilot should not have been a surprise at all. [The NTSB linked it to a similar accident in 1994.](http://www.ntsb.gov/investigations/AccidentReports/Reports/AAR1001.pdf#page=91&zoom=auto,72,374)  Recent research indicates that while autopilots don't cause human pilots to lose their physical joystick skills, the autopilots do replace the human pilot's cognitive skills, [like recognizing failures](http://hfs.sagepub.com/content/56/8/1506).    While the intent of autopilots was to allow humans to focus more on these failures and less on routine calculations, it seems that human minds just wander, resulting in potential crashes.  

Like a truck driver falling asleep with the cruise control on,  boredom when supervising an AI autopilot can be fatal. The moral here for future AI is that technology needs to find a way of keeping humans engaged for the tasks it cannot perform itself.  From a safety perspective, partial AI may be as problematic as no AI at all. 



## 5. Car-Assembling Robot Arms (1979-Present)

[On January 25, 1979,](https://www.wired.com/2010/01/0125robot-kills-worker/) Robert Williams, a factory line worker at a Ford factory in Flat Rock, Michigan became the the first human to be accidentally killed by a robot.  While laws and safety mechanisms are improved and incorporated into the design of robotic arms after each accident, those safety mechanisms still occasionally fail. The year 2015 provided some particularly grisly headlines.  ["Robot grabs man, kills him in German car factory"](https://www.washingtonpost.com/news/morning-mix/wp/2015/07/02/robot-grabs-man-kills-him-in-german-car-factory/) proclaims one article. A tagline an article about a *different* incident read ["The man was reportedly stabbed by a metal arm and electrocuted."](http://www.independent.co.uk/news/world/asia/worker-killed-by-robot-in-welding-accident-at-car-parts-factory-in-india-10453887.html)

It is not a coincidence that the first recorded death by robot occurred in a car factory, or that the accidents continue. Cars are heavy, and made of metal. Robotic arms that lift, weld, bend and shape metal are correspondingly powerful; they pose a greater risk to humans than a robotic sprinkler system. The traditional method of keeping robots and people in separate rooms works only under ideal conditions.  As soon as an arm needs maintenance or repair, a human is sent into the path of a welding robot that is *already misbehaving* and the potential for an accident increases. 


{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/en/9/9b/FANUC_6-axis_welding_robots.jpg" description="Six axis welding robot. The stickers warning people not to step near or on it seem obvious, but could be ignored by a service technician." %}


Just like the combine harvester, accidents frequently happen when humans do not stop the robot while trying to fix a problem and do not follow safety instructions.  The death of Ramji Lal, the worker killed by a welding robot in 2015 in an Indian car factory, occurred while Lal was trying to dislodge a piece of stuck material from the robot. A union representative claimed [management failed to make the environment around the robot safe for workers](http://timesofindia.indiatimes.com/india/Terminator-redux-Robot-kills-a-man-at-Haryanas-Manesar-factory/articleshow/48460738.cms), and the police commissioner booked factory management on negligence charges. 
In the vividly reported case of the German car factory, that malfunction that led to the death of a contractor happened while *installing* the robot: [the robotic arm came alive and crushed the contractor](http://www.independent.co.uk/news/world/europe/worker-killed-by-robot-at-volkswagen-car-factory-10359557.html).

## Conclusion

Complexity, failure to always follow official safety procedures, human boredom, and software bugs have all played roles in accidental death due to robot.  Concluding that humans are part of the problem in human-robot fatalities sounds like circular logic. 

A better conclusion is that expecting humans to act like 20th century robots- tireless, precise, always following every step- is a poor use of the art of engineering. While adopting and *actually following* more safety procedures will keep (and has already kept) humans safe, we are now at a technological tipping point. Instead of expecting humans to act more like robots to keep them safe from robots, we should demand and design smarter robots that act more like humans. 


{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c5/Caught_Coding_%289690512888%29.jpg/1920px-Caught_Coding_%289690512888%29.jpg" 
description="Baxter, a humanoid manufacturing robot with a torque-controlled arm designed to give way when humans run into it, is an example of a smart, collaborative robot design." %}


