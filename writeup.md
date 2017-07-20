# **Finding Lane Lines on the Road -- Hari Thatavarthy** 

## Writeup 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on the work performed in a written report


---

### Reflection

### 1. Describing the Pipeline

My pipeline consisted of 8 steps.

a. First I converted all yellow lines to white as it was hard to identify yellow lines on concrete roads

b. Then i converted the image to GrayScale. Converting to grayscale is necessary to limit the number of colors in the image to 256 values (8 bit). This will effectively help me identify the lines later.

c. I reduced the noise through gaussian function . I used Kernel size of 5. Reducing the kernel size may improve the performance of video processing but i have left it for now at 5 as i am not sure how to will really impact the final outcome.

d. I then performed Canny Edge Detection to highlight the edges

e. I narrowed down the region of interest by using a common formulae that can be applied to all images/videos.

f. I then identified the line segments through Hough Transform.
   For Hough transform , i used the following values for function attributes.
    1. Threshold : 20    # minimum number of votes (intersections in Hough grid cell)
         I used 20 as i felt appropriate given the pace at which the presumed vehicle is moving in the videos.
         It seemed to be a highway and i believe a threshold value of 20 seems justifiable.
    2. Min line lenght : 5  #minimum number of pixels making up a line
    3. Max line Gap : 5  # maximum gap in pixels between connectable line segments
    
g. I then extrapolated the line segments to fit into straight line (the coorodinates required to plot the straight line is obtained through least square method)

h. I then added weight to left and right straight lines.


After my pipeline is ready, i recursively processed  each image/video by passing it through the pipeline.



### 2. Identify potential shortcomings with your current pipeline


a. I have tested my pipeline against a sample image that i downloaded from web. The top portion of the image has road with fresh concreate and the bottom portion has dull and fainted concrete. The Canny edge detection did not identify a line segment there by making the output useless

b. Challenge video has steep right curves where the vehicle seemed to have steered towards the right from the center of the line. As  my region of interest was constant , the  lane lines  drawn by my pipeline are little off from the actual lane lines.


### 3. Suggest possible improvements to your pipeline
a. A dynamic way to set the region of interest based on the curvature of the road can improve the end result.
