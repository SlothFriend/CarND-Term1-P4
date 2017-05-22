# Advanced Lane-Detection for Self-Driving Cars

[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

In this project (#4 in Udacity's SDCND) I develop a pipeline to detect the road lane and lane features from images taken within a driving vehicle. The pipeline processes single images but can also be applied to frames of a video.

If you want to toy with the code, it's all in [pipeline.ipynb](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/pipeline.ipynb). The code is well-documented and there's lots of supporting text to walk you through the notebook. [Make sure you get all the dependencies installed. My repo of [Udacity's starter](https://github.com/SealedSaint/CarND-Term1-Starter) might help.] 


## Overview: The Pipeline

The lane-detection pipeline consists of the following steps:

1. Pre-Step: Calibrate the camera
2. Undistort the image
3. Threshold the image using gradients and colors
4. Apply a perspective transform to view the image from top-down
5. Identify the lane lines in warped image
6. Draw onto the original image

The pre-step, calibrating the camera, is performed only once (assuming all the images are taken from the same camera). All the other steps are performed on each image.

### Calibrate the Camera

"Calibrating the camera" really means accounting for the distortion in an image introduced by the camera's lens. This is done using multiple images of checkerboard patters, which should have stright lines. Examining how the checkerboard patterns are distorted allows us to precisely identify how the camera lens is distoring images - which means we can undistort them.

![Distorted Checkerboard Image](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/camera_cal_images/not_enough_corners/calibration1.jpg)

### Undistort the Image

With the camera calibrated, we simply need to apply the knowledge gained to undistort images. This is important because it will restore the straightness of lines, helping to identify lane lines later in the pipeline. The difference between the distorted and undistorted images is clear. The bent lines are now straight.

Distorted | Undistorted
:---: | :---:
![Distorted Checkerboard Image](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/camera_cal_images/not_enough_corners/calibration1.jpg) | ![Undistorted Checkerboard Image](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/example_images/undistorted_checkerboard.jpg)

### Threshold the Image

Thresholding is a method of narrowing down the pixels we are interested in. This can be done using a combination of gradient and color filters. Here's what a thresholded image looks like.

Original | Thresholded
:---: | :---:
![Original Image](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/test_images/test2.jpg) | ![Thresholded Image](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/example_images/threshold_test2.jpg)

### Perspective Transform

While undistorting and thresholding help isolate the important information, we can further isolate that information by looking only at the portion of the image we care about - the road. To focus in on the road portion of the image we shift our perspective to a top-down view of the road in front of the car.

Thresholded - Normal Perspective | Thresholded - Top-Down Perspective
:---: | :---:
![Thresholded Image in Normal Perspective](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/example_images/threshold_test2.jpg) | ![Thresholded Image in Top-Down Perspective](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/example_images/warped_threshold_test2.jpg)

### Identify the Lane Lines

From the top-down perspective it's much easier to identify the lane lines. Lane curvature is also much easier to calculate. Here is an image showing the lane lines identified by a sliding window search. Best-fit lines are also shown in yellow for each lane line (these will be used to calculate lane curvature).

![Lane Lines Identified in Warped Thresholded Image](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/example_images/lane_detection_warped_test2.jpg)

### Drawing onto the Original Image

Finally, we take all this information we gathered and draw the results back onto the original image. The calculated right/left lane curvature and center-lane offset are shown in the top-left of the image.

![Final Image with Lane Identified](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/example_images/final.jpg)

## Applying the Pipeline to Videos

At the end of [pipeline.ipynb](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/pipeline.ipynb) is some simple code that processes videos using this lane-detection pipeline. My final video output for three different videos can be found on YouTube here:

* [Project Video](https://www.youtube.com/watch?v=v_leQokpNnU)
* [Challenge Video](https://www.youtube.com/watch?v=YIfH7aO-D_4)
* [Harder Challenge Video](https://www.youtube.com/watch?v=3lMie0rdx4E)
