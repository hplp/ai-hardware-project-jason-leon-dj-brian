[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=16838356)

# TinyFaces Final Report

## Team Name: 
Head Hunters

## Team Members:
- Jason Nguyen
- Brian Boner
- Leon Vaughan
- DJ Veliadis

## Introduction and Setup
(Intro to project)

We used the Arduino Nano 33 BLE Sense Board and the OV7675 camera from the Arduino TinyML kit. (include picture below) 

To complete this project, we used multiple free software tools.
- [Arduino IDE][arduino_website] (Follow instructions to download)
- [Google Colab][colab_website] (Requires free google account)
- [Edge Impulse][impulse_website] (Create free account to use)
- [Python](https://www.python.org/downloads/) (We used Python v3.12.7)
- Python Pillow and pyserial packages (run installation command in command prompt/terminal)

```shell
python3 -m pip install Pillow pyserial
```

> If you do not have pip installed, you will need to [install it](https://pip.pypa.io/en/stable/installation/).

To follow along with the project, you will need to download the files below
- [Serial Communication with OV7675 camera](Arduino_OV767X.zip)
- [Arduino Image Capture](nano33_tinyml_kit_image_serial.ino)
- [Base64 Image Data Format](base64.h)
- [Python Image Capture](serial-image-catpure.py)
- [Data Augmentation Jupyter Notebook](ei-image-augmentation.ipynb)
- [Live Image Classification](nano33_camera_live_inference.ino)

## Image Capture
To capture images, we 

## Data Augmentation


## Model Training


## Setup Live Image Classification


## Testing and Results


[arduino_website]:https://www.arduino.cc/en/software
[colab_website]:https://colab.research.google.com/
[impulse_website]:https://edgeimpulse.com/
