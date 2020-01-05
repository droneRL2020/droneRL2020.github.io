## Welcome to Seoho Kang's Project Page

This pages contain my projects on robotics and deep learning I have done so far. 
I like to use C++ and Python as main languages. 

### GoWithRobo: Robotic Shopping Cart finding items for customers

GoWithRobo provides robotic shopping cart in marts. The cart helps customers finding items in marts and especially visually impaired customer can shop independently with our cart. 
<iframe width="560" height="315" src="https://www.youtube.com/embed/gzfZvT5ImeY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

As a robotics engineer and founding member of GoWithRobo, I built the whole robot’s HW and SW from scratch which end up tested in 5 Targets, 2 Whole Foods Market, 1 CVS, 1 Home Depot. There were briefly 10 steps to accomplish this goal.
1.	Simulation
Before purchasing lidar, I made Gazebo simulation of mart-like environment and tested the performance of mapping and localization with different lidar settings. I learned lidar's distance affects directly to localization performance in large environment like marts.
2.	Choosing microcontrollers
I have tried raspberry pi3, Jetson TX2 and Intel NUC. Other than RTAB-Map, every task depended a lot on CPU performance. After using NUC, most of the errors occured by frequency were solved. I tested AWS EC2 but this led problem because of poor internet reliablity in many places in the US.
3.	Differential driving Model.
Since, mart is very crowded I chose differential driving model to escape freely instead of car-like(Ackerman) model. I bought 4 wheels and 4 motor drivers and implemented RS232 and 4 wheels differential driving model.
4.	PID
In order to, reduce oscillation I added PID part in my code and tuned it. Also, I filtered out some weird signals from the motor driver.
5.	Odometry
First, I tried wheel encoder as odometry but the wheel we bougth output very unstable wheel odometry. Second, I tried lidar based odometry(laser_scan_matcher) and it worked great. I also tried ICP odometry but the problem was Kinect V2 made 2D lidar ziggle. I thought it was because Kinect's laser sensor affects lidar.
6.	IMU and TF
I chose to buy BNO055 because it was easy to set up. I used tf package to define coordinate information of lidar, IMU, and the base frame(robot).
7.	Mapping
I tried and compared cartographer, gmapping, hector SLAM for 2D mapping and A-LOAM for 3D Mapping. Since mart was large, loop closure did not work well and it got even worse when I drew map running robot fast. I gathered Bag file and ran very slowly and tried many parameter combinations but it did not get better. After this, I chose to buy Velodyne VLP-16 and projected this 3D point cloud into 2D map. 
8.	Localization
I tried AMCL and cartographer. I did not find cartographer setting to designate initial pose of the robot so I chose to use AMCL. In order to cover 3D space I bought Dynamixel motor and implemented Spin-hokuyo but there was a weird drifting errors. For quick implementation I chose to cover 3D space using ultrasonic sensors instead.
9.	Local Plannner
I tuned parameters of DWA local planner and Teb local planner. Both had pros and cons. Especially for DWA, it went very slow when robot had to rotate and translate simultaneously.  
10.	Move Base
When robot gets stuck it was very hard to escape using traditional move base package. I chose to use “move_base_flex” and wrote a script to customize old version of move_base. I could utilize pros of multiple recovery behaviors and multiple planners.

### Image Based Moving Obstacle Avoidance of Drone Using Deep Reinforcement Learning
This project aims to train(DQN, PPO) drone to avoid moving obstacles. I achieved this goal by making Unity(C#) environment and even drone could avoid in stochastic environment(trained without wind, tested with wind). 
Please check link below to check results and code.  

[Moving Obstacle Avoidance Drone Code&Result](https://github.com/droneRL2020/Dynamic_obstacle_avoidance_unity)

Plus, this project ambitiously aimed to do "Simulation to Real" which makes deep reinforcement learning model robust to domain changes.
I have tried 4 categories.
1. Autoencoders(DAE, beta-VAE, DARLA): I aimed for autoencoder to output same background so that input image simplifies to same background and the moving obstacle. However, all three models(DAE, beta-VAE, DARLA) could not describe the position changes of the moving obstacles. All three models over simplified so that moving obstacle's position in the image changed after the process of autoencoder.
2. Optical flow: I utilized Farneback algorithm. It worked well in an ideal setting but when obstacle's speed changes especially when obstacle was moving too slow or too fast, the algorithm did not catch moving obstacle. Since Farneback algorithm generates filter by itself I simply fed (current image - previous image) as an image and let PPO learn to understand the moving obstacle's velocity. This worked not only well with background change but also was robust to moving obstacle's texture, size changes.
3. Adversarial noise: Since, this project's goal is "Simulation to Real-world", I imagined what if there is a noise(filter) that makes simulation + noise = real world. So, I made a classifier that classifies two different domain images. After this, I trained an adversarial noise. The classifier classified 'A domain image+noise' as B domain. With this noise, I trained PPO and tested in different domain. Drone could avoid better in unseen domain.
<iframe width="560" height="315" src="https://www.youtube.com/embed/_IH0HoHp17U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Haptic Watch for Visually Impaired to Grab Object 
This project aims to make heptic watch that enables the blind grab object they want. I utilized ssd and tf-lite to detect object and in order to output 10Hz actuation I attached Coral Edge TPU on the raspberry pi3. I extracted object's center and if the center was located in among 5 regions(left, right, up, down, forward) it ouptuts vibration to the watch. To get user input, I made an app using google voice to text.  

<img align="left" width="280" height="200" src="https://user-images.githubusercontent.com/34183439/71782272-a644d300-301b-11ea-8e91-d4c35b7a0a4c.JPG">
<img width="280" height="200" src="https://user-images.githubusercontent.com/34183439/71782296-e99f4180-301b-11ea-8ef9-843424a1dd9e.JPG">
<iframe width="560" height="315" src="https://www.youtube.com/embed/StuMvEEdssI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Imitation Learning Based Self-Driving
This project aims to make a camera-based self-driving car using imitation learning. It self-drives hallway by only using a camera. I faced problem of the non-markovian, and multi-model behaviors and I plan to solve this by combining RNN.
Please visit linke below to see code and result of this project.

[End to End Self-Driving Code&Result](https://github.com/droneRL2020/End-to-end-self-driving)
### AED Drone Delivery Simulator
This project aims to prove the potential of AED drone delivery by simulating AED delivery based on real cardiac arrest data over 5 years in Seoul. My role, as an intern, was to make drone delivery time database for each delivery distance and height by simulating drone(V-Rep). I also flew real drone in windy and snowy weather. I added average arming time of the drone. By flying real-drone I not only validated simulation but also could add threshold in different weathers.  

![AED Drone](https://user-images.githubusercontent.com/34183439/71782907-e22f6680-3022-11ea-9901-92c7ca04e41c.PNG)
![AED Drone2](https://user-images.githubusercontent.com/34183439/71782909-e65b8400-3022-11ea-9e40-0b2f872c3f00.PNG)
![AED Drone3](https://user-images.githubusercontent.com/34183439/71782973-b95ba100-3023-11ea-946f-ac9e0830a5ce.png)
