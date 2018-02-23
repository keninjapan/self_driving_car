# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./writeup_images/original.jpg "Original"
[image2]: ./writeup_images/gray.jpg "Grayscale"
[image3]: ./writeup_images/blur.jpg "Blur"
[image4]: ./writeup_images/canny.jpg "Canny"
[image5]: ./writeup_images/region_of_interest.jpg "Region of interest"
[image6]: ./writeup_images/hough_lines.jpg "With hough lines"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. I'll explain those steps with an example image.

#### **Original Image:** 
![alt text][image1]

#### **Step 1:** Converts it into gray scale.
![alt text][image2]

#### **Step 2:** Blurs the image.
![alt text][image3]

#### **Step 3:** Applies the Canny algorithm on the image.
![alt text][image4]

#### **Step 4:** Filters out the uninterested area.
![alt text][image5]

#### **Step 5:** Uses Hough Transform algorithm to find the lane lines.
![alt text][image6]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function.
First, I separated the line segaments found by Hough Transform into left and right lanes buckects and also filtered out some outlier lines like horizon lines. Then, I fitted a line into each buckets using the least-squares method to represent left and right lane lines.


### 2. Identify potential shortcomings with your current pipeline

- Hard to deal with the very curved lane lines. Now I use one single straight line to represent a lane line, and the short coming is that when the lane line is curved easpecially at the bottom of the images (inside the region of interest), my pipeline can not draw the prefect lines hovered on the real lane line.

- If the lane line is formed by some short dots, not solid line segaments, my pipeline can not figure out the right slope of those dots and the final straight may deviate. Although I have tuned the parameters of Hough Transform, minLineLength and maxLineGap to reduce this problem, it still may be impacted by some cases I haven't encountered.

- The whole pipeline is really hand-tuned. I think the structure of pipelines for finding lane lines is solid but there are many parameters tuned by my intuition coming from the images I've seen. Like the above two problems, curved lines and short lane line segaments, are just the cases I can think of at the moments. For the real world cases, there must be more diverse situations needed more attention, and tuning the parameters specially for each case is not a scalable solution. We have one optional challenge in the project, but in the real world there may be hundreds of them.

### 3. Suggest possible improvements to your pipeline

- For filtering out the outlier line semgament part, I use a hard-coded number, +/-0.5, as a threshold, which should be derived everytime for each line group from the standard deviation of the lines group instead.

- Instead of fitting a straight line, I can connect the line segaments from Hough Transform by connecting a line segament with the closet one, and in this case the curved line can be better represented.

- Having more example images and building a pipeline for evaluation will make the development of the pipeline more robust and scalable.
