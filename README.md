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
To train the model to recognize your faces, you needed to capture images of hyour faces on the OV767X camera. You can use the following files to do so (should we include original repo?):
- [Serial Communication with OV7675 camera](Arduino_OV767X.zip)
- [Arduino Image Capture](nano33_tinyml_kit_image_serial.ino)
- [Base64 Image Data Format](base64.h)
- [Python Image Capture](serial-image-catpure.py)

After these files are on your computer, open the Arduino IDE. 
In the Arduino IDE, **Sketch > Include Library > Add .ZIP Librar...**. Select **Arduino_OV767X.zip** file. This library is required for the Arduino Nano 33 BLE Sense to communicate with the camera on the TinyML kit.

Next, go to **File > Open...** and open the sketch **(YourFilePath)/nano33_tinyml_kit_image_serial.ino**. This file will capture, scale and crop the image and output it as Base64 data. 

Plug the Arduino Nano 33 BLE Sense board into your computer and make sure the board/port show up in the IDE

Compile and upload the sketch to the board (**Sketch > Upload**)
You should see "Done" if your program uploaded successfully.

Open a terminal or command prompt window and navigate to the directory that contains the Python Serial Image Captrue script. Example (windows):

```shell
chdir Downloads/tinyml-project/
```

Install [PySerial](https://pyserial.readthedocs.io/en/latest/) and [Pillow](https://pillow.readthedocs.io/en/stable/) Python packages if you have not already done so

```shell
python3 -m pip install Pillow pyserial
```

Run the [Serial Image Capture Python](serial-image-catpure.py) script:

```shell
python3 serial-image-capture.py
```

> **Troubleshooting**
> If you see an error like `No module named '_tkinter'`, it means that (for some reason) Python was not installed with the tkinter package. You will need to install it with `brew install python-tk` (macOS), `python3 -m pip install tk` (Windows and Linux).

From the **Port** drop-down menu, select the serial port associated with your Arduino board (check with the Arduino IDE to verify the port).

Press **Connect**. You should see a live view of the Arduino camera. Click *Embiggen view* to make the image bigger. Due to the slow nature of converting and transmitting raw image data over a serial connection, do not expect more than a few frames per second.

Now, setup the camera such that only your face is visible in the live view of the Arduino camera. Enter your name in the box next to *Label* to set the label of the image to your name. Click **Save Image** to save the image to the directory that the Python script is in. Capture at least 50 images, slightly altering where you appear in the frame and how your head is oriented to create as full of a dataset as possible. Repeat this process for each person that you want to identify (try to keep the 
## Data Augmentation (Optional)


## Model Training


## Setup Live Image Classification


## Testing and Results


[arduino_website]:https://www.arduino.cc/en/software
[colab_website]:https://colab.research.google.com/
[impulse_website]:https://edgeimpulse.com/
