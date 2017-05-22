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
6. Un-transform back to orginal perspective and draw lane and lines

The pre-step, calibrating the camera, is performed only once (assuming all the images are taken from the same camera). All the other steps are performed on each image.

### Calibrate the Camera

"Calibrating the camera" really means accounting for the distortion in an image introduced by the camera's lens. This is done using multiple images of checkerboard patters, which should have stright lines. Examining how the checkerboard patterns are distorted allows us to precisely identify how the camera lens is distoring images - which means we can undistort them.

![Distorted Checkerboard Image](https://github.com/SealedSaint/CarND-Term1-P4/blob/master/camera_cal_images/not_enough_corners/calibration1.jpg)

### Undistort the Image

Now that the camera has been calibrated, all the hard work is done here. We simply need to apply that knowledge gained to undistort images. This is important because it will restore the straightness of lines, helping to identify lane lines later in the pipeline. The following image is the same as above, but undistorted. The bent lines are now straight.

![Undistorted Checkerboard Image]()
