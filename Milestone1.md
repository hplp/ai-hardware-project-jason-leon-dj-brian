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

**Let's provide the link to this specific section when we're done.**

Your progress should reflect the following by providing screenshots, photos, and instructions.


## Set up your hardware (if applicable)
Below is an image of how our hardware was set up, being plugged in via micro USB cable to the Arduino Nano board which was seated into the expansion board to connect with the camera. From there the hardware was controlled directly through the Arduino IDE.
<img width="372" alt="image" src="https://github.com/user-attachments/assets/5ea36b3e-2d8e-4091-87d5-d3741110cc72">


## Identify (or train) your model 

**In order to train our model, we first had to use the code in the "program your hardware" section of this repo (https://github.com/edgeimpulse/workshop-arduino-tinyml-roshambo) to access the arduino camera. Once accessed, we took multiple pictures of each group member at different angles and with different facial expressions. All photos taken for a specific group member was labeled as a class of their name. When our model recognizes any one of our faces, the green LED on the arduino board should be activated and the name of the specific group member should be printed in the console. In order to show that our program is capable of facial recognition in general, we're using a random dataset online containing 170 images of different people, which we will label as "_face". This is so that the program can recognize in real time when someone's face is in the frame that isn't one of the group members'. When this occurs, the label "random" should be printed in the console and the red LED should be activated. Lastly, we created a dataset of no faces by taking many pictures of random, every day objects and walls. We will label this set as "_background", which will be printed to console when our program does not detect any faces in real time. The LED will not be activated when this occurs to show that the program is able to distinguish between real human faces and no faces.

Using the pictures that we took and the dataset of random faces that we used, we scaled, translated, and flipped the images to create a larger training dataset. After finalizing the training dataset, we set aside 20% of the images for validation and uploaded the training/validation datasets to Edge Impulse (https://edgeimpulse.com/) to train our model. Edge Impulse allowed us to create a model that could be implemented on the Arduino TinyML board.**

## Program your hardware
**In order to be able to use the Arduino Tiny ML kit, we first needed to download the latest version of the Arduino IDE and a Python version above 3.6 (we downloaded 3.12.7 specifically)
We found a repository (https://github.com/edgeimpulse/workshop-arduino-tinyml-roshambo.git) with code available for use under the Apache License 2.0, and used that to capture our images. After cloning the repository to our local machines, and navigating to the project's root, we need to run ```python3 -m pip install Pillow pyserial``` in order to have the dependencies we need in order to run ```python3 serial-image-capture.py```**

## Run the first iterations to test the computation module in your system.
We were unable to test how the AI model worked live when trying to recognize our faces versus others' faces or background details due to having to share our hardware but we'll be able to validate its functionality in our next milestone. At this stage we're very confident that the work we've done will be able to function correctly with some minor tweaking once we get the board back.

## Respond to the feedback in the repo.
We are very pleased with the positive feedback we've received by our peers directly below. The source of the data that is to be used in the training is directly from the arduino camera, as well as a database online containing hundreds of random faces. We have verified that the model size does fit our hardware. Additionally, our expected outcome of this entire project is to have our program be able to distinguish between our group members, the random faces online, and no faces through proper facial recognition. 

**Feedback received on proposal presentation assignment:** 
- "Everything was very clearly defined and laid out" - James Chun
- "Great presentation!" - Michael Sekyi
- "Cool project! I like the scope of the project and the specificity of your objectives, excited to see the results!" - Andy Chen
- "Looks good, all parts of proposal covered. The project is promising but realistic." - Kyle Clemente
- "Exciting project! The proposal looks decent. The application is interesting. Try to idendify the source of the data that is to be used in the training and place it to Github. Verify the model size fits to the hardware. If you are going to share the hardware, contact with the group who you will share the hardware with." - Tongxuan Tian
- "Strong proposal with a lot of detail on the objectives in terms of what kinds of specific features are being portrayed and how they will be evaluated. Expected outcomes can be improved by describing a more concrete output or deliverable as the ultimate goal." - Davis Wang
- "Very unique project! I've always wondered how these systems within our phones were so accurate, to be able to distinguish between similar facial features, so I am looking forward to the final results and demo of this project. The timeline looks reasonable and they seem capable of bringing this in on time during their presentation." - Phi Lu
