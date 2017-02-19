#**Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Description of my pipeline.

My pipline line consisted of the following steps:

1) Convert the images to grayscale

2) Perform a gaussian blur on the images

3) Identify edges in the images using the canny function

4) Specify the region of interest using the region_of_interest function, which keeps the region of the image defined by the polygon formed from `vertices` and sets the rest of the image to black.

5) Find lines using hough transform, which accepts the identifed edges as input. Note I modified the hough_lines function to also return an array of points for each line.

6) Create two lines from the hough lines using the crawford_lines function.  The crawford_lines function divides the hough lines into two groups based upon their slope: group 1 has positive slope and group 2 has negative slope.  For each group, I find the average slope and average y-intercept.  Using the boundaries of the region of interest and the avergage slopes and y-intercepts, I calculate the two lines to identify the lane boundaries.

7) Combine the lane lines and the original image using the weighted_img function.


###2. Potential shortcomings of the current pipeline


One potential shortcoming happens when lines are identified in the region of interest that are not truly part of the lane markings, which impacts the calculation of the average slop and y-intercept values.  This causes the system to misidentify the true lane marking.  This issue was observed when processing the solidYellowLeft.mp4 video.  In this video, it was observed through visial imspection several horizontal paint lines that intersected the lane boundaries and would therefore negatively impact the average slope and y-intercept calculations.

Another shortcoming is that the algorithm is not robust to curved lane markings.  If the road has significant curvature, then the system can only perform a linear estimation of the lane boundary.


###3. Suggested possible improvements to the pipeline

A possible improvement would be to add a function to reject outliers when performing the calculation of the average slope and y-intercepts.

Another potential improvement could be to perform a higher order approximation of the lane boundary, which should make the system more robust to curved lane markers.