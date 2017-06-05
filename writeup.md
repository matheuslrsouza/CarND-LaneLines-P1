# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image1]: ./writeup_images/grayscale.png "Grayscale"
[image2]: ./writeup_images/canny.png "Canny"
[image3]: ./writeup_images/mask.png "Mask"
[image4]: ./writeup_images/result.png "Result with hough lines"

---

### Reflection

### 1. Pipeline

I start by converting the image to grayscale.
Then the gradient is computed to identify the edges using the canny function.
Then an image is created only in the place where we want to recover the points (lane lines)
The hough lines are then applied to retrieve the straight lines
Then the lines obtained in the hough_lines are drawn in the original image

In order to draw a single line on the left and right lanes, I modified the draw_lines () function 
to calculate the slope of the given line by two points. Then I separated the right and left straight lines,
to do this, I checked whether the value is positive or negative. If the slope is positive it means
that this line belongs to the right lane, otherwise this straight line is part of the left lane.
In the right I discarded straight lines with slope values ​​smaller than .5, this was the form found
to ignore straight lines in the middle of the road. Likewise in the left lane were skipped straight with slopes less than .7.
After separating the sides, I try to retrieve the most extreme points from all the lines, in order to draw the full line.
In order to maintain the two implementations, both a full line (extrapolate) and several segments, I added
a parameter called extrapolate_line in the draw_lines method. I also changed the hough_lines method return to return
the lines.

##### Grayscale
![image1]
##### Canny
![image2]
##### Mask
![image3]
##### Result with hough lines
![image4]


### 2. Shortcomings

One possible shortcoming would be on moment to identify/draw the full line, sometimes
the line does not stay to the full extent as in example P1_example.mp4