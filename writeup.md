#**Finding Lane Lines on the Road** 

##Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 major steps: 
1. Convert original image to grayscale.
2. Apply Gaussian smoothing to the grayscale image.
3. Use Canny function to find ages via gradient.
4. Define an area of interest (polygon) and applies a mask to black out the rest of the image.
5. Apply Hough lines and extrapolate them to draw a single line on left and right.
6. Convert the image with the lines drawn back to color.

In order to draw a single line on the left and right lanes, I used a draw_lines_ext() function by that consisted of 4 major steps:
1. Separated each Hough segment detected to left and right sided based on slope and recorded the coordinates of each.
2. Used the coordinates recorded to fit a line for each side and found their coefficients a and b.
3. Used the line coefficients to fit a line that runs from the bottom of the frame to the top of the polygon of interest.
4. Drew the newly onbrained line onto the image 


###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the car is changing lanes and there are 3 major lanes in the area of interest - currently the same slope lines would be averaged-out which will result in two lines on the frame again one of them inaccurate.

Another shortcoming could be when another car is cutting in front and it is blocking the view of the lane markings which will currently result in an error since it would not find at least one segment on left or right side to extrapolate from.

A third shortcoming could be when there are a big number of smaller lane markings, shadows on the road, areas of gradient chage, that result in distractions in the form of false positive line segments, which seems to be the case with the challenge video.

###3. Suggest possible improvements to your pipeline

A possible improvement to the changing lanes shortcoming could be to classify the segments not only by slope but also by proximity so it case piece together more than just a static left and right lines.

An improvement to the no segments with particular slope problem could be to just check the count it found and not try to proceed drawing a line if count is 0.

The challenge video could potentially be solved by taking some screenshots of the raw version first so the pipeline can be tested with them. Then try to weed out any segments that are distractions and trigger false positives.