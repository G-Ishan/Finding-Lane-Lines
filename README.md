# Reflection

[//]: # (Image References)

[image1]: ./report_images/first_iteration.png "First Iteration"
[image2]: ./report_images/improved.png "Improved"

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First I converted the images to grayscale. Then, I applied a guassian blur with a kernel size of (5,5). This allowed to me apply Canny edges to the scene. Once I had the Canny edges, I applied a mask based on a ROI for the lane lines. From here, I applied Hough Lines and overlayed it on the image. These first iteration of these can be shown in the image below:

![alt text][image1]

The draw_lines function had to be improved to extrapolate the lane lines across the whole line (instead of the dashes). To accomplish this I implemented separate_lines(), find_longest_line(), and extrapolate_line(). In order, these functions first separated the Hough Lines into left and right lines based on their position in the scene. Then I found the longest line for each region using distance between intercepts. I used these lines to extrapolate because I felt they represented their lane well, being the longest line. To extrapolate the line, I knew I wanted the bottom ends at the bottom of the image, and the top ends were defined based on the positions I chose for my original mask (about the center of the image). I just had to find the x intercepts for the bottom of the lanes and I did that by using the slope formula. The overall pipeline described above stayed the same and the improved result is shown below:

![alt text][image2]


### 2. Identify potential shortcomings with your current pipeline

In the video output, I can tell the lane lines are a little jittery. This is due to the fact that lane lines have thicknesses. The longest lane line that is extrapolated is sometimes at the left of the lane marker and sometimes at the right. This causes some differences in extrapolated across the video which leads to jitteriness. 

Another shortcoming is that the extrapolation of the lane lines relies heavily on the slope of the found hough lines. The test videos did not include any instances of sharp curves or turns. I think the code would struggle in this situations.

Another shortcoming is that my current pipeline cannot complete the challenge video.  I wanted to move along with the course at this time so I have saved this challenge for a future date.

### 3. Suggest possible improvements to your pipeline
To account for the jitter in the video, an improvement could be made to account for the previously extrapolated lane line. This takes me back to the lessons from the ITSDC ND where in localization, it is important to constantly take in data and also account for the previous path. I think this would improve the jumping around of lane lines as well.

To improve the extrapolation on curves, the lane lines could be fit to a nonlinear curve instead of a straight line. This would allow splines to match the curvature of the road.

For the challenge in the future, I would likely have to improve my masking to mask yellow colors and white colors separately in the image. Then I could pick up the yellow and white lane lines better in a mixed image that includes both.

