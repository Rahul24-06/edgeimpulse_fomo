# Edge Impulse FOMO 

![FOMO](https://hackster.imgix.net/uploads/attachments/1454152/_nskAWxaGUv.blob?auto=compress%2Cformat&w=900&h=675&fit=min)

Object detection models are vital for many computer vision applications. They can show where an object is in a video stream or allow you to count the number of objects detected. But they’re also very resource-intensive— models like MobileNet SSD can analyze a few frames per second on a Raspberry Pi 4, using a significant amount of RAM. This has put object detection out of reach for the most interesting devices: microcontrollers. Microcontrollers are cheap, small, ubiquitous, and energy-efficient—and are thus attractive for adding computer vision to everyday devices. But microcontrollers are also very resource-constrained, with clock speeds as low as 200 MHz and less than 256 Kbytes of RAM—far too little to run complex object, detection models. But… that has now changed! We have developed FOMO (“faster objects, more objects”), a novel DNN architecture for object detection, designed from the ground up to run on microcontrollers.

![Live Classification](https://hackster.imgix.net/uploads/attachments/1454163/screenshot_20220607-232109_chrome_IxyBJTYaWK.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)


Sensor & Block Information
* Camera module with input images 160 x 160 pixels
* An image block to normalize the image data, and reduce the color depth to grayscale
* FOMO transfer learning block-based on MobileNetV2 0.35

## Data Collection
To collect the data, we need to connect a device that can collect the images. For this project, we will be using Android mobile. Click on the Devices tab, and connect the mobile using the QR code.

![Connected to mobile](https://hackster.imgix.net/uploads/attachments/1454164/screenshot_20220607-162853_chrome_l4zvHRVgwU.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

Now select the Label as IC, LED, and Resistors respectively, and click the Capture button to collect the image data.

![Data acquisition - LED](https://hackster.imgix.net/uploads/attachments/1454167/screenshot_20220607-163957_chrome_d7alunlbil.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

![Data acquisition - IC](https://hackster.imgix.net/uploads/attachments/1454165/screenshot_20220607-163312_chrome_ktz7nyO8QW.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

![Data acquisition - RESISTOR](https://hackster.imgix.net/uploads/attachments/1454166/screenshot_20220607-163516_chrome_xlzA3OyRps.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)


## Design an impulse
Now we had collected the dataset for Training and Testing. We use 80% of the data for training and the rest 20% of the data for testing the model.

![Data acquisition](https://hackster.imgix.net/uploads/attachments/1454172/ss1_7vg9kRJygz.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Now we have to label the data on the images as shown below.

![Labeling data - Resistor](https://hackster.imgix.net/uploads/attachments/1454175/ss7_BOvHcLlpBd.png?auto=compress%2Cformat&w=740&h=555&fit=max)

![Labeling data - IC](https://hackster.imgix.net/uploads/attachments/1454176/ss6_aA1MUVk92T.png?auto=compress%2Cformat&w=740&h=555&fit=max)

We correct the data collected to 80% train and 20% test split by moving the data from train to test dataset or vice-versa. In this example, we have got an 80% / 20% split here.

![80% 20% train/test data](https://hackster.imgix.net/uploads/attachments/1454193/ss11_LxS3EfMgoW.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Next, we create an impulse by selecting the Image data, processing block, learning block, and output features. 
* We have used 160x160 images
* Add Image processing block
* Add the learning block generated from the previous steps
* We have 3 output features (IC, Led, Resistors)

![Create impulse](https://hackster.imgix.net/uploads/attachments/1454201/ss12_m4LS4Oqcx4.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Next, we generate features by clicking the Generate Features button. This takes a few seconds to generate the features. Feature explorer explains the relation between the three features ( IC, Led, Resistor).

![Generate Features](https://hackster.imgix.net/uploads/attachments/1454205/ss14_JA82AUAVF5.png?auto=compress%2Cformat&w=740&h=555&fit=max)

We set the parameters as shown below. Once the Training settings, click on the Training button to start training the model.

![Training](https://hackster.imgix.net/uploads/attachments/1454206/ss15_uGcjU1sOvD.png?auto=compress%2Cformat&w=740&h=555&fit=max)

We can see the training output once the training is done. The training output explains the confusion matrix, Inferencing time, RAM usage, and Flash usage. The confusing matrix has TP, TN, FP, and FN for the features (LED, Resistor, and IC).

![Training output](https://hackster.imgix.net/uploads/attachments/1454207/ss17_8LoB8ONYzR.png?auto=compress%2Cformat&w=740&h=555&fit=max)

From the above training output, we can find the F1 score as 96.7% for the quantized (int8) model which is a decent output of an object detection model. The Flash usage is 77.6K which can be deployed to an edge device easily.

## Deploy
Now let's deploy and test them on the phone. Click on the Deployment and click on connect to mobile phone tile. Scan the QR code shown using the scanner on the mobile camera.

![Deployment](https://hackster.imgix.net/uploads/attachments/1454209/ss18_KEj73EAj9w.png?auto=compress%2Cformat&w=740&h=555&fit=max)

Once the classifier is loaded on the mobile, the inferencing is done on edge as shown below.

![Inference](https://hackster.imgix.net/uploads/attachments/1454210/screenshot_20220607-232017_chrome_GnU7KDCsIm.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

![Inference](https://hackster.imgix.net/uploads/attachments/1454211/screenshot_20220607-231937_chrome_7SyPWuZdi4.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

![Inference](https://hackster.imgix.net/uploads/attachments/1454212/screenshot_20220607-232004_chrome_PSajzw8mIW.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

![Inference](https://hackster.imgix.net/uploads/attachments/1454213/screenshot_20220607-232109_chrome_DM5sWv1o38.jpg?auto=compress%2Cformat&w=740&h=555&fit=max)

If you faced any issues in building this project, feel free to ask me. Please do suggest new projects that you want me to do next.

Give a thumbs up if it really helped you and do follow my channel for interesting projects. :)

Share this project if you like.

Github - https://github.com/Rahul24-06/

Happy to have you subscribed: https://www.youtube.com/c/rahulkhanna24june?sub_confirmation=1

Thanks for reading!
