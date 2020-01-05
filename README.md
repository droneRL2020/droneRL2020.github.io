## Welcome to Seoho Kang's Project Page

This pages contain my projects on robotics and deep learning I have done so far. 
I like to use C++ and Python as main languages. 

### GoWithRobo: Robotic Shopping Cart finding items for customers

GoWithRobo provides robotic shopping cart in marts. The cart helps customers finding items in marts and especially visually impaired customer can shop independently with our cart. <iframe width="560" height="315" src="https://www.youtube.com/embed/gzfZvT5ImeY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

As a robotics engineer and founding member of GoWithRobo, I built the whole robot’s HW and SW. (Tested in 5 Targets, 2 Whole Foods Market, 1 CVS, 1 Home Depot). 
1.	Simulation
Before purchasing lidar, I simulated different lidar specs by making similar environment to marts and tested mapping and localization.
2.	Choosing microcontrollers
I have tried raspberry pi3, Jetson TX2, Intel NUC.
3.	Differential driving
I implemented RS232 and 4 wheels differential driving model.
4.	PID
In order to, reduce oscillation I tuned PID and filtered out weird signals.
5.	Odometry
First, I tried wheel encoder as odometry but the wheel we bougth output very unstable wheel odometry. Second, I tried lidar based odometry, ICP odometry, RTAB Map odometry.
6.	IMU fusion
7.	Mapping
I tried cartographer, gmapping, hector SLAM.
8.	Localization
AMCL, cartographer
9.	Local Plannner
Tuned DWA local planner, Teb local planner
10.	Move Base
Finally, in order to solve robot stuck problem I wrote a script of “move_base_flex” to customize old version of move_base.


### Haptic Watch for Visually Impaired to Grab Object 
<iframe width="560" height="315" src="https://www.youtube.com/embed/StuMvEEdssI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Imitation Learning Based Self-Driving



### Image Based Moving Obstacle Avoidance of Drone Using Deep Reinforcement Learning



### AED Drone Delivery Simulator

