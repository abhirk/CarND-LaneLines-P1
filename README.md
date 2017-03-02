# **Project 1: Finding Lane Lines on the Road** 
  A self-driving car needs to determine the bounds of the lane of the road in which it needs to drive. In this project, we have built the core logic pipeline that will help the car identify the lane lines, which can be used to navigate.

**Goals**
The goals of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on the findings and the work involved in the project

[initial]: ./readme_images/grey.jpg "Initial image"
[grey]: (./readme_images/grey.jpg =1000x650)
[gaussian]: ./readme_images/gaussian.jpg "Gaussian blur"
[canny]: ./readme_images/canny.jpg "Canny Edge detection"
[masked]: ./readme_images/masked.jpg "Masked region"
[hough]: ./readme_images/hough.jpg "Hough transform"
[weighted]: ./readme_images/weighted.jpg "Final image"

---

### Reflection

### 1. Pipeline
Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The following example illiustrates the steps in the pipeline in brief:
 - Consider the initial image as shown below.
 -   First we convert Image to Grayscale. 
     ![ 2 - Grayscale][grey]
 -   Image thresholding - WHY?
 -   Mask the region of interest
 -   Edge detection - Canny
 -   Hough transform - describe results
 -   Improve draw lines

-------
In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...
If you'd like to include images to show how the pipeline works, here is how to include an image: 

-----

### 2. Identify potential shortcomings with your current pipeline

##### a) Approach Shortcomings:
- One shortcoming is the parameters for the region of interest are dependent on the the initial angle for the lane lines and their position in the image (decided by the position of the camera w.r.t. the road). More complex and sharp turns might not return correct lanes. Similarly the code is not tested for the lane lines when the road turns (sharply), which might cause error in determining the bounds of the lanes correctly.

 - The code is also not tested for correctness in cases where the signs painted on the road, but which are not part of the lines e.g. "STOP", Direction arrows like right turn or "ONE WAY" or simply the pedestrian crossing.

##### b) Implementation Shortcomings:
 - One potential shortcoming would be what would happen when there is noise in the detected Hough Transform. The line fitted by the linear regression is further away from what it should be. 

 - Another shortcoming is each set of lane lines determined in a image/frame of a video is independent of the previous frame. This can cause flicker due to changes in the frame lines or sudden changes in the line lengths or angle due to noise or other errors.


### 3. Suggest possible improvements to your pipeline
 - A possible improvement for reducing the noise from the lines returned from the Hough transform is to mask the region that should not have lane edges assuming we are driving in the center of the lane and the camera position is fixed.
 - Fitting the points to a curve instead of line can improve the lane bounds that are detected
 - A possible way to reduce the flicker and smoothen the sudden changes in the lanes in the video is to remember previous N frames and aggregate the position of the lane lines.

