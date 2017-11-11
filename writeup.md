# **Finding Lane Lines on the Road**

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: documentation/grayscale.png "Grayscale"
[image2]: documentation/gaussian_blur.png "Gaussian Blur"
[image3]: documentation/edges.png "Edges"
[image4]: documentation/masked_edges.png "Masked Edges"
[image5]: documentation/found_lines.png "Found Lines"
[image6]: documentation/found_lines_on_orig.png "Found Lines on Original"
[image7]: documentation/found_lines_avg_lines_on_orig.png "Found Lines and Average Line on Original"
[image8]: documentation/result.png "Result"

---

### Reflection

### 1. Description of pipeline

My pipeline consisted of 7 steps.

  1. Transform image into gray scales ![Grayscale][image1]
  2. Trasnform image with gaussian blur ![Gaussian Blur][image2]
  3. Transform image with canny edge algorithm ![Edges][image3]
  4. Mask only the interesting area ![Masked Edges][image4]
    1. The area is from the bottom corners to the middle of the image
  5. Use the Houghlines algorithm to extract lines in the image ![Found Lines][image5] ![Found Lines on Original][image6]
  6. Filter the found lines to left and right Lines
    1. In genral we only want to look at lines that have at least 22.5°
    2. Left (blue on image)
      1. Slope < 0
      2. Line in left half of the image
    3. Right (green on image)
      1. Slope >= 0
      2. Line in right half of the image
    4. Find out the average slope for each side
      1. Only allow lines that are off inside 9° of average slope of lines
  7. Calculate average line for each side ![Found Lines and Average Lines on Original][image7]

  ![Result][image8]

### 2. Identify potential shortcomings with your current pipeline

  * Different weather conditions could change the video quality or color themes, characteristics defined in my pipeline maybe wont find lines anymore.
  * Different times of day
    * Day (sun shining into the cam)
    * Night
  * Anything else of road type then going straight
    * Curve
    * Crossing
    * Horizontal straight lines on the row
    * Roads without Lines (construction or just bad road)
    * Roads with lines that are not visible on the video, or very light road

### 3. Suggest possible improvements to your pipeline

  * Collect data for all those shortcomings above to test the algorithm
    * Photos or
    * Videos
  * Maybe save information after one calculation and save information to use it in the next run
