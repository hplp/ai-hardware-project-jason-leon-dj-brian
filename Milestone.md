## Team Name:
Head Hunters
## Team Members:
- Jason Nguyen
- Brian Boner
- Leon Vaughan
- DJ Veliadis

## Project Title: 
TinyFaces: Real-Time Face Recognition on Arduino

## Milestone 1: 
In this milestone, you will provide the URL of your repo (which reflects the progress) or a PDF document for your progress on November 26th.

If you provide the link to your repo, create an explicit section (or folder) for the milestone. You can provide the link directly to that section.

In order to be able to use the Arduino Tiny ML kit, we first needed to download the latest version of the Arduino IDE and a Python version above 3.6 (we downloaded 3.12.7 specifically)
We found a repository (https://github.com/edgeimpulse/workshop-arduino-tinyml-roshambo.git) with code available for use under the Apache License 2.0, and used that to capture our images. After cloning the repository to our local machines, and navigating to the project's root, we need to run ```python3 -m pip install Pillow pyserial``` in order to have the dependencies we need in order to run ```python3 -m pip install Pillow pyserial```

**Let's provide the link to this specific section when we're done.**

Your progress should reflect the following by providing screenshots, photos, and instructions.


## Set up your hardware (if applicable)

**Provide a picture of the arduino set up on Brian's laptop**

## Identify (or train) your model 

**In order to train our model, we first had to use the code in the "program your hardware" section to access the arduino camera. Once accessed, we took multiple pictures of each group member at different angles and with different facial expressions. All photos taken for a specific group member was labeled as a class of their name. When our model recognizes any one of our faces, the green LED on the arduino board should be activated and the name of the specific group member should be printed in the console. In order to show that our program is capable of facial recognition in general, we're using a random dataset online containing 170 images of different people, which we will label as "random." This is so that the program can recognize in real time when someone's face is in the frame that isn't one of the group members'. When this occurs, the label "random" should be printed in the console and the red LED should be activated. Lastly, we created a dataset of no faces by taking many pictures of random, every day objects and walls. We will label this set as "no face recgonized," which will be printed to console when our program does not detect any faces in real time. The LED will not be activated when this occurs to show that the program is able to distinguish between real human faces and no faces. 

## Program your hardware

**Provide an explanation of the repository we found and used to allow us to access the arduino camera**

## Run the first iterations to test the computation module in your system.



## Respond to the feedback in the repo.

**This looks like something we will do after they give us feedback, not sure we need anything on this for now unless it's talking about the proposal feedback?**
