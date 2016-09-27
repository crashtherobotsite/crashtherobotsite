---
layout: post
title: '3 Historical Algorithms Still Making Robots Safer'
date: '2016-09-19 19:00:00 -0400'
categories: machine-learning research robotics safety
author: AMB
published: false
---

*TL;DR: We want robots that are fast, smart, and safe.   In 2016, we're closer than ever to achieving that goal. Self-driving cars, package-delivering drones, and robotic vacuum cleaners are all possible because of increased hardware availability, but also because of some particularly smart thinking.  This article covers 3 of the biggest leaps forward in algorithms for AI and robots from the early years- the 1960s, 70s, and 80s.*


##1960s:  NASA uses Digital Image Processing for Mars Photos
One of the most enduring and popular outputs of the robots that NASA sends to space is the beautiful images they send back to the public, but early projects had a problem.  Analog hardware settings for things like exposure time and photographic sensitivity had to be set in advance, and couldn't be easily changed once a vehicle was in space.  Robert Nathan of NASA's Jet Propulsion Laboratory [convinced early mission project leaders](http://history.nasa.gov/computers/Ch9-3.html)  to add Digital Image Processing to the Mariner  and Surveyor programs in the mid-1960s.   

Digital Image Processing is crucial for robotics, and it is so commonplace now that we often don't even recognize it as an engineering achievement.  DIP at its core is 'smart mapping' in a photo- taking a gray image and stretching the colors to the lightest white and the blackest black to allow our eyes to see more information in an image.   DIP is what allows users to fill Pinterest with moody self-portraits,  but it also picks out cancer cells from normal cells in imaging equipment, and lets us see very small differences in temperature or elevation very clearly.   Without the algorithms to change the map of input pixels to output pixels, we would never see stunning images like this: 

{% include ext_image.html url="http://apod.nasa.gov/apod/image/1609/Filaprom_Lawrence_960.jpg" description="Notice how this isn't what YOU see when you stare at the sun? Thank [NASA](http://apod.nasa.gov/apod/astropix.html)" %}

We also wouldn't be able to make our own pictures look better either...


{% include ext_image.html url="http://lestaylorphoto.com/wp-content/uploads/2015/07/Before-After-1400W%28pp_w768_h256%29.jpg" description="Now imagine this... on the moon." %}


Once we could map image to image, DIP also expanded the capabilities of *other* types of sensors. If robots can map from camera to camera, then they can map from sonar to camera, or LIDAR to camera, or any other number of sensors.   

##1970s: Robots Learn to Walk with the Zero Moment Point
Any toddler could tell you that learning how to walk on two legs is HARD. Robotics researchers agree with the toddlers. The earliest bipedal robots that could walk were programmed to follow this rule: "Always keep your center of gravity somewhere above your base of support."  This rule was easy to program with a few simple calculations about a robot's joints, but it didn't result in robots that walked like humans or any other living biped.  

 Remember the children's game 'Red light, green light'?  For reference,  your center of gravity is in the middle of your torso, pretty close vertically to your belly button. Your base of support is more or less the rectangle on the ground formed by your toes and heels on both feet.  Imagine walking so that if someone yelled "Red light!" at you, your center of gravity was always located somewhere over your feet, with no leaning forward or backwards too far.  You would never *lose* the game because you would never get caught with one foot in the air and fall over.  You would never win the game either, because keeping your belly button over one or both your feet forces you to walk with a slow, shuffle that accurately represents early walking robot motion. 
 
 
{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/4/47/Nao_Robot_%28Robocup_2016%29.jpg" description="Big feet help too..." %}
 
 
Enter [Miomir Vukobratović](http://www.pupin.rs/RnDProfile/vukobratovic.html) a Serbian mechanical engineer, and his Zero Moment Point.  In 1968, Dr. Vukobratović presented the first paper explaining an expanded, looser rule for walking robots to follow: "Move so that the physical point (the ZMP) where contact forces caused by friction are exactly balanced out by the inertia and gravity is inside your base of support."  

{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/d/dd/ZMP.GIF" description="The Zero Moment Point" %}

Once the concept had been articulated, numerous papers were published by others using it to construct their own walking robots.  [This rule is still used in robots today](http://www.cs.cmu.edu/~cga/legs/vukobratovic.pdf) as a metric for how stable a bipedal robot's walk is. The usefulness comes from its simplicity: no matter how many joints or servos we place on a bipedal robot, it still only has 1 or 2 feet in contact with the ground.  Observations that come from follwing the rule include how friction forces limit how fast robots (and humans) can walk safely; if the inertia due to fast motion overpowers the friction forces of the foot (say, because of ice),  the result is a good old Looney Tunes scramble that ends with the walker in a heap. 

{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/thumb/3/39/ASIMO_4.28.11.jpg/800px-ASIMO_4.28.11.jpg" description="Honda's Asimo, arguably one of the most famous robots that uses the ZMP in it's walking algorithm" %}


##1980s: Rete Algorithm and Expert Systems Save Lives
[The failure of 1970s research](https://en.wikipedia.org/wiki/History_of_artificial_intelligence#Boom_1980.E2.80.931987) to produce a general AI that could think like a human gave rise to a new kind of AI to get around the problem: "[the expert system.](https://en.wikipedia.org/wiki/Expert_system)"  Instead of trying to develop *general* principles of thinking,  AI researchers re-evaluated what was necessary to make an AI an expert in a specialized area (also called a "domain").  Even with the slower computers of the 1980s, expert systems succeeded in [producing useful business insights](https://en.wikipedia.org/wiki/Expert_system#History) and [prescribing medication for rare blood diseases as well as human experts](http://www.it.bton.ac.uk/staff/lp22/cs237/cs237medicalxsys.html#MYCIN:%20medical%20diagnosis%20using%20production%20rules), assuring their continued existence in the software world to this day. 


{% include ext_image.html url="https://ict-patana.wikispaces.com/file/view/2002-9980fig2.gif/32424373/491x273/2002-9980fig2.gif" description="" %}

The basic idea of an expert system is to encode huge numbers of logical rules that describe domain knowledge like medicine, business, or even 'common sense' into a database. An AI program then uses an 'inference engine' to pull information from the database to answer a question. 

The speed at which an inference engine can evaluate logical statements is critical to performance of the AI.  Initial naive algorithms were very slow because they checked every rule individually, running through a series of "IF-X-THEN-Y" statements that formed a decision tree. For example,  consider these statements: 
 1. If the patient is warm, they have a fever. 
 2. If the patient is sick, they might die. 
 3. If the patient is bleeding, they might die.
 4. If the patient has a fever, they are sick. 
 
A human immediately makes the jump from "If the patient is warm, they might die." However, an AI originally would need to run its program *twice*- first to acquire the new information or *inference* that the patient is sick, and then a second time through the rules to get the new information that the patient might die.  While this example seems small, imagine a tree where new information like statement (4) is only gleaned after running many of comparisons, and then forces the whole rule set to be re-computed.  The results become too slow to compute. 

A clever human would try to re-order the rules so that this sort of mishap did not happen often, but that means a designer is responsible for hand-ordering thousands of rules to try and get the order that results in the least extra work for the computer. Sounds rather backwards, doesn't it?  To solve this problem, CMU professor Charles Forgy created the [Rete algorithm](https://en.wikipedia.org/wiki/Rete_algorithm).  He first published a version in 1974, and descendants of this algorithm are still in use in expert systems more than 40 years later.  

["The brilliant idea that Dr. Charles Forgy developed was to decouple the evaluation of hypothesis from execution sequencing."](http://www.sparklinglogic.com/rete-algorithm-demystified-part-2) 

 'Rete' means 'net' in Latin, and the Rete algorithm builds a "Rete", a network of nodes in a [trie](https://en.wikipedia.org/wiki/Trie) data structure that keeps track, at each node, of a *single condition* that can be used to satisfy part of a rule.   A rule with a set of conditions to satisfy  is represented as a *path through the network*.  ([Here](http://cis-linux1.temple.edu/~giorgio/cis587/readings/rete.html) are some [examples](http://www.sparklinglogic.com/rete-algorithm-demystified-part-2) of Rete networks with different kinds of rules.)  If the set of true facts matches all the conditions for a rule, then the terminal "Rule node" is reached, and may result in a conclusion or in an inference, an additional fact to send back through the Rete. 


{% include ext_image.html url="https://upload.wikimedia.org/wikipedia/commons/0/05/Rete.svg" description="" %}

The structure of a Rete is meant to take advantage of the fact that while there are many, many facts and rules in a system, there are many fewer new facts discovered *while we are running the algorithm*.   Building a Rete means that when new facts are discovered (like the fact that our patient is sick), we don't have to re-evaluate all of the other rules (paths through the Rete). We can run through only the new paths that use our new fact, avoiding unrelated facts and paths, and we do not have to worry about missing other branches that use  our fact.  The downside of building this Rete is memory storage (we have to be able to store all the facts and the mappings to them in memory), which is traded off for better speed. 

The Rete algorithm has been improved on by its creator, but the basic version has been [implemented in multiple computer languages](http://stackoverflow.com/questions/12474769/how-to-use-rete-algorithm)  and is still in use today.  

##Extras
1. [Jess, the Java Implementation of Rete](http://www.jessrules.com/docs/71/rete.html)
2. [A Timeline of Robotics History](http://www.robotshop.com/media/files/PDF/timeline.pdf)


