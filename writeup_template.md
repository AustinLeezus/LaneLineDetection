# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report




---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.
My Pipeline consists of several steps

first I take in the image and define parameters for the later filters. After I have completed that I create a grayscale copy of the image. 
I define a region of interest polygon using four points. 

I then apply a Gaussian Blur to help optimize my canny filter before running the greyscale through the canny filter to obtain a gradient image. I also apply a mask so that I am only left with the region of interest.

Using the HoughLinesP function in OpenCv I am able to obtain an array of lines of type line which defines start and end points for the lines as points (x1,y1), (x2,y2)

Iterating through the lines I am able to use y1-y2/x1-x2 to determine the slope of the line. Depending on if it meets a minimum threshold and it is postive or negative I am able to determine if the line is part of the left lane line, right lane line, or noise. I add and average slope values and calculate the average intercept that makes up each line.

I then use the top and bottom bounding y values of my region of interest as well as the average slope and intercept of the lines to calculate the x values of the top and bottom for each line. 

I use the point pairs determined in the previous step to define an average line for each lane line and project it on the original image along with the detected Hough Lines. An example output is defined below



[//]: # (Image References)

[image1]: ./test_image_output/test_images/solidWhiteCurve.jpg 

### 2. Identify potential shortcomings with your current pipeline


My pipeline only seems to work well with lines when the car is at low curvature. If the car were to be in a high curvature environment such as those of the challenge activity it will not work well for detecting the lanes.

Also a straight line is not an accurate estimate of a road that is not straight so I would have to do something other than mx+b


### 3. Suggest possible improvements to your pipeline

I could filter the gray scale with a mask defined by a color threshold for yellow or white. This would attempt to verify and detect only yellow and white lines rather than all lines

After I am able to detect these lane lines I would 

Extrapolate point data for the lines rather than just averaging them and try to define a second degree linear regression that more accurately fits the curve

Another potential improvement could be to ...
