# Advanced Computer Engineering Project

## Software and Hardware used
Hardware used for this project: 
 - [x] Single Board Computers : Raspberry Pi, Jetson Nanos, Odriod
 - [x] Two Robotic Arms
 - [x] Range of sensors and actuator
                                
Software used for this project: Python

## Quick Install
To get started, you will need to download this repository to do so, download GitHub onto your raspberry pi using the following command:

```bash
sudo get install git -y
```
When this is complete, clone the relevant branches to the relevant Pis. Use this command to do so:
```bash
git clone github.com/da5905p/UoGACE/--BRANCH NAME--
```
*Where you change --BRANCH NAME-- for the relevenat branch i.e. Network, GUI.*

Note: Not all Pis need all branches to function. The list of which pis are required for which systems are below.

TouchScreen Pi = GUI, Network  
moonBuggy Pi = moonBuggy, Visual, Network  
Bases = Arm, Visual, Network  

## Description
This project consisted in creating software and assembling hardware in order to make an Arm and a Car that could be used working together, automated or remotely controlled, where the Car/Rover would be transporting objects which can be thought as resources for examination in another planet or resources needed to work in different colonies. The Arm would be a standing tool that took any objects from the transports to a storage.

The project was sectioned in multiple branches and multiple teams which received a small task to reach the final result. There are 8 branches: moonBuggy, Arm, Network, Visual, GUI, baseNavigation, testBranch and Environment-&-Dependancies branch. The main goal of this project was to use the available hardware to design and program a functionable robot which, as a short brief, will be able to use movement functions for the base and it will move around collecting an object from the storage and it will be able to grab that object and deposit it onto the car and also from the car to the storage. 

Everything can be controlled using a keyboard however, in future iterations of the project it is possible to make full use of the pygame library in order to instead use joysticks or an application on a tablet.

An image of the robot after it was put together will be attached:

![image](https://user-images.githubusercontent.com/75362937/112773379-c94b1080-902d-11eb-881e-bcc51d90ea0e.png)

### Arm Control
The main purpose of the Arm branch was to develop a code which will give the user the possiblity to control the arm remotely. The arm is able to rotate in any direction, rise up and down and different other functions. At the end of the physical arm, a claw is present which will be used to grab and also drop things from a certain location to another location, which is the storage, and vice versa.

There are different movements possible: GripsOpen, GripsClose, WristUp, WristDown, ElbowUp, ElbowDown, ShoulderUp, ShoulderDown, Stop etc. 

As an example: 

```bash
>>> arm.move(usb_arm.GripsOpen)
```
The grips will open.

Programmed sequence of actions can be created for this, these sequences being multiple arrays of commands as seen in the following example:

```bash
rotate = [[usb_arm.BaseCtrClockWise,7],[usb_arm.GripsOpen],[usb_arm.BaseClockWise,6.8]]
```

And to run the action: 

```bash
arm.doActions(rotate)
```

### Image Detection
OpenCV is a Python libarary that was used to solve computer vision problems. The team was provided with a camera which will be used to take the RGB colours description of the object and find the HSV colours. To install the OpenCV, install_opencv.sh will need to be run; all the libraries and dependencies will be installed using that file:

```bash
sudo apt-get install -y libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
```

Test files are provided to test if the camera is working properly.

For more informations regarding the Image Detection branch, follow this link: https://github.com/da5905p/UoGACE/tree/Visual/GUI

### Network 
This branch will allow the different devices to connect with each other and at the same time, whenever a device is sending information it will encrypt it and when it receives it, it will decrypt it. The Network is one of the most important one since it makes the whole system working together possible. 

To assure the security of the network, the use of crypthographic keys was necessary. For this project, Fernet was used to provide the keys, this being an implementation of symmetric authenticated cryptography:

```bash
from cryptography.fernet import Fernet
key = Fernet.generate_key()
```

The command will provide a URL-safe base64-encoded 32-byte key.

### Moonbuggy
There are different scripts for this branch: one being a key control which will permit the use of the robot by keyboard (movement, turning); the autonomous script which represents the obstacle avoidance (it is using the infrared sensor to check if there is any object in a range of 5 cm that needs to be avoided). If an object is detected, it will stop and move either left or right, after deciding which path is clear. 

Another script named Path correction was implemented. It has two sensors on both side of the wheels and by the use of this you can tell if the number of turns on each wheel does not balance. If there is a difference of more than 3 turns, the script will make the robot stop and then turn the opposite side.

As for the last script is the one that uses the light following sensors; it sees the tape on the floor and it will do a 180 degrees turn and backs into the parking bay that is marked up with tape.

![image](https://user-images.githubusercontent.com/75362937/112965346-166bd700-9141-11eb-91ec-d37bd28efe00.png)

### GUI
The graphical user interface was devloped to allow different users to sign in and control different aspects of the projects such as: movement control of the buggy, movement control of the arm or turning the camera. 

There are different commands that can be used such as: the login button, sign out button, network status & system status, report issue (used to report any issues that the user may face when using the robot) and emergency which is a button that will be used to ensure safety of the system when something goes wrong. 

A link to the wireframe design for the GUI can be found here: https://framer.com/share/ACE-GUI--uqXDT6NO8jMDT6XoKdXz/Aj17HOaoW

## Authors and aknowledgements
The project was developed by: 
 - [x] Arm Branch: Md Jafrul Hasan Tufael, Joao Pedro P Dos Reis, Goncalo Alexandre Nunes, Joan Garcia Castro, Blanca Urechiatu.
 - [x] MoonBuggy Branch: Naa A Kotey.
 - [x] Network Branch: David E Ansa.
 - [x] Visual Branch: Maher Qawash, Ravi Kumar, Shahd R A F Aldaihani, Ross K Barret.
 - [x] GUI Branch: David E Ansa, Regan J Smith, Marwan Jamal.


