---
layout: post
title:  "On quantifying risk"
date:   2016-07-28 15:07:00 -0400
categories: uncertainty autonomy testing 
author: WRVB
---

In my co-blogger's last post, she wrote about [fault tree analysis (FTA)][fta].

> An FTA involves very real engineering work and forces a deep understanding of
> a robotic system. However, it works at a system level and narrows the focus
> to parts that can cause problems rather than normal operation. The FTA tool is
> ideal for getting traction on hypothetical problems that are hard to discover
> by looking at a schematic or source code of a complex machine like a
> self-driving car. 

FTA is a good example of what you might call 'classical' risk analysis. Imagine
there's an event you don't want to happen (say, a traffic fatality). The
basic idea is to list conditions under which the event can happen: there is no
accident, or the airbags deploy successfully and are sufficient.[^ai-terms] That
gives you a new problem: how do you ensure those conditions occur? One way is to
repeat the process. For each bad event (a traffic accident occurs, airbags don't
deploy successfully, airbags are insufficient) you list conditions under which
the event might occur. Repeat the process enough times and you wind up with
small, easy to model, easy to quantify events ("the airbag did not deploy
because the wiring was severed by the crash").

[^ai-terms]: These are analogous to preconditions and postconditions of AI,
    though for decision-making problems we typically have a goal we want to
    occur rather than an event we want to prevent.

The point of the exercise is to take something large and hard to model ("how
likely is a traffic fatality?") and break it into many things that are small and
easy to model ("How likely is the airbag wiring to be severed by a crash?").
These easy to model things can be combined using the rules of probability to
compute the probability of the complicated thing. The details of the computation
are beyond the scope of this post, but the process is straightforward and
mechanical.

This seems nice: we can answer a complicated question by answering a bunch of
simple questions and doing some computation. But there's a catch, and it's a big
one. The answer we get is only as good as the model we build.  If we don't
know about some sources of risk, or we mischaracterize the risk from the
ones we *do* know about, our answer can be completely wrong.

That's not a big deal for the kinds of systems industry has traditionally dealt
with. FTA works quite well even for complicated systems like spacecraft or
medical devices. But it works because those systems can be broken down into a
reasonable number of pieces simple enough for engineers to quantify, and
increasingly, artificial intelligence is creeping in to domains where that is
not true. 

Consider a system like the Tesla autopilot, using a variety of complex sensors
to plan for safe navigation. Try to build a fault tree, and sooner or later
you wind up trying to model the failure modes of vision and range finding
algorithms. At that stage, you have one of two choices. You can give up, and
assign a fixed probability of failure to your algorithm, or you can try to write
down the complicated conditions on the geometry and lighting and texture of the
world around you, along with the myriad quantities you require to accurately
predict the performance of your sensors. 

This is an exercise in futility. The space of reasonable images your vision
algorithm may encounter is enormous in a way that is difficult to parse. For
forty years, researchers have been developing new and smarter sets of rules to
parse images. All of that research has been eclipsed[^vision] by simple
algorithms that replace that hand-engineering with lots of training data and
computational power. 

[^vision]: Okay, okay, calm down, only on some problems. I'm sure your CVPR
    paper is lovely.

Problems don't have to be geometric, or even physical, for this phenomenon to
occur.  Deep Blue defeated then-world champion Garry Kasparov in 1996 using a
system of hand-coded rules devised by talented engineers who deeply understood
both chess and AI. This was possible because, despite the complexity of chess,
good play can be encoded in relatively few, relatively simple rules.[^deep-blue]
The game of Go has a rule set with around the complexity as chess, and until
recently, it was believed that human-level play would take decades of research,
because even with enormously large rule sets for evaluating board positions, the
best Go programs were barely able to play at amateur levels. That changed with
the advent of learning methods that are *not* based on hand-coded rules. 

[^deep-blue]: The key word is relatively: the general rules Deep Blue used were
    broken into 8000 parts in addition to special rules for the opening and end
    game, and using these rules it still had to evaluate millions of board
    positions per second.

These modern methods for AI and machine learning are fundamentally different
from the classical approach of breaking down a big problem into little problems
which can be solved by hand. Instead, we write down a very large space of
possible models, and use algorithmic cleverness to search that space for a good
model. Deep learning, the underlying technique used to beat a Go world champion,
is an example of this flavor of approach. 

The issue is not that there are no rule-based models for complicated
systems like vision. The issue is that they are *too big* for humans to find,
and we don't have any systems in place to quantify the risk for systems humans
don't understand. 

This is a huge problem. It doesn't matter how much Tesla unit tests their
software; taken as a whole, the system is almost surely too complicated to
quantify. I don't know what kinds of algorithms Tesla uses in its
autopilot,[^tesla] and it doesn't really matter; the function that vision system
is performing is so complex we cannot possibly expect engineers to understand
every nuance in how it will perform, and I would take any promise that they can
with a huge grain of salt.

[^tesla]: My informed guess is that it was a combination of tracking
    carefully-engineered visual features and a variety of hand-coded heuristics
    to build a world model from the feature tracks, and I would be surprised if
    they were using anything like deep learning for perception. 

One possible solution is to be conservative and mitigate the known risks. If the
Tesla autopilot had a max speed of 5mph, it would be safe regardless of the
reliability of its vision system. An alternative solution is to test the system
exhaustively, for hundreds of thousands of hours in every conceivable
circumstance. For a company like Tesla, the first solution means it won't sell
any cars, and the second means it would pay so much to develop its fleet that
it would hardly matter how many cars it sold. 

Robotics companies today have no good choices, and if we want to see our sci-fi
future of robots making everyone's lives easier, that needs to change. We need a
way to accurately quantify risk, to predict when a system will fail and how that
failure can be mitigated.

[fta]: https://en.wikipedia.org/wiki/Fault_tree_analysis

