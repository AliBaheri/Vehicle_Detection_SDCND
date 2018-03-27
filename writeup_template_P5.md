

**Vehicle Detection Project**

The goals / steps of this project are the following:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Optionally, you can also apply a color transform and append binned color features, as well as histograms of color, to your HOG feature vector. 
* Note: for those first two steps don't forget to normalize your features and randomize a selection for training and testing.
* Implement a sliding-window technique and use your trained classifier to search for vehicles in images.
* Run your pipeline on a video stream (start with the test_video.mp4 and later implement on full project_video.mp4) and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

[//]: # (Image References)
[image1]: ./examples/car_not_car.png
[image2]: ./examples/HOG_example.jpg
[image3]: ./examples/sliding_windows.jpg
[image4]: ./examples/sliding_window.jpg
[image5]: ./examples/bboxes_and_heat.png
[image6]: ./examples/labels_map.png
[image7]: ./examples/output_bboxes.png
[video1]: ./project_video.mp4


### Histogram of Oriented Gradients (HOG)

#### 1. Explain how (and identify where in your code) you extracted HOG features from the training images.

First of all, let's exploe the data a bit:

<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/CARvsNotCar.png">

To obtain HOG feature and visulazation the `get_hog_features` has been implemented. For obtain the following imagee, I have considered `pix_per_cell = 8`, `cell_per_block = 2`.

<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/car_HOG.png">
  
<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/nonCar_HOG.png">



#### 2. Explain how you settled on your final choice of HOG parameters.

I tried various combinations of parameters in SVM classifier. The process was mainly relied on trial and error.

#### 3. Describe how (and identify where in your code) you trained a classifier using your selected HOG features (and color features if you used them).

First, I trained a `linear SVM`. The accuracy is then obtained by `score()` method. Finally, the predicted results were obtianed using `predict()` method.

### Sliding Window Search

#### 1. Describe how (and identify where in your code) you implemented a sliding window search.  How did you decide what scales to search and how much to overlap windows?

I decided to search random window positions at random scales all over the image and came up with this (ok just kidding I didn't actually ;):

<p align="center">
<img width="400" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/SlidingWindowsTech.png">


#### 2. Show some examples of test images to demonstrate how your pipeline is working.  What did you do to optimize the performance of your classifier?

Ultimately I searched on two scales using YCrCb 3-channel HOG features plus spatially binned color and histograms of color in the feature vector, which provided a nice result.  Here are some example images:

<p align="center">
<img width="400" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/detect_car.png">


### Video Implementation

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (somewhat wobbly or unstable bounding boxes are ok as long as you are identifying the vehicles most of the time with minimal false positives.)

Here's a [link to my video result](https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/project_output.mp4)

<p align="center">
<img src="https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/gif_video_output.gif"/>



#### 2. Describe how (and identify where in your code) you implemented some kind of filter for false positives and some method for combining overlapping bounding boxes.

I recorded the positions of positive detections in each frame of the video.  From the positive detections I created a heatmap and then thresholded that map to identify vehicle positions. Here's an example result showing the heatmap:

<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/Heat1.png">
  
<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/Heat2.png">
  
<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/Heat3.png">
  
<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/Heat4.png">
  
<p align="center">
<img width="600" src= "https://github.com/AliBaheri/Vehicle_Detection_SDCND/blob/master/output_images/Heat5.png">
  
### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

The proposed pipeline works well. However it cannot be considered a real-time vehicle detection pipeline. One potential future work includes implementing real-time object detection algorithms such as YOLO.
