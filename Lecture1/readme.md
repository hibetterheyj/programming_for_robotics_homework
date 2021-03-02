# Exercise1

>   [Lecture Slides (PDF, 2.4 MB)](<https://ethz.ch/content/dam/ethz/special-interest/mavt/robotics-n-intelligent-systems/rsl-dam/ROS2021/lec1/ROS Course Slides Course 1.pdf>)
>
> [Exercises (PDF, 314 KB)](<https://ethz.ch/content/dam/ethz/special-interest/mavt/robotics-n-intelligent-systems/rsl-dam/ROS2021/lec1/Exercise Session 1.pdf>)
>
> Files: [smb_common.zip (ZIP, 2.3 MB)](https://ethz.ch/content/dam/ethz/special-interest/mavt/robotics-n-intelligent-systems/rsl-dam/ROS2021/lec1/smb_common.zip)
>
> [Video Recording](https://www.youtube.com/watch?v=aL7zLnaEdAg)

1. Setup the SMB simulation:

   ```shell
   cd git
   wget https://ethz.ch/content/dam/ethz/special-interest/mavt/robotics-n-intelligent-systems/rsl-dam/ROS2021/lec1/smb_common.zip
   unzip smb_common.zip -d ./
   cd ~/Workspaces/smb_ws/src
   ln -s ~/git/smb_common/
   ls
   cd ..
   catkin build
   ```

2. Launch the simulation with roslaunch and inspect the created nodes and their topics

   ```shell
   rosnode list
   rostopic list
   rostopic echo /cmd_vel
   rostopic hz /cmd_vel
   rostopic hz /tf
   rqt_graph
   ```

3. Command a desired velocity to the robot from the terminal

   ```shell
   rostopic pub /cmd_vel geometry_msgs/Twist "linear:
     x: 1.0
     y: 0.0
     z: 0.0
   angular:
     x: 0.0
     y: 0.0
     z: 0.0"
   ```

4. Use **teleop_twist_keyboard** to control your robot using the keyboard. Find it online
   and compile it from source! Use git clone to clone the repository to the folder
   ~/git.

   ```shell
   407  cd git
   409  git clone https://github.com/ros-teleop/teleop_twist_keyboard
   410  cd ~/Workspaces/smb_ws/src/
   411  ln -s ~/git/teleop_twist_keyboard/
   413  cd ..
   414  catkin build teleop_twist_keyboard 
   415  source devel/setup.bash 
   416  roscd teleop_twist_keyboard
   417  pwd
   /home/ros/Workspaces/smb_ws/src/teleop_twist_keyboard
   ```

5. **Grading**

   - smb_gazebo_ex1.launch

     ```xml
     <?xml version="1.0" encoding="utf-8"?>
     
     <launch>
       <!-- ARGS-->
       <arg name="world" default="robocup14_spl_field" />
       <!-- Model path -->
       <arg name="model_zoo_path" default="/usr/share/gazebo-11/" />
       <arg name="world_file_path" default="$(arg model_zoo_path)/worlds/$(arg world).world" />
     
       <!--NODE-->
       <!-- 
         <node name="teleop_twist_keyboard" pkg="teleop_twist_keyboard" type="teleop_twist_keyboard" output="screen" />
       -->
     
       <!--INCLUDE-->
       <include file="$(find smb_gazebo)/launch/smb_gazebo.launch">
         <arg name="world" value="$(arg world)" />
         <arg name="world_file" value="$(arg world_file_path)" />
       </include>
     </launch>
     
     ```

   - Command

     ```shell
     cd ~/Workspaces/smb_ws/
     source devel/setup.bash
     roscd teleop_twist_keyboard/
     cd ../smb_common/smb_gazebo/launch/
     roslaunch smb_gazebo_ex1.launch
     # start a new terminal
     rosrun teleop_twist_keyboard teleop_twist_keyboard
     ```

     

   

