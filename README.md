# FOMO Resistor, IC, and LED 160x160

![FOMO](https://hackster.imgix.net/uploads/attachments/1454152/_nskAWxaGUv.blob?auto=compress%2Cformat&w=900&h=675&fit=min)


## Introduction
Have you ever tried opening a circuit board and had no clue what it is? Well, I have got you a solution. With a mobile phone and edge impulse, you can run a trained object detection model to identify the electrical components (Resistor, Capacitors, IC, etc)

Object detection models are vital for many computer vision applications. They can show where an object is in a video stream or allow you to count the number of objects detected. But they’re also very resource-intensive— models like MobileNet SSD can analyze a few frames per second on a Raspberry Pi 4, using a significant amount of RAM. This has put object detection out of reach for the most interesting devices: microcontrollers. Microcontrollers are cheap, small, ubiquitous, and energy-efficient—and are thus attractive for adding computer vision to everyday devices. But microcontrollers are also very resource-constrained, with clock speeds as low as 200 MHz and less than 256 Kbytes of RAM—far too little to run complex object, detection models. But… that has now changed! We have developed FOMO (“faster objects, more objects”), a novel DNN architecture for object detection, designed from the ground up to run on microcontrollers.

Sensor & Block Information
* Camera module with input images 160 x 160 pixels
* An image block to normalize the image data, and reduce the color depth to grayscale
* FOMO transfer learning block-based on MobileNetV2 0.35

![Live Classification](https://hackster.imgix.net/uploads/attachments/1454163/screenshot_20220607-232109_chrome_IxyBJTYaWK.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)


To collect the data, we need to connect a device that can collect the images. For this project, we will be using Android mobile. Click on the Devices tab, and connect the mobile using the QR code.

Now select the Label as IC, LED, and Resistors respectively, and click the Capture button to collect the image data.

Now we had collected the dataset for Training and Testing. We use 80% of the data for training and the rest 20% of the data for testing the model.

Now we have to label the data on the images as shown below.

We correct the data collected to 80% train and 20% test split by moving the data from train to test dataset or vice-versa. In this example, we have got an 80% / 20% split here.

![Create impulse](https://hackster.imgix.net/uploads/attachments/1454201/ss12_m4LS4Oqcx4.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Next, we generate features by clicking the Generate Features button. This takes a few seconds to generate the features. Feature explorer explains the relation between the three features ( IC, Led, Resistor).


We set the parameters as shown below. Once the Training settings, click on the Training button to start training the model.


We can see the training output once the training is done. The training output explains the confusion matrix, Inferencing time, RAM usage, and Flash usage. The confusing matrix has TP, TN, FP, and FN for the features (LED, Resistor, and IC).

![Training output](https://hackster.imgix.net/uploads/attachments/1454207/ss17_8LoB8ONYzR.png?auto=compress%2Cformat&w=740&h=555&fit=max)

From the above training output, we can find the F1 score as 96.7% for the quantized (int8) model which is a decent output of an object detection model. The Flash usage is 77.6K which can be deployed to an edge device easily.

## Deploy
Now let's deploy and test them on the phone. Click on the Deployment and click on connect to mobile phone tile. Scan the QR code shown using the scanner on the mobile camera.

Once the classifier is loaded on the mobile, the inferencing is done on edge as shown below.

![Inference](https://hackster.imgix.net/uploads/attachments/1454210/screenshot_20220607-232017_chrome_GnU7KDCsIm.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)


![Inference](https://hackster.imgix.net/uploads/attachments/1454213/screenshot_20220607-232109_chrome_DM5sWv1o38.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)



You can find the detailed explanation and tutorial on my [Hackster profile](https://www.hackster.io/rahulkhanna). 

Happy to have you subscribed:  [Youtube](https://www.youtube.com/c/rahulkhanna24june?sub_confirmation=1)

Thanks for reading!
