# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "Solid White Curve"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 3 phases. First, I extract the edges from the image. Next, I mask out all image data outside a region of interest. Lastly, I draw the lane lines over the image.

My edge extraction phase has 3 steps. First, I convert the image to grayscale. Next, I apply a gaussian blur. Lastly, I apply the Canny transform to select the edge pixels. The result is a black and white image with edges extracted.

My masking phase has 2 steps. First, I generate four vertices for the region of interest. Next, I apply this polygon to the edge extracted image as a mask. This erases any edges from the sky or side of the road.

My draw lines phase has 4 steps. First, I calculate all the hough lines from the edges that remain in the masked image. Next, I separate the hough lines into left and right lists of lines. Third, I convert the 2 lists of lines into 2 single lines for the left and right lanes. Lastly, I superimpose the the two lane lines on top of the original input image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating the hough lines into left and right lists of lines. Next, I filtered both lists by minimum and maximum possible slopes. Third, I calculated the slopes and centers of the 2 lines by averaging the slopes and centers of the lines in both lists. Lastly, I derived the x coordinates of the endpoints for each lane line from the average slopes and centers.

Here is my processed output from the `solidWhiteCurve.jpg`: 

![alt text][image1]

Click on [this link](https://raw.githubusercontent.com/fvasquez/CarND-LaneLines-P1/master/test_videos_output/solidWhiteRight.mp4) to view my processed output for the `solidWhiteRight.mp4`. The other processed videos are in the `test_images_output` directory of this repo.

Click on the [this link](https://raw.githubusercontent.com/fvasquez/CarND-LaneLines-P1/master/test_videos_output/solidYellowLeft.mp4)
to download my processed output for the `solidYellowLeft.mp4`. I noticed that Firefox does not recognize the video format of this output `.mp4` but I can still play the video after I download it to my machine.

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the horizon line is higher than the y coordinate hardcoded into this notebook. The lane lines will crisscross.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to edge detect the y coordinate of the horizon line so that it can be used in region of interest and lane line endpoint calculations.
