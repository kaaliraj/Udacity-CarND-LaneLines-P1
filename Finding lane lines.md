# **Finding Lane Lines on the Road** 


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
First, I converted the images to grayscale (will make the image robust for white line as well as yellow line detection), 

**cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)

then I applied gaussian smoothing for precise canny edge detection 

**cv2.GaussianBlur(img, (kernel_size, kernel_size), 0)
**cv2.Canny(img, low_threshold, high_threshold)


then in order to find the road lines,at first the below region of an image is marked as point of interest ,vertices was specified and hough 
transform was applied to find coordinated of lines in region of interest 

**cv2.HoughLinesP(img, rho, theta, threshold, np.array([]), minLineLength=min_line_len, maxLineGap=max_line_gap)

then **playing with dependent parameters of canny() and HoughLinesP() 

a continous line coordinate is extracted.


**draw a single line on the left and right lanes:

in order to distinguish between left lane and right lane a simple concept of slope is used ,
slope of the left line is positive and that of right line is negative.
from the output of HoughLinesP() ,slope of each line is calculated and looked for condition above ,
an average slope of left line and right line is summed up and then used to draw a line. 

**idea of slope from https://www.mathwarehouse.com/algebra/linear_equation/slope-of-a-line.php

**here are images of the output:
please find the results at **test_images folder   ...final.jpg



### 2. potential shortcomings of the current pipeline


One potential shortcoming would be what would happen when the **car is travelling in curves,

**the slope value shifts amd makes lines closer to the car unstable(jittering).

Another shortcoming could be what **if the right lanes are not marked,the path cannot be traced with this code


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to instead of regular averaging a slope a **weighted averaging can be done so that **lines closer to the car are given more weightage while averaging.

 
