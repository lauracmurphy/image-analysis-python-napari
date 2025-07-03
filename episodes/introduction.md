---
title: 'Introduction'
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 
- What will I learn in this course, and how is it structured?
- Why use Python for microscopy image analysis?
- What are digital microscopy images, and how do they differ from everyday images?
- What kinds of things can I measure from images using Python?
- How is the course organised and what software and data will I need to follow along?
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives
- Describe the aims and structure of the course
- Identify the main Python tools used in microscopy image analysis
- Recognise different types of microscopy image data and formats
- Verify that the required software and packages are installed
- Navigate the lesson materials and setup environment
::::::::::::::::::::::::::::::::::::::::::::::::

## Welcome

This course introduces essential tools and techniques for working with digital microscopy images using Python. It is aimed at researchers and students with some experience in microscopy and a basic familiarity with scripting. You do not need to be an expert programmer to benefit.

We’ll use real image data and widely-used open-source Python libraries.

## What will we do in this course?

By the end of the course, you will be able to:

- Open and inspect images in Python
- Explore and process multi-dimensional datasets (e.g. time series, z-stacks, multi-channel images)
- Apply filters and perform background correction
- Segment and measure biological objects (e.g. nuclei, cells)
- Use Napari for visualising and interacting with image data

## Bioimage Analysis

Bioimage analysis allows you to extract measurable information from biological samples. Examples include:

- Object size, shape, and area
- Intensity or signal distribution per region
- Cell counts, distances, and object relationships
- Colocalisation of signals across channels

A typical image analysis workflow looks like:

1. **Preprocessing** (e.g. background subtraction, filtering)
2. **Segmentation** (defining objects of interest, such as nuclei)
3. **Feature extraction** (e.g. area, intensity, shape, location)
4. **Analysis and interpretation** (e.g. plotting, classification, statistics)

## Key software tools

In this course, we’ll use:

- **Jupyter notebooks**: for writing and running Python interactively
- **NumPy**: for handling numerical arrays (which is what images are!)
- **scikit-image**: for general image processing operations
- **matplotlib**: for plotting and displaying images
- **Napari**: for interactive viewing and annotation of multi-dimensional images

All episodes use open-source tools that you can install locally or access via your institution’s JupyterHub (e.g. Noteable for University of Edinburgh users).

::::::::::::::::::::::::::::::::::::: callout
### 💡 Reflection

Have you used any of the following before?

- Jupyter notebooks
- Napari
- Python image libraries (e.g. scikit-image, OpenCV)

Take a minute to note down which tools you're already familiar with and what you'd like to learn.
::::::::::::::::::::::::::::::::::::::::::::::::

## What kind of data?

We’ll work with real microscopy images, including:

- Multi-channel fluorescence `.tif` files
- 3D z-stacks and time series
- Proprietary formats (e.g. `.nd2`, `.czi`)

We'll also cover how to read metadata, understand bit depth, and interpret image dimensions.

::::::::::::::::::::::::::::::::::::: callout
### Note: RGB vs Multichannel Images

Images like `.jpg` or `.png` use RGB colour, where each pixel contains red, green, and blue values. This format is common in photography, but also used in scientific imaging — for example, brightfield pathology slides stained with H&E or H-DAB are typically stored as RGB images.

In fluorescence microscopy, however, images are usually stored as **separate grayscale channels**, one per fluorophore (e.g. DAPI, GFP, RFP). These can be combined into a colour composite for display, but are fundamentally different from RGB images where colour is already baked in. These are the only types of images we'll look at today but it's important to know that RGB images exist and you may need to analyse and it might look a bit different from what we do today.

:::::::::::::::::::::::::::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::::

## Course structure

This course is made up of the following episodes:

1. **Introduction** (this episode)
2. **Opening and checking an image**
3. **Applying Filters**
4. **Thresholding and Segmentation**
5. **Measurements**
6. **Introduction to Napari**

Each episode includes code-along demonstrations, exercises, and challenges. 

## Meet the dataset

Here is one of the images we’ll be working with:

![Sample fluorescent image](fig/FluorescentCells_3channel_thumb.jpg){alt="Thumbnail of test image"}

This is a multi-channel fluorescent image showing nuclei, membranes, and cytoplasm in different colours.

You’ll also work with z-stacks, RGB images, and proprietary formats like `.nd2`.

➡️ See the [Reference page](../reference) for a quick recap of Python syntax and digital image basics used in this course.

---

::::::::::::::::::::::::::::::::::::: keypoints
- This course is for researchers with some Python and microscopy experience
- We will use open-source tools for exploring, processing, and analysing images
- You will learn how to work with multi-dimensional bioimages and extract useful measurements
::::::::::::::::::::::::::::::::::::::::::::::::
