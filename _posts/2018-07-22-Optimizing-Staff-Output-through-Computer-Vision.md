---
layout: post
title: Optimizing Staff Output through Image Processing/Computer Vision
---

![alt_text]({{ site.url }}/images/terminator.jpg)

### Introduction

I had the pleasure of working with <a href='https://www.homechef.com/'>Home Chef</a>, a subscription based meal delivery company based in Chicago.

Home Chef carries out it's operations in a big part by leveraging an efficient service line using a flexible workforce that can be deployed to complete different task as per needs. Something they could use was information on how many employees are working on a line at any given time, ideally in real-time.

To that effect, they provided me with access to a camera feed pointed at one of the assembly lines.

![alt_text]({{ site.url }}/images/test_video.gif)

And our aim here is to count these people:

![alt_text]({{ site.url }}/images/count_people.jpg)

### Approach

I used an unsupervised approach for this project.

A video through the camera’s web interface is downloaded and then passed on to the program as an argument, along with a start and end time (in seconds). The video is split to only include the portion between the start and the end time.

The camera records at 30fps with a resolution of 1920*1080.

From the split video:

1. All frames are extracted.

![alt_text]({{ site.url }}/images/sample_frame.jpg)

2. The frames are converted to grayscale.

![alt_text]({{ site.url }}/images/bwframe.jpg)

3. The grayscale frames are cropped to 1920*500.

![alt_text]({{ site.url }}/images/bwcropframe.jpg)

4. Mixture of Gaussian (MoG) is applied to all frames.

The GIF exceeds the size Github allows to upload so I've uploaded it here on <a href='https://imgur.com/a/mn5LcDr'>imgur!</a>

5. Results of MoG are saved.

6. To each MoG frame, a median filter is applied to reduce noise.

![alt_text]({{ site.url }}/images/medianfilter.jpg)

7. Erosion and thresholding to further reduce noise.

![alt_text]({{ site.url }}/images/otsu_thresholding.jpg)

8. <a href='https://en.wikipedia.org/wiki/Connected_component_(graph_theory)'>Connected components</a> are counted from this frame.

9. Median of Connected Components over 300 frames taken to arrive at answer.

![alt_text]({{ site.url }}/images/finalresult.jpg)

Some of the advantages of using an unsupervised approach such as this over a deep learning/network based approach is that this allows much greater flexibility of deployment i.e. the skeleton of this algorithm may be applied to any other project where it's desired to count any moving entities. Another advantage is that this algorithm is a lot 'lighter' than a deep learning model which would take a long time to train.

### Results

Algorithm was tested over different time frames and compared to manually counting number of people by eye.

![alt_text]({{ site.url }}/images/resultstable.jpg)

It was found that the algorithm was consistently off by +/- 2 people. However, when there were no people on the assembly line - the algorithm reported figures of 5/6 people.

Since the algorithm works off movement, it someone did not move over a period of 10 seconds they were not counted.

### Improvements

1. Taking median of Connected Components over more frames (~300 seconds) by leveraging more processing power through AWS could further help with accuracy.

2. Using a camera with a wider field-of-view to capture movement in the extremities.

3. Taking image from 2 cameras placed on different sides and using frames from both to average out discrepancies.
