# **Finding Lane Lines on the Road** 


1. Describe the pipeline

The pipeline consisted of 8 stages:
- Color selection: isolate colors going from dark yellow to white.
- Region masking: Applying a trapezoid mask to isolate the region where the lines are displayed.
- Convert image to greyscale.
- Gaussian blur: reduce image noise and reduce details by smoothing the picture.
- Canny edge detection: Use to detect strong edge (strong gradient) pixels
- Hough Transform: Used to identify lines on the picture.
- Lane calculation: Based on the different lines which were found after the hough transform, define two lines (left and right)
- Merging: Merge original image with the right and left lines created in previous step

Hough transform

The different parameters (treshold, minimum length or maximum gap between 2 lines) were adjusted taking an empirical approach.

Lane calculation

For each line, the slope and the length is calculated. Horizontal lines are excluded if the slope is too low. Lines which are too short are also excluded because they could be not relevant for determining the correct position of the lane.

Then the lines are sorted between left lines (positive slope) and right lines (negative slope). For each side, the average of coordinates (x1,y1) and (x2,y2) is calculated based on all the coordinates of all the lines. The slope and origin of the lines going through those "averaged" coordinates is calculated.

The lines can be quite short. Therefore, the left/right lines are extended from the middle till the bottom of the image.

Finally, the lines are displayed to match the left and right lanes.

2. Identify any shortcomings

Weather condition:
If the image is darker due to bad weather, some lanes could not be detected because of a low contract. This could be solved by improving the color selection algorithm

Lane color:
If a blue lane was displayed, it is not sure that the color would be detected by the algorithm.



3. Suggest possible improvements

- The color selection algorithm could be improved to isolate certain colors only (blue, yellow, white).

- On every image, a complete different new set of lines (right and left) is created to be displayed on the image. Saving the lines from previous images could be useful for 2 reasons: 
1) if one of the lane could not be detected, the line from previous image could be displayed again.
2) the right/left lines are moving all the time, from one frame to the the next, and can possibly detect wrong lines. The lines could be "smoothed" by combining the new calculated lines with the lines from the last 2 or 3 frames.

