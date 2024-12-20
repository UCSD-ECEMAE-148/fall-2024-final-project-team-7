<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://jacobsschool.ucsd.edu/">
    <img src="images\UCSDLogo_JSOE_BlueGold.png" alt="Logo" width="400" height="100">
  </a>
<h3>ECE/MAE148 Final Project</h3>
<p>
Team 7 Fall 2024
</p>
</div>

<h2><b>Table of Contents</b></h2>
<ul>
  <li><a href="#team-members">Team Members</a></li>
  <li><a href="#final-project">Final Project</a></li>
  <li><a href="#original-goals">Original Goals</a></li>
  <li><a href="#goals-we-met">Goals We Met</a></li>
  <li><a href="#our-hopes-and-dreams">Our Hopes and Dreams</a></li>
  <li><a href="#stretch-goals">Stretch Goals</a></li>
  <li><a href="#final-project-videos">Final Project Videos</a></li>
  <li><a href="#cad-parts">CAD Parts</a></li>
  <li><a href="#final-assembly">Final Assembly</a></li>
  <li><a href="#">Hardware</a></li>
  <li><a href="#software-design">Software Design</a></li>
  <li><a href="#gantt-chart">Gantt Chart</a></li>
  <li><a href="#course-deliverables">Course Deliverables</a></li>
  <li><a href="#acknowledgments">Acknowledgments</a></li>
  <li><a href="#contact">Contact</a></li>
</ul>

## Team Members

<li>Jeffrey Bratman - Aerospace Engineering</li>
<li>Christoph Bach - Mechanical Engineering</li>
<li>Ashlee Young - Electrical Engineering</li>

## Final Project

This project utilizes the DepthAI Toolbox in the robocar framework to identify a person and follow them until an ArUco marker is shown. If a valid marker is shown, a green light is flashed on the LCD screen and the car will back up and make a u-turn to identify another person. If an invalid marker is shown, a red light is flashed on the LCD screen and the car will continue to follow the person until a valid marker is detected.

---

### Original Goals

The original goal for this project was to have a car that patrols an area using a predetermined path and upon detecting a human, follow them until a valid ID is shown.

---

### Goals We Met

1. **ArUco Marker Detection**  
   Using an OAKD-Lite Camera and the DepthAI Toolbox, we successfully detected ArUco markers from the `aruco.DICT_4X4_50` dictionary. An Arduino-controlled LCD screen indicates the detection status:

   - **Blue:** Waiting for detection.
   - **Green:** Valid marker detected.
   - **Red:** Invalid marker detected.

2. **Person Detection**  
   Using the DepthAI Toolbox, the system detects people up to 6 meters away. When a person is detected, the car follows them by dynamically adjusting its speed and steering. This detection capability integrates real-time depth data and RGB video streaming.

3. **Dynamic Response to Markers**  
   Once an accepted ArUco marker is detected:
   - The car halts, flashes a green light on the LCD screen, and backs up.
   - It then switches its mode to search for another human to follow.  
   
---
### Our Hopes and Dreams
Our dream goal was a patrouling function in our car. It should drive around in a specified area and come up to a person once recognized. After scanning a correct AruCo Marker it should go back to patrouling

---

### Stretch Goals

- **GPS Integration**  
  Enabling the car to follow a predefined route with waypoint precision.
- **Enhanced Object Avoidance**  
  Using an additional camera or LiDAR for safer navigation in environments with dynamic obstacles.

---

## Final Project Videos

[![LCD Aruco Verification](images/lcd_aruco_verification.gif)](images/lcd_aruco_verification.mp4)
[![Driving Car](images/Driving_car_size_adjusted.gif)](images/Driving_car.MOV)

### CAD Parts

<div align="center">

**Main Mounting Plate**

![Main Mounting Plate](images/IMG1-main_mounting_plate.png "Main Mounting Plate")

**Jetson and DC-DC Converter Mount**

![Jetson and DC-DC Converter Mount](images/Jetson_Mount.png "Jetson Mounting Plate")

**Combined Camera and LIDAR Mount**

![Combined Camera and LIDAR Mount](images/IMG2-combined_lidar_camera_mount.png "Combined Camera and LIDAR Mount")

**Camera Mount**

![Main Mounting Plate](images/IMG3-camera_mount.png "Camera Mount")

**LCD Mount**

![Combined Camera and LIDAR Mount](images/IMG4-LCD_mount.png "LCD Mount")

</div>

---

### Final Assembly
![Final Car](images/IMG_8206.JPG "Final Car")

---

### Hardware
- Jetson NANO
- Arduino NANO
- OAK-D Camera
- Waveshare 2" LCD

<div align="center">
  
**Wiring Diagram**

![Wiring Diagram](images/wiring_diagram.png "Wiring Diagram")

**Arduino** 

![Arduino](images/arduino.png "Arduino")

</div>
---

### Software Design

#### ROS2 Nodes

The project leverages ROS2 with a custom node called `CameraControlNode` to handle:

1. **Person Detection:**  
   Uses DepthAI's spatial neural network to detect people and estimate their 3D position.
2. **Navigation:**  
   Dynamically adjusts speed and direction to track the detected person.
3. **ArUco Marker Recognition:**  
   Detects and processes ArUco markers to determine the next course of action.

#### DepthAI Pipeline

The DepthAI pipeline enables real-time computer vision by combining:

- **Color Camera:** Captures high-resolution images for visualization and object detection.
- **Mono Cameras:** Generate stereo depth perception using grayscale images.
- **Stereo Depth Module:** Computes depth maps and provides 3D coordinates of detected objects.
- **MobileNet-SSD Neural Network:** Processes RGB frames for object detection and spatial localization.
- **Output Queues:** Streams processed data to the host application.

#### ROS2 Topics

- `/person_detection`: Publishes detected person data, including their spatial position.
- `/aruco_markers`: Shares information about detected ArUco markers.
- `/cmd_vel`: Issues velocity commands for dynamic navigation.

#### Arduino Communication

The Arduino facilitates communication via serial commands:

- `"yes"`: Valid marker detected.
- `"no"`: Invalid marker detected.
- `"waiting"`: No marker detected.

---

### Gantt Chart

![Gantt Chart](images/Gantt_Chart_Final_v2.png "Gantt Chart")

---

### Course Deliverables

[![Course Deliverables](./images/course_deliverables.png)](https://drive.google.com/drive/folders/19BW6AHKIXl78ZI0pPDGdtria1HKv7pat?usp=drive_link)

---

### Acknowledgements

Special thanks to Professor Jack Silberman, Winston, and Alexander for an amazing Fall 2024 Class.

---

### Contact
<li>Jeff | jbratman@ucsd.edu</li>
<li>Chris | chris.bach@tum.de</li>
<li>Ashlee | asy001@ucsd.edu</li>
