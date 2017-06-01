#Finding Lane Lines on the Road

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline.

The pipeline works as follows:
1. First convert the image to grayscale
2. Apply gaussian blur
3. Apply Canny edge detection
4. Apply a mask to the image keeping the part we are interested in only
5. Use Hough transformation to find lines from the detected edges
6. Draw the lines
7. Combine the original image with the image of the lines

In order to draw a single line on the left and right lanes I calculated the slope of each detected image, then using a threshold on the slope I classified lines into three categories: left lane lines, right lane lines or other lines like horizontal that I discarded.
Then using numpy's polyfit I adjusted two lines, one for the left lane and one for the right lane and got a line equation $y = m*x$ for each lane. Using this two equations I got the points I needed for drawing the left and right lanes. I draw the lines starting at the bottom of the screen and ending at a fixed height of 1.7 of the image height.

### 2. Potential shortcomings

One potential shortcoming that I detected with my image processing pipeline is that the slope by itself is not always the best way to classify if a line is a right lane line or a left lane line. Many shadows on the challenge video got past this and were classified as left lane lines and caused my line to jump a lot.

Also changes on the surface of the highway were detected as lines and although horizontal lines were filtered by the slope they introduced a lot of noise.

The drawn line jumped quite a bit and needed some smoothing.


### 3. Possible Improvements

The lane classification could be improved by using other metrics not only the slope. Also better filtering of the noise lines.

Smoothing of the lane line movement. Using info from the past frames implement a smoothing function for the lane line to be more stable.
