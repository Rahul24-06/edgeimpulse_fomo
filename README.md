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

We had captured 300 images of resistors, IC, and LED each of size 160x160 using Android mobile. The Labeled images are dataset for Training and Testing. We use 80% - 20% of the data for training and testing the model. We create an Impulse on the Edge impulse platfrom to generate features.

![Create impulse](https://hackster.imgix.net/uploads/attachments/1454201/ss12_m4LS4Oqcx4.png?auto=compress%2Cformat&w=740&h=555&fit=max)

With the generated features, we create an object detection model. We can see the training output once the training is done. The training output explains the confusion matrix, Inferencing time, RAM usage, and Flash usage. The confusing matrix has TP, TN, FP, and FN for the features (LED, Resistor, and IC). From the training output, we can find the F1 score as 96.7% for the quantized (int8) model which is a decent output of an object detection model. The Flash usage is 77.6K which can be deployed to an edge device easily.

![Training output](https://hackster.imgix.net/uploads/attachments/1454207/ss17_8LoB8ONYzR.png?auto=compress%2Cformat&w=740&h=555&fit=max)

We can loader the edge impulse classifier on the mobile, the inferencing is done on edge as shown below. And now we can identify resistors, led and IC on a  mobile without any knowledge on the circuit. 

![Inference](https://hackster.imgix.net/uploads/attachments/1454210/screenshot_20220607-232017_chrome_GnU7KDCsIm.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)
![Inference](https://hackster.imgix.net/uploads/attachments/1454213/screenshot_20220607-232109_chrome_DM5sWv1o38.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

You can find the detailed explanation and tutorial on my [Hackster profile](https://www.hackster.io/rahulkhanna). 

Happy to have you subscribed:  [Youtube](https://www.youtube.com/c/rahulkhanna24june?sub_confirmation=1)

Thanks for reading!
