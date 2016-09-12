
---
layout: post
title: 'Microsoft Research''s Formula for a Safe Robot is called PrSTL'
date: '2016-09-12 19:00:00 -0400'
categories: computation probability microsoft research 
author: AMB
published: false
---

*TL;DR: We want robots that are fast, smart, and safe. Historically, those goals have been traded off, but we need robots to move quickly, use noisy, real-world data, AND still provide useful guarantees on safety.  Microsoft Research and partners at Berkeley University have proposed a framework, called [PrSTL (Probabilistic Signal Temporal Logic)](https://people.eecs.berkeley.edu/~dsadigh/Papers/sadigh-uncertainty-rss16.pdf) that claims to provide exactly that.*

##When is it safe to cross the street?
When is it safe for a robot to cross the street?   As children, I was taught to look "left-right-left": my parents knew that looking a second time is necessary because a car could be approaching that I did not see the first time. Parents impart this knowledge to children with worried scolding. We remember the scolding, and we use our eyes and ears before we cross the street. We need both the model, and the data, to make a decision.

Modern robotics systems commonly need both parts as well. First, before a robot is ever let loose on the world, machine learning techniques are used to build a model that functions as the robot's "rules of the road". Millions of pictures of cars, might be used to train a model for use in identifying cars in a cross walk.  Second, the robot's camera sends new data to the robot's decision maker (also called a 'planner'). In a perfect world, the robot sends its camera data to the model and the model outputs an answer to the robot's question- is it safe to cross the road? 





http://arxiv.org/pdf/1510.08474v1.pdf
http://research.microsoft.com/en-us/um/people/akapoor/papers/RSS2016WS.pdf
https://people.eecs.berkeley.edu/~dsadigh/Papers/sadigh-uncertainty-rss16.pdf
https://www.linkedin.com/in/ashish-kapoor-a2971b6