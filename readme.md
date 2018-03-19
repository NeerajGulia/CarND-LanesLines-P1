# **Finding Lane Lines on the Road** 

## Writeup Template

## Steps to find the lane lines on the road
1. Identify the white and yellow lines using the HLS color space
2. Convert the image to grayscale, since next steps will work on only one channel image
3. Blur the image so that when we identify the edges those are smooth
4. Find the edges in the image, we will use canny method to find the edges
5. Clip the image to find only the region of interest. This is the region which has the lane lines 
6. Find the lines using the hough lines method
7. Find average line and extrapolate if necessary
8. Plot the lane lines on the image


---

## Reflection

## Explanation of Average and extrapolate of lines in step 7

There are many frames in a video which does not contain the continuous lane lines, also in case of dotted white lines its necessary to extrapolate the lane lines.
Also due to rough road and sudden changes in road color its necessary to find and plot the lines based on the average of lines of the previous frames.
### Steps:
1. Get the hough lines - we will get the start and end points of the line
2. Identify the slope to get to know if the line falls in left side or right side
3. Use polyFit method of numpy library to identify the coefficients of a line (y = mx + b)
4. Using these coefficients we can extend the line to the desired region - numpy's poly1d function can be used to find the line
5. Also we can average out the coefficients of previous frames to smooth out the line - this will be very helpful when the frames will run as video
6. Since we know the top Y and bottom Y coordinates, using the coefficients of the line we can find the corresponding top X and bottom X points and using these coordinates we can draw the line
7. Since I knew the line coordinates, I draw a light green area which denotes the current lane - this looks cool as compared to only the lane lines

#### Example of processed image:

![Processed Image](./solidYellowCurve.jpg?raw=true "Processed Image")

#### Challenge video

![Challenge](./challenge.gif?raw=true "Challenge")


### 2. Identify potential shortcomings with your current pipeline

1. Since the pipeline processing is based on the camera output, in case of a bumpy road/path it would be very hard to find the lane lines efficiently
2. This might not work in night
3. If the road does not have lanes drawn on road, the pipeline will fail 

### Bibliography
[Extrapolate lines with numpy polyfit](https://peteris.rocks/blog/extrapolate-lines-with-numpy-polyfit/)

[Create directory in Python](https://stackoverflow.com/questions/12517451/automatically-creating-directories-with-file-output)

[VideoFileClip error](https://stackoverflow.com/questions/43966523/getting-oserror-winerror-6-the-handle-is-invalid-in-videofileclip-function)
