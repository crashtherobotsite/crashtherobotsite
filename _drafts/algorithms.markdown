---
layout: post
title: '5 Landmark Algorithms that Made Robots Safer'
date: '2016-09-19 19:00:00 -0400'
categories: machine-learning research robotics safety
author: AMB
published: false
---

*TL;DR: We want robots that are fast, smart, and safe.   In 2016, we're closer than ever to achieving that goal. Self-driving cars, package-delivering drones, and robotic vacuum cleaners are all possible because of increased hardware availability, but also because of some particularly smart thinking.  This article covers the historic biggest leaps forward in algorithms for mobile robots. *


##1960s:  NASA uses Digital Image Processing for Mars Photos
One of the most enduring and popular outputs of the robots that NASA sends to space is the beautiful images they send back to the public, but early projects had a problem.  Analog hardware settings for things like exposure time and photographic sensitivity had to be set in advance, and couldn't be easily changed once a vehicle was in space.  Robert Nathan of NASA's Jet Propulsion Laboratory [convinced early mission project leaders](http://history.nasa.gov/computers/Ch9-3.html)  to add Digital Image Processing to the Mariner  and Surveyor programs in the mid-1960s.   

Digital Image Processing is crucial for robotics, and it is so commonplace now that we often don't even recognize it as an engineering achievement.  DIP at its core is 'smart mapping' in a photo- taking a gray image and stretching the colors to the lightest white and the blackest black to allow our eyes to see more information in an image.   DIP is what allows users to fill Pinterest with moody self-portraits,  but it also picks out cancer cells from normal cells in imaging equipment, and lets us see very small differences in temperature or elevation very clearly.   Without the algorithms to change the map of input pixels to output pixels, we would never see stunning images like this: 

![Notice how this isn't what YOU see when you stare at the sun...](http://apod.nasa.gov/apod/image/1609/Filaprom_Lawrence_960.jpg)http://apod.nasa.gov/apod/astropix.html

We also wouldn't be able to make our own pictures look better either...
![enter image description here](http://lestaylorphoto.com/wp-content/uploads/2015/07/Before-After-1400W%28pp_w768_h256%29.jpg)
Now imagine this... on the moon. 

Once we could map image to image, DIP also expanded the capabilities of *other* types of sensors. If robots can map from camera to camera, then they can map from sonar to camera, or LIDAR to camera, or any other number of sensors.   

##1970s: Robots Learn to Walk with the Zero Moment Point
Any toddler could tell you that learning how to walk on two legs is HARD. Robotics researchers agree with the toddlers. The earliest bipedal robots that could walk were programmed to follow this rule: "Always keep your center of gravity somewhere above your base of support."  This rule was easy to program with a few simple calculations about a robot's joints, but it didn't result in robots that walked like humans or any other living biped.  

 Remember the children's game 'Red light, green light'?  For reference,  your center of gravity is in the middle of your torso, pretty close vertically to your belly button. Your base of support is more or less the rectangle on the ground formed by your toes and heels on both feet.  Imagine walking so that if someone yelled "Red light!" at you, your center of gravity was always located somewhere over your feet, with no leaning forward or backwards too far.  You would never *lose* the game because you would never get caught with one foot in the air and fall over.  You would never win the game either, because keeping your belly button over one or both your feet forces you to walk with a slow, shuffle that accurately represents early walking robot motion. 
 
 ![Big feet help too...](https://upload.wikimedia.org/wikipedia/commons/4/47/Nao_Robot_%28Robocup_2016%29.jpg)
 
Enter [Miomir Vukobratović](http://www.pupin.rs/RnDProfile/vukobratovic.html) a Serbian mechanical engineer, and his Zero Moment Point.  In 1968, Dr. Vukobratović presented the first paper explaining an expanded, looser rule for walking robots to follow: "Move so that the physical point (the ZMP) where contact forces caused by friction are exactly balanced out by the inertia and gravity is inside your base of support."  

![The Zero Moment Point](https://upload.wikimedia.org/wikipedia/commons/d/dd/ZMP.GIF)

Once the concept had been articulated, numerous papers were published by others using it to construct their own walking robots.  [This rule is still used in robots today](http://www.cs.cmu.edu/~cga/legs/vukobratovic.pdf) as a metric for how stable a bipedal robot's walk is. The usefulness comes from its simplicity: no matter how many joints or servos we place on a bipedal robot, it still only has 1 or 2 feet in contact with the ground.  Observations that come from follwing the rule include how friction forces limit how fast robots (and humans) can walk safely; if the inertia due to fast motion overpowers the friction forces of the foot (say, because of ice),  the result is a good old Looney Tunes scramble that ends with the walker in a heap. 

![Honda's Asimo, arguably one of the most famous robots using ZMP for walking](https://upload.wikimedia.org/wikipedia/commons/thumb/3/39/ASIMO_4.28.11.jpg/800px-ASIMO_4.28.11.jpg)



##1980s
##1990s
##2000s
##2010s


## More sources for Robotics History
http://www.robotshop.com/media/files/PDF/timeline.pdf
