# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I performed Gaussian Blurring to reduce the complexity of the image and make it easy to focus only on the pixels of our objects of interest.
Then, I performed the edge detection by using the autocanny() function that I made inorder to automatically find the threshold values rather than hand-coding them each time.
I've used a triangular polygon as my Region Of Interest(ROI) and drew Hough lines on the lane edges that lie within the ROI.

In order to draw a single line on the left and right lanes, I modified the draw_lines():
* Initially I found the segments whose slopes are between -0.6 and -0.9 and averaged them to calculate the averaged left lane line slope.
* Then, I found the segments whose slopes are between 0.45 and 0.75 to be averaged and found the averaged right lane line slope.
* Average the left line segment points to get and average point through which the left/right line will pass through.
* After getting the average point and slope, I calculated the 2 point's position along the line on bottom and half height of the image.
* Finally I connected the 2 points to extrapolate the line segments.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be:
The lines were not efficiently drawn when the slope values I gave as threshold went out of range. Also the model didn’t perform well in cases where the lane lines had slight shadows.




### 3. Suggest possible improvements to your pipeline

A possible improvement would be instead of just dealing with the RGB color space, I think considering other color spaces like HSV, HLS and other aspects like gradients could be of a great help during lane identification.

Another potential improvement could be to train the images on a CNN model, which gives a better accuracy rate than most of the image processing algorithms.
