# Project1_FindingLanes
---

# **Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a video processing pipeline that finds lane lines on the road 
* Reflect on the work in a written report

---

### Reflection

### Description of the pipeline.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I used gaussian blurring followed by canny edge detection to find the edges in the image. The edge images are masked using a region of interest which is specified as a polygon and fed to the hough transform which identifies straight lines in the edge images. 

I modified the provided draw_lines() baseline function implementation to then identify the left and right lanes using ransac (Random Sample Consensus) and plot them in green and red colors. The [RANSAC](https://en.wikipedia.org/wiki/Random_sample_consensus) algorithm fits two straight line models, one each for the left and right lanes to the points in each of the line segments returned from the hough transform lines.

#### Example Images and the correspoding output
![example image from video](/test_images/solidYellowCurve2.jpg)

![output of the algorithm] (/test_images_out/solidYellowCurve2_out.jpg)

### Potential shortcomings with the current pipeline


One potential shortcoming would be that the algorithm does not handle the case where either the left or right lane is missing. To enhance this algorithm we could add additional logic to check to see if the model we fit has a slope that is close enough to 45 degrees and has a sufficient number of inlier points.

Another potential shortcoming is that when the lanes are curved, the algorithm still tries to fit a straight line. One possible strategy to try out is to use a different model like a parabola curve.

Also something to keep in mind is that when cars cut in and out of our vehicle's lane then we may not be able to detect the lanes temporarily. Some kind of state estimation and tracking technique like Kalman Filtering could be applied to predict the lane positions even when it is not detected.

A common situation in urban conditions that is not handled is crosswalks and other traffic sign markers on the road. It would be necessary to segment those edges out by some kind of filtering that only looks for lines that are oriented vertically.


### Possible improvements to the pipeline

When the lanes are curved, the algorithm still tries to fit a straight line model. One possible strategy to try out is to use a different model like a parabola curve to handle this case a little better.

Also something to keep in mind is that when cars cut in and out of our vehicle's lane then we may not be able to detect the lanes temporarily. Some kind of state estimation and tracking technique like Kalman Filtering could be applied to predict the lane positions even when it is not detected.

Further there are edge cases where the lanes at exit signs are often bifurcated or split into multiple lanes. For such cases we need to consider fitting a piecewise spline model with 2 segments.

A nice enhacement would be to additionally detect the nature of the lane and classify it as "solid" or "dashed" and "white or "yellow".
