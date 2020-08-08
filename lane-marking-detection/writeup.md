# **Finding Lane Lines on the Road**

**Finding Lane Lines on the Road**

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the frame to grayscale so that the line detection would not need to be dependent on the color. Next, I performed a Gaussian blur on the image to get rid of any noise. Next, I did a Canny edge detection to detect the edges in the grayscaled image. Next, I extracted a triangular region of interest where the line markings are usually located in the image. Next, I did a Hough lines detection to extract line segments from the edges. Finally, I superimposed the averaged lines on top of the original images to show the detected lane markings.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first filtering line segments that had extreme slopes. For example, I kept slopes that ranges between &#177;0.5 and &#177;0.8 which was usually the range of slopes that the line markings were part of. I averaged out the left and right slopes to get a single measurement for each side. Next, I picked a random point from the collection of line segments on each lane edge. Then, using point-slope form, I derived the equation of a line for each lane edge. To get the final lines, I just drew line segments from the bottom of the screen to the middle of the screen with each line equation.

### 2. Identify potential shortcomings with your current pipeline

When no lines are detected with the Hough lines detection, it is difficult to use my draw_lines algorithm because I won't be able to filter any lines.

Also if some of the lane markings become erased on the road, the Hough line detection won't be able to find enough pixels to actually form a line.

Also, like in the extra credit clip, if the camera is too close to the windshield, then my triangular region won't cover any of the lanes, and as such, I won't have any lines to do lane recognition on.

### 3. Suggest possible improvements to your pipeline

Make the triangular region wider so that I will be able to capture the lanes even if the camera is closer to the windshield.

Maybe if I'm not able to find any lane markings on one side, try to reflect the lane marking from the other side just so that we can draw an approximate line. 
