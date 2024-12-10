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

Now, setup the camera such that only your face is visible in the live view of the Arduino camera. Enter your name in the box next to *Label* to set the label of the image to your name. Click **Save Image** to save the image to the directory that the Python script is in. Capture at least 50 images, slightly altering where you appear in the frame and how your head is oriented to create as full of a dataset as possible. Repeat this process for each person that you want to identify (try to keep the number of different people small).

Capture at least 50 images of the background with the label *_background* so the model can recognize when a face does not appear within the frame. 

After all images are capture, add them to a single .zip file. In Windows you can do this by highlighting all of your image files and Right-Clicking **Send to > Compressed (zipped) folder** name the .zip file **dataset.zip**. 

## Data Augmentation (Optional)
If you are not able to capture enough data to train the model, you can alter each image to create a larger dataset. To do this, you can use the provided [jupyter notebook](ei-image-augmentation.ipynb). 

Once you have the notebook downloaded, open [Google Colab](colab_website)

Run the first code cell (press **shift + enter** to run cells) to install Node.js. You might see a pop-up warning you that the Notebook is not authored by Google. Click **OK**.

While that cell is running, click on the *folder* icon on the left-side pane to open the file browser pane. Right-click (or click the *upload* icon) to upload a file to the Notebook. Select your **dataset.zip** and click **Open**. This will upload your original dataset.

Go to [edgeimpulse.com](https://edgeimpulse.com/). Create an account if you have not already done so. Click **Login** and click **Create new project**.

Click on **Dashboard** and click on the **Keys** tab. Double-click to highlight the entire API key and copy it (don't worry if you can't see the whole key, it will be copied).

Head back to the Google Colab script. Continue running cells until you get to the `### Settings` cell. Overwrite the value of the `EI_API_KEY` string with the API key you copied from your project.

Continue running cells. The script performs the following actions:

 * Extracts your *dataset.zip* into the */content/dataset/* folder
 * Generates new images based on each original image: flipped, rotated, zoomed, translated, noise added
 * Zips the new dataset (including augmentations) into *out-augmented.zip* if you would like to download it
 * Uploads the full dataset to Edge Impulse, automatically splitting between training and test sets

If you head to the *Data acquisition* page in your Edge Impulse project, you should see your fully augmented dataset split between the *Training data* and *Test data* tabs. Note that some images might not be uploaded: Edge Impulse performs a deep inspection (via hashing) of each sample to ensure no two samples are the same. So, if you try to upload two images that are exactly the same, Edge Impulse will keep the first and reject the second.

## Model Training
To train the model, we used Edge Impulse, which is a free AI development platform. Edge Impulse makes it easy to create a sketch that can be added to the Arduino Nano 33 BLE Sense board. In the data augmentation section, we provided a Jupyter notebook that added the dataset to an edge impulse project. 

If you collected enough data to skip the data augmentation section, you will need to create a new [Edge Impulse](impulse_website) project. If you do not already have an account, you can create one for free. 

To upload your images to Edge Impulse, put them all in a single folder. Navigate to **Data Acquisition** and click on the *Upload Data* button. Select *Select a folder* for **Upload mode**, *Automatically split between training and testing* for **Upload into category**, and *Infer from filename* for **Label**. Next click on *choose files* and select the folder with your images. Finally, select **Upload Data** to upload your images. 

> **Note**
> The Python script that we used to capture images automatically saved each image to a file with the file name as the label followed by a unique id, which allows for Edge Impulse to label each image accurately based on the filename.

Go to your project in Edge Impulse. Go to the **Impulse design** page. Change the *Image data* resolution to be:

 * Image width: **48**
 * Image height: **48**
 * Resize mode: **Fit shortest**

Click **Add a processing block** and add the **Image** block. Click **Add a learning block** and select the **Classification** block.

Click on **Image** under *Impulse design*. Change the *Color depth* to **Grayscale**. 

Click **Save parameters** and click **Generate features** on the next page. Wait while Edge Impulse generates the training features from your dataset.

When feature extraction is complete, you should see a 2D feature explorer showing the relative separation among the class groupings along with an estimation of the time and resources required to perform feature extraction on your target device (default: Arm Cortex-M4F).

Click on **Classifier** under *Impulse design*. Change the *Number of training cycles* (epochs) to **100**. Leave everything else as default. Click **Start training**.

When training is complete, take a look at the model results. Before the training process starts, Edge Impulse automatically sets aside a random 20% of your training data for validation. The accuracy, loss, and confusion matrix are calculated based on this validation set. How well did your model perform?

Go to the **Model testing** page and click **Classify all**. This will perform inference on your test dataset and display the results.

Navigate to the **Deployment** page in your project. Edge Impulse is capable of exporting your project (feature extraction and model inference) to a number of supported hardware platforms. Note that the *C++ library* option is the most versatile: so long as your target hardware has a C++ compiler (and enough flash/RAM), you can run inference with your trained Edge Impulse model! However, the C++ library may not be optimized for some hardware (e.g. ML accelerators).

In the search bar, enter **Arduino** and select the **Arduino library** option.

Scroll down to the bottom of the page. Leave the [EON Compiler](https://www.edgeimpulse.com/blog/introducing-eon) enabled (this converts your interpreted model to C++ code to save on flash/ROM). Leave *Quantized (int8)* selected. Click **Build**

When the build process is complete, you should have an Arduino library (in .zip format) automatically downloaded to your computer. This library includes the blocks we created in the Edge Impulse Studio: feature extraction and classification (i.e. the fully trained model).


## Setup Live Image Classification
Next, we set up the Arduino Nano 33 BLE Sense board to be able to perform live image classification of our faces.

If you have not already, download the [Arduino Live Image Classification](nano33_camera_live_inference.ino) program.

Open the Arduino IDE then open the Live Image Classification script **File > Open** and navigate to the program on your computer. 

You will need to import the Edge Impulse library. Select **Sketch > Include Library > Add .ZIP Library**. Select the library that you downloaded from Edge Impulse and click **Open**.

Open **File > Examples > \<NAME_OF_LIBRARY\> > nano_ble33_sense > nano_ble33_sense_camera**. Copy the `#include` line for your library.

Replace the `#include <head-hunters_inferencing.h>` line in the live classification script with your `#include` line. 

Compile and upload the sketch to your board.

> **Note**
> This step may take a long time to complete.

Once the sketch is uploaded to your board, run the python serial image capture script again.
```shell
python3 serial-image-capture.py
```

Select the port of your Arduino board and click **Connect**. The viewer will show you what the Arduino sees. Use the same setup as you did for image collection and get in front of the OV767 camera. The terminal window should have the printed inference results. The values correspond to the prediction scores -- the highest prediction score is the classification result. 


## Testing and Results
(explain our results)

[arduino_website]:https://www.arduino.cc/en/software
[colab_website]:https://colab.research.google.com/
[impulse_website]:https://edgeimpulse.com/
