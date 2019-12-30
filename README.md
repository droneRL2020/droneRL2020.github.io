# Projects and Work during Robotics Master's at NYU

## GoWithRobo: Robotic Shopping Cart finding items for customers
GoWithRobo offers robotic shopping carts in marts, assisting visually impaired customers in locating items and shopping independently
<iframe width="560" height="315" src="https://www.youtube.com/embed/gzfZvT5ImeY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
Designed and built hardware and software from scratch to prototype a robotic shopping cart, tested in 5 Targets, 2 Whole Foods Markets.
1.	Simulation  
Created a Gazebo simulation of a mart-like environment to test mapping and localization performance with various LiDAR settings before purchasing. Learned that LiDAR range significantly impacts localization in large spaces like marts.
2.	Differential driving Model    
Due to the crowded mart environment, I selected a differential drive model for better maneuverability over an Ackerman model. Purchased 4 wheels, 4 motor drivers, and implemented RS232 and a 4-wheel differential drive system.
3.	PID  
Added and tuned a PI controller to reduce oscillation and filtered out irregular signals from the motor driver.
4.	Odometry   
Initially used wheel encoders for odometry, but they produced unstable results. Switched to LiDAR-based odometry (laser_scan_matcher), which performed well. I also tested ICP odometry with Kinect V2, but it caused interference with the LiDAR, leading to instability.
5.	IMU and TF   
Chose the BNO055 for its ease of setup and used the tf package to define the coordinate frames for the LiDAR, IMU, and robot base.
6.	Mapping and localization  
Compared Cartographer, Gmapping, and Hector SLAM for 2D mapping, and A-LOAM for 3D mapping. The 30m range 2D LiDAR caused loop closure errors and map distortion due to accumulated errors and lack of features. To resolve this, I purchased the Velodyne VLP-16 (100m range) and projected its 3D point cloud into a 2D map, which improved accuracy. To reduce dynamic object interference, mapping was conducted near opening hours with the robot paused when people passed by. Final pathway noise was manually cleaned up using Photoshop. Finally, localization was achieved using 2D LiDAR with AMCL.
7.	Local Plannner   
Tuned parameters for DWA and TEB local planners. While DWA generally performed better, it slowed during complex maneuvers requiring both rotation and translation. Added two ultrasonic sensors to detect fallen floor items for costmap updates, which the 2D LiDAR missed.
8.	Move Base  
When the robot got stuck, traditional move_base struggled with recovery. I switched to move_base_flex and customized the move_base package, allowing the use of multiple recovery behaviors and planners.

&nbsp;
## Learn to avoid through Reinforcement Learning
This project aims to train(DQN, PPO) drone to avoid moving obstacles. I achieved this goal by making Unity(C#) environment and figured that even drone could avoid in stochastic environment(trained without wind, tested with wind). 
1. Used 7 coordinates (ball position, velocity, and drone position) as state input, trained with a 0.99 gamma, achieving a 99% avoidance rate without wind effects during training or testing.
![RL_collision_avoidance1](https://github.com/user-attachments/assets/faa70808-9ee9-4d40-a595-0c79861b0939)
2. Introduced wind during testing, and the drone maintained a 97% avoidance rate. The ball's random direction changes were handled by the drone adjusting its decision after the ball passed halfway, as the Q-function was more influenced at this stage due to the 0.99 gamma.
![RL_collision_avoidance2](https://github.com/user-attachments/assets/2e08d200-49ff-4dd2-88a9-859f4990d109)
3. Image pixel was given as input.
![RL_collision_avoidance3](https://github.com/user-attachments/assets/91f57fd7-5d1e-4ef0-90f9-fa367dfbc054)
4. To bridge the gap between simulation and reality, adversarial noise was added to simulations to mimic real-world conditions. Consistency loss was applied to ensure robustness by generating a single noise image per scene.
<iframe width="560" height="315" src="https://www.youtube.com/embed/_IH0HoHp17U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  

&nbsp;
## Haptic Watch for Visually Impaired to Grab Object 
This project developed a haptic watch to assist the visually impaired in grasping desired objects. I implemented object detection using SSD and TensorFlow Lite on a Raspberry Pi 3 with Coral Edge TPU to achieve 10Hz actuation. The object's center was divided into five regions (left, right, up, down, forward), triggering vibrations in the corresponding direction. Additionally, I created a mobile app with Google Voice-to-Text for user input.
<img align="left" width="280" height="200" src="https://user-images.githubusercontent.com/34183439/71782272-a644d300-301b-11ea-8e91-d4c35b7a0a4c.JPG">
<img width="280" height="200" src="https://user-images.githubusercontent.com/34183439/71782296-e99f4180-301b-11ea-8ef9-843424a1dd9e.JPG">
<iframe width="560" height="315" src="https://www.youtube.com/embed/StuMvEEdssI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  

&nbsp;
## Vision based EKF pose estimator
This project estimates 3D pose from image data using EKF with outlier rejection via a low-pass filter and RANSAC.
![image](https://github.com/user-attachments/assets/58e9cf6c-a8aa-4a65-bdb9-e96b4bf23538)
[Report](https://github.com/droneRL2020/Camera_based_pose_estimation_and_localization/blob/master/Mobility_Report_Project_2.pdf)
