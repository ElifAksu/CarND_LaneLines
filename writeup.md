# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

A pipeline is created to find lane lines on the road. The steps and the results will be presented. 

Example image from the road is as below

[//]: # (Image References)

[image1]: ./test_images/solidWhiteRight.jpg "firstimage"
![alt text][image1]
---

### Reflection

### Pipeline 

My pipeline consists of 5 steps. 
1.  Convert rgb image to the grayscale image 

[image2]: ./images_output/blurgray_solidWhiteRight.jpg "BlurGrayscaleSolidWhiteRight"
![alt text][image2]

2.  Apply Gaussian smoothing to get smooth edges

[image3]: ./images_output/masked_edges_solidWhiteRight.jpg "MaskedGrayscaleSolidWhiteRight"
![alt text][image3]

3. Apply Canny Edge detection algorithm to find edges 
4. Mask the image to find road lines (Filter the out of interest area)

[image4]: ./images_output/houghlines_solidWhiteRight.jpg "HoughscaleSolidWhiteRight"
![alt text][image4]

5. Apply Hough Transform to find lines from the edges 

[image5]: ./images_output/redlines_solidWhiteRight.jpg "RedscaleSolidWhiteRight"
![alt text][image5]

At the end of these algorithm steps, we obtain line points (x1,x2,y1,y2) from Hough transform. 
The output lines can be one solid line or split lines. 
In order to draw a single line on the left and right lanes, I modified the draw_lines() function, applying avarage and extrapolation calculations. The steps are:
1. The left lines and right lines are found according to slope values. The line shows the left line if the slope is less than -0.5 and higher than -3.  The positive thresholds (0.5 - 3) are applied to find right lines
2. The left and right line points are seperated and collected in different lists. The avarage line points are calculated with these point lists. Avarage slope is calculated from avarage points.
4. Extrapolated line points are calculated with avarage points. The bottom(y=540) and top (y=330) of the lines are known as the region of interest decides these y points. With the help of extrapolation equation, upper and lower x points are found.  

The output is as follows;

[image6]: ./images_output/process_image.jpg "Process"

![alt text][image6]


### 2. Identify potential shortcomings with your current pipeline

The first shortcoming is when the road lines are curved, the lines are not found correctly.

Another shortcoming is that if the road line is not detected, there is no output on the screen. The current algorithm does not keep the previous values



### 3. Suggest possible improvements to your pipeline

A possible improvement would be to add prediction to this pipeline to give the output even if the lane line is not detected. 

The pipeline can be improved to include curved lines
