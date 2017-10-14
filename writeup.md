# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline is made up by the following steps:

* Convert image from RGB to HSV color-space (it is more easy to do the next step in HSV color-space)
* We threshold the HSV image for a range of yellow and white colors, in this step the converted image is in gray scale
* Define a kernel size of 5 and apply Gaussian smoothing
* We apply canny edge detector
* A triangle region was defined in order to discard edges (the camera has a fixed position)
* Hough transform is applied in order to detect the lane lines

Try and error approach was used to find the parameters of the previous steps. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by applying linear models.
If the amount of points to estimate a single line on the left and right lanes is less than 30, a simple linear model was used to
interpolate the lane line. Otherwise Lasso regression was used. To estimate the hyperparameter alpha, we try values in the range 
between 0.5 and 10. The following images are examples of the final output of the pipeline:


![solidWhiteCurve](https://raw.githubusercontent.com/ricardoues/CarND-LaneLines-P1/master/test_images_output/solidWhiteCurve.jpg "solidWhiteCurve")



### 2. Identify potential shortcomings with your current pipeline


Maybe linear models are not a good idea due to the local behaviour of the points belonging to a lane line.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use a method more robust such as spline interpolation.

Another potential improvement is to use cross validation to select hyperparameters in Lasso regression. 
