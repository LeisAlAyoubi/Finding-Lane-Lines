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

My pipeline consisted of 5 steps. First, I converted the images to grayscale. After the conversion to grayscale I used the canny method to 
identify edges in the image. I set the lower threshhold to 50 and the upper threshold to 150 (factor 1:3). I didnt not apply the Gaussian Blur function explicitly because it is already applied in the canny function by default. As a third step I drew lines around the region of interest which is also refered to applying a mask on the image. I used a four sided polygon as a mask, the points needed for setting up the polygon were found by trial and error. The fourth function used was the hough_lines function where is set the threshold to 10, the minimum line length to 30 and the max line gap to 20. These values showed good results. The fifth step was to use the draw_lines function to draw red lines on the identified lanes.  

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first sorting the points with respect to their slope. Lines with a slope of zero or greater than +/- 0.5 where omitted cause the lane lines cant ever have a slope of zero or greater than +/- 0.5. A negative slope indicates that the points belong to the left lane and a positive slope implies that the points belong to the right lane. After classifing the points I used the polyfit function provided by numpy library to find the coefficients of the line of best fit between the points of the left and the right lane. I then used the coefficents to draw the line on the original image.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road is curved and therefore a straight line wouldnt best decribe the lane markings. 

Another shortcoming could be that the polyfit function doesnt always provide the right approximation which suits our goal best. Sometimes the drawn line appears to have a slope greater than +/-0.5 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use another higher polynomial function to decribe curved roads.

Another potential improvement could be to restrict the slope of the possible lines drawn by the polyfit function.
