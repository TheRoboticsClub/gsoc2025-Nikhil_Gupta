---
layout: post
title: "Community Bonding Week-2"
subtitle: "Exploring datasets and GSoC'25 JdeRobot kickoff meeting"
date: 2025-05-30
categories: [blog]
# tags: [jekyll, github-pages, al-folio]
author: Sakhineti Praveena
---


## Meeting with Mentors

Started this week with the usual weekly sync up with the mentors, where we discussed various aspects of the project and my progress so far.  David encouraged me to play around a bit with the datasets, download, parse and implement inference, even if it's simple at this stage.

Sergio highlighted the importance of understanding the input and output formats of the models, and how crucial it is to be able to handle these effectively to extract meaningful metrics. He pointed out that knowing the format of the dataset and how they are passed to the models are crucial for the project over internal workings of each model layer. Santiago shared a helpful insight that any complex computer vision problem can be broken down into smaller subproblems of classification or regression. And finally, david addressed the elephant in the room — we all learned how to pronounce each other’s names correctly yay!

## This Week’s To-Do

- [x] Go through different dataset formats.
- [x] Download the datasets and parse them.
- [x] Use a portion of a COCO dataset to implement inference

## Progress

This week was all about exploring dataset formats and getting hands-on with them. I started with the COCO dataset and downloaded the 2017 validation images, training images, and the 2017 Train/Val annotations from the [official COCO website](https://cocodataset.org/#download). My goal was to understand how the dataset is structured, how the annotations are stored, and how to work with them effectively.

I referred to the [COCO data format documentation](https://cocodataset.org/#format-data) to dive deeper into the annotation structure. The main `annotations.json` file contains several top-level keys: `info`, `licenses`, `images`, `annotations`, and `categories`. Each object in the `annotations` list typically includes fields such as `id`, `image_id`, `category_id`, `bbox`, `area`, and `iscrowd`. The `bbox` is formatted as `[x, y, width, height]`, where `(x, y)` marks the top-left corner of the bounding box. To understand this better, I started mapping the annotations to their corresponding images and visualizing them with bounding boxes in a notebook called [coco.ipynb](https://github.com/TheRoboticsClub/gsoc2025-Sakhineti_Praveena/tree/main/demos/coco.ipynb).

Initially, I redundantly mapped the annotations to images in [coco.ipynb](https://github.com/TheRoboticsClub/gsoc2025-Sakhineti_Praveena/tree/main/demos/coco.ipynb). But later, I discovered the official COCO API, which simplifies the process of loading, parsing, and visualizing annotations. It was a bit humbling to realize how much easier things could have been — but also a valuable lesson in finding the right tools. With this understanding, I proceeded to implement a simple object detection pipeline [detection_coco.ipynb](https://github.com/TheRoboticsClub/gsoc2025-Sakhineti_Praveena/tree/main/demos/detection_coco.ipynb), using a pretrained Faster R-CNN model from TorchVision. I ran inference on a small subset of 10 images from the COCO dataset to test how everything worked together, below is an image I populated inference for. 
{% include figure.liquid path="assets/img/blog/2025-05-30-Community-Bonding-Week-2/objDetection.png" class="img-fluid rounded z-depth-1" zoomable=true %} 
Following that, I explored the Pascal VOC dataset. I downloaded the 2012 training and validation sets from the [official VOC site](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/). Unlike COCO, VOC uses separate XML files for each image to store annotations. Each file contains object instances with tags like `<name>` for the class label, `<difficult>` (a flag to indicate whether the object should be considered in evaluation), and `<bndbox>`, which specifies the bounding box coordinates in the format `(xmin, ymin, xmax, ymax)`. I parsed and visualized several VOC images in a separate notebook  [PascalVoc.ipynb](https://github.com/TheRoboticsClub/gsoc2025-Sakhineti_Praveena/tree/main/demos/PascalVoc.ipynb). I also came across a useful [script](https://github.com/shiyemin/voc2coco/blob/master/voc2coco.py) to convert VOC annotations to COCO format.

In addition, I briefly explored the YOLO dataset format. YOLO annotations are stored in `.txt` files, one per image, with each line containing five values: `<class_id> <x_center> <y_center> <width> <height>`, all normalized between 0 and 1 relative to the image dimensions. The format is simple and optimized for real-time detection.

Finally, towards the end of the week, I began exploring `Streamlit`, a lightweight framework for building data apps in Python. Although I didn’t get the chance to complete a working GUI yet, I managed to grasp the basics — which I plan to build on in the coming weeks as I move toward creating a user-friendly interface for visualizing model outputs.

## GSoC’25 JdeRobot Kickoff Meeting (29/05)

This week, I had the GSoC’25 kickoff meeting for JdeRobot, where I got to meet my fellow contributors, mentors, and the org admins. Pedro Arias began the session with a quick overview of JdeRobot, highlighting its main focus areas — robotics education, AI-driven robotics, and robot programming tools. It was inspiring to see how wide-ranging and impactful the organization’s work is.
{% include figure.liquid path="assets/img/blog/2025-05-30-Community-Bonding-Week-2/kickoffmeeting.png" class="img-fluid rounded z-depth-1" zoomable=true %} 
We then had a round of introductions, which was a great way to connect with like-minded people working on exciting and diverse projects. Following that, Pedro shared some helpful insights into the work methodologies we’ll be following, including contribution guidelines and evaluation timelines. David also gave us an important reminder to be proactive, not just during our weekly check-ins but throughout the week — by sharing timely updates, asking questions, and staying engaged. I will make sure to keep that in mind. He reassured us that no question is too small or silly. Overall it was a really helpful session to kick things off!

