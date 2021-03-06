## Welcome to Seoho Kang's Project Page

This pages contain my projects on robotics and deep learning I have done so far. 
I use C++ and Python as main languages. 

### GoWithRobo: Robotic Shopping Cart finding items for customers

GoWithRobo provides the robotic shopping cart in marts. The cart helps customers to find items in marts and especially visually impaired customer can shop independently using this cart.
<iframe width="560" height="315" src="https://www.youtube.com/embed/gzfZvT5ImeY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

As a robotics engineer and founding member of GoWithRobo, I built HW and SW of the whole robot from the scratch to prototype and got down to test in 5 Targets, 2 Whole Foods Markets, 1 CVS and 1 Home Depot. There were briefly 10 steps to accomplish this execution.
1.	Simulation  
Before purchasing lidar, I made Gazebo simulation of mart-like environment and tested the performance of mapping and localization with different lidar settings. I learned lidar's distance affects directly to localization performance in large environment such as marts.
2.	Choosing microcontrollers   
I have tried raspberry pi3, Jetson TX2 and Intel NUC. Other than RTAB-Map, every task depended a lot on CPU performance. After using NUC, errors occurred by frequency limitation were solved. I've tested AWS EC2 but this caused the problem due to poor internet reliablity in common places in the US.
3.	Differential driving Model    
Since the mart is very crowded, I chose the differential driving model to escape freely instead of car-like(Ackerman) model. I bought 4 wheels, 4 motor drivers, implemented RS232 and 4 wheels differential driving model.
4.	PID  
In order to reduce oscillation, I added PID part in my code and tuned it. Also, I filtered out some weird signals from the motor driver.
5.	Odometry   
First, I tried wheel encoder as odometry but the wheel we bought output very unstable wheel odometry. Second, I tried lidar based odometry(laser_scan_matcher) and it worked great. I also tried ICP odometry but the problem was Kinect V2 made 2D lidar ziggle. I thought it was because Kinect's laser sensor affects lidar.
6.	IMU and TF   
I chose to buy BNO055 because it was easy to set up. I used tf package to define coordinate information of lidar, IMU, and the base frame(robot).
7.	Mapping  
I tried and compared cartographer, gmapping, hector SLAM for 2D mapping and A-LOAM for 3D Mapping. Since mart was large, loop closure did not work well and it got even worse when I drew map running robot fast. I gathered Bag file and ran very slowly and tried many parameter combinations but it did not get better. After this, I chose to buy Velodyne VLP-16 and projected this 3D point cloud into 2D map. 
8.	Localization   
I tried AMCL and cartographer. I did not find the cartographer setting to designate initial pose of the robot so I decided to use AMCL. In order to cover 3D space, I bought Dynamixel motor and implemented Spin-hokuyo but there was weird drifting errors. For quick implementation, I fixed to cover 3D space using ultrasonic sensors instead.
9.	Local Plannner   
I tuned parameters of DWA local planner and Teb local planner. Both had pros and cons. Especially for DWA, it went very slow when robot had to rotate and translate simultaneously.  
10.	Move Base  
When the robot got stuck, it was very hard to escape using traditional move base package. I chose to use “move_base_flex” and wrote a script to customize the old version of move_base. I could utilize pros of multiple recovery behaviors and multiple planners.

### Image Based Moving Obstacle Avoidance of Drone Using Deep Reinforcement Learning
This project aims to train(DQN, PPO) drone to avoid moving obstacles. I achieved this goal by making Unity(C#) environment and figured that even drone could avoid in stochastic environment(trained without wind, tested with wind). 
Please refer to the link below to check the results and code.  

[Moving Obstacle Avoidance Drone Code&Result](https://github.com/droneRL2020/Dynamic_obstacle_avoidance_unity)

Plus, this project ambitiously aimed to do "Simulation to Real" which makes deep reinforcement learning model robust to domain changes.
I have tried 4 categories as below.
1. Autoencoders(DAE, beta-VAE, DARLA): I aimed for autoencoder to output same background so that input image simplifies to the same background and the moving obstacle. However, all three models(DAE, beta-VAE, DARLA) could not describe the position changes of the moving obstacles. All three models have over simplified so that the position of moving obstacle in the image have changed after the process of autoencoder.
2. Optical flow: I utilized the Farneback algorithm. It worked well in an ideal setting but when the speed of obstacle has changed, especially when obstacle was moving too slow or too fast, the algorithm did not catch the moving obstacle. Since Farneback algorithm has generated filter by itself, I simply fed (current image - previous image) as an image and let PPO learn to understand the moving obstacle's velocity. This worked well not only with background change but also moving obstacle's texture and size changes.
3. Adversarial noise: Since this project aimed at "Simulation to Real-world", I imagined what if there is a noise(filter) that makes "simulation + noise = real world". So, I made the classifier that classifies two different domain images. After this, I trained an adversarial noise. The classifier classified 'A domain image+noise' as B domain. With this noise, I trained PPO and tested in different domain. Drone could avoid better in unseen domain.
<iframe width="560" height="315" src="https://www.youtube.com/embed/_IH0HoHp17U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  
  
### Haptic Watch for Visually Impaired to Grab Object 
This project aims to make heptic watch which enables the blind to grab the object they want. I utilized ssd and tf-lite to detect object and in order to output 10Hz actuation, I attached Coral Edge TPU on the raspberry pi3. I extracted the center of the object and if the center was located in among 5 regions(left, right, up, down, forward) it output vibration to the watch. To attain the user's input, I made an app using google voice to text.  

<img align="left" width="280" height="200" src="https://user-images.githubusercontent.com/34183439/71782272-a644d300-301b-11ea-8e91-d4c35b7a0a4c.JPG">
<img width="280" height="200" src="https://user-images.githubusercontent.com/34183439/71782296-e99f4180-301b-11ea-8ef9-843424a1dd9e.JPG">
<iframe width="560" height="315" src="https://www.youtube.com/embed/StuMvEEdssI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  
  
### Imitation Learning Based Self-Driving
This project aims to make a camera-based self-driving car using imitation learning. It self-drives hallway by only using a camera. I faced the problem of the non-markovian, and multi-model behaviors and I planed to solve this by combining RNN.
Please visit the link below to see code and result of this project.

[End to End Self-Driving Code&Result](https://github.com/droneRL2020/End-to-end-self-driving)  

  
### AED Drone Delivery Simulator
This project aims to prove the potential of AED drone delivery by simulating AED drone delivery time based on real cardiac arrest and ambulance devliery time data occured over 5 years in Seoul. My role as an intern was to make drone delivery time database for each delivery distance and height by simulating drone(V-Rep). I also gathered the flight time database by flying real-drone in windy and snowy weather. I utilized "Mission Planner" and "dronekitAPI" to activate waypoint flight. After flying real-drone, I added the average arming time of the drone. I validated the simulation as well as added threshold time in different weathers.  

![AED Drone](https://user-images.githubusercontent.com/34183439/71782907-e22f6680-3022-11ea-9901-92c7ca04e41c.PNG)
![AED Drone2](https://user-images.githubusercontent.com/34183439/71782909-e65b8400-3022-11ea-9e40-0b2f872c3f00.PNG)  
<iframe width="560" height="315" src="https://www.youtube.com/embed/aKwoe8s6SYg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
