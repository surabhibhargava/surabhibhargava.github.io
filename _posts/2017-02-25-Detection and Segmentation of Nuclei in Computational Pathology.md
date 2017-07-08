---
title: "Detection and Segmentation of nuclei in Computational Pathology"
layout: post
date: 2017-02-25 00:00
<!-- image: /assets/images/markdown.jpg -->
headerImage: false
tag:

category: blog
author: surabhibhargava
description: Detection and Segmentation of nuclei in Computational Pathology
---
<h3><b> Introduction </b></h3>

Detection and segmentation of nuclei in histopathological images has numerous biomedical applications. The conventional method involves manual inspection and analyses performed by pathologists to make diagnostic and prognostic assessments based on certain features of the nucleus.

Manual annotation of nuclei and inspection of the derived features is a highly tedious and time consuming process. Hence many computer aided image analysis techniques of automating this analysis have been proposed. Existing approaches dealing with detection and segmentation of nuclei are rather limited and generally fail to segment touching or overlapping nuclei. Even if they succeed, the shape of the nucleus is often distorted.

We have converted this segmentation problem into a three class classification problem where each pixel can be classified into one of the three classes: Inside nucleus, Boundary and Not nucleus and not boundary.

Further we have developed a post-processing technique which segments nuclei having different markers as separate.

<h3><b> Methodology </b></h3>
This section consists of three parts:

1) <b> Data Preparation and Pre - Processing </b>: <br>
<b> Annotations </b>: In order to prepare the ground truth for CNN training, manual annotations have been performed using Aperio ImageScope. <br>

<b>Ternary Maps</b>: Ternary maps are generated using annotations which are further used as the labels for training. A pixel takes one of the three gray scale values:<br>
-* A pixel inside nucleus : 255 <br>
-* A pixel on the boundary : 128 <br>
-* A pixel not inside nucleus and not on boundary : 0 <br>

The figure below shows a test image, its annotations as what it appears in ImageScope while annotating and the resulting ternary map.<br>
<!-- <img src="/img/assets/testImage.png" width="200" /> <img src="/img/assets/annotatedImage.png" width="200"/> -->

Test Image | Annotated Image | Ternary Map
-|-|-
![Test Image](/assets/testImage.png) | ![Annotated Image](/assets/annotatedImage.png) | ![Ternary Map](/assets/ternaryMap.png)

<br><b>Color Normalization</b>: It is used to normalize the variation in stain colors across different images. All images are made to appear similar to a target image using color normalization. We have adopted the technique in <a href="http://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=7460968">this</a> paper. <br>

The images below show a source image, target image and a normalized image. It may be clearly seen that the source image is colour normalized to appear like the target image. This results in an improvement of accuracy since the images have similar appearance while training and testing.

Source Image | Target Image | Normalized Image
-|-|-
![Source Image](/assets/sourceImg.png) | ![Target Image](/assets/targetImg.png) | ![Normalized Image](/assets/normalizedImg.png)

<br>
2) <b>The Convolutional Neural Network </b>:<br>
A convolutional neural network (CNN) has been used to predict the class of a pixel by feeding in a small window around the pixel as the input to the CNN. Each pixel is classified as nucleus, boundary or not nucleus and not boundary.<br>

The architecture of the Convolutional Neural Network is mentioned in the table below. We have used Torch for training and testing the CNN.<br>

The dataset used had images of 20x and 40x resolution and a slightly different architecture has been used for the two resolutions.

![CNN arch](/assets/arch.jpg)
<br><br>
![Architecture details](/assets/architecture.png)

3)<b> CNN output and Post - processing:</b> Probability maps for each class are obtained as the output of the CNN. We obtain nuclei maps from these probability maps by thresholding and applying the post-processing technique developed.

The flow chart below describes the post-processing technique used.
<br><br>
<img src="/assets/postpro.jpg" width="550" /><br>
<br>
<b>Post-Processing Technique:</b>
<br>
Probability Maps and Coloured maps for a given test image:<br>

Test Image | Nucleus Probability Map | Boundary Probability Map | Non-Nucleus Probability Map
-|-|-|-
![Test Img](/assets/tp.png) | ![Nucleus Prob Map](/assets/pm.png) | ![boundary pm](/assets/bpm.png) | ![Non Nuc pm](/assets/nnpm.png)

Test Image | Binary Map | Coloured Map
-|-|-
![Test Img](/assets/tp.png) | ![Bianry Map](/assets/bin.png) | ![Colour map](/assets/color.png)  

<br>
<h3><b> Some More Results </b></h3>
<b>Detection & Segmentation Results for 20x resolution Prostate gland biopsy images:</b>

Test Image | Coloured map | Coloured map superimposed on image
-|-|-
![Test Img](/assets/1t.png) | ![Coloured Map](/assets/1m.png) | ![Colour map superimposed on image](/assets/1c.png)


Test Image | Coloured map | Coloured map superimposed on image
-|-|-
![Test Img](/assets/2t.png) | ![Coloured Map](/assets/2m.png) | ![Colour map superimposed on image](/assets/2c.png)

<br><b>Detection & Segmentation Results for 40x resolution Prostate gland biopsy image:</b>

Test Image | Coloured map | Coloured map superimposed on image
-|-|-
![Test Img](/assets/3t.png) | ![Coloured Map](/assets/3m.png) | ![Colour map superimposed on image](/assets/3c.png)


<br><br>
<h4><b> Acknowledgements </b></h4>
This work was started as a part of my final year thesis project along with <a href="https://sanuj.github.io/about/">Sanuj</a> under the guidance of <a href="http://www.iitg.ernet.in/amitsethi/">Prof. Amit Sethi</a>, Neeraj Kumar Vaid, Abhishek Vahadane and Ruchika Verma.<br>

It has recently been published in the IEEE Transactions on Medical Imaging.<br>
 <a href="http://nucleisegmentationbenchmark.weebly.com/"> Click here </a> to get Nuclei segmentation code and dataset and the paper.<br>

<a href="http://www.iitg.ernet.in/amitsethi/posters/16.SharmaBhargava.pdf">Click here</a> to get our Thesis poster.
