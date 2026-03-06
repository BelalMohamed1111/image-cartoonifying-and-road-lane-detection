# Image Cartoonifying and Road Lane Detection

This repository contains a two-part computer vision project focused on image stylization and feature extraction. The project explores applying image processing filters to stylize real-world images into cartoons, and building a custom Hough Transform accumulator from scratch to detect road lanes.

## Table of Contents
* [Project Overview](#project-overview)
* [Part I: Image Cartoonifying](#part-i-image-cartoonifying)
* [Part II: Road Lane Detection](#part-ii-road-lane-detection)
* [Project Structure](#project-structure)
* [Installation & Setup](#installation--setup)
* [Author](#author)

---

## Project Overview

This project explores both aesthetic image manipulation and mathematical feature extraction without relying heavily on high-level, "black-box" detection functions. All development is documented and executed within Jupyter Notebooks to serve as a visual, step-by-step log.

---

## Part I: Image Cartoonifying

The objective of this section is to make real-world images look like genuine cartoon sketches by flattening colors and emphasizing strong edges. 

**Pipeline:**
1. **Grayscale Conversion & Smoothing:** The image is converted to grayscale and passed through a Median filter to reduce noise while keeping edges sharp.
2. **Edge Detection (The Sketch):** A Laplacian filter is applied to find rapid intensity changes, followed by binary thresholding to create a stark black-and-white edge mask.
3. **Color Flattening (The Painting):** A Bilateral filter is used to smooth flat regions of the original image while preserving sharp edges. To optimize performance, smaller filter sizes are applied iteratively.
4. **Final Overlay:** The Laplacian sketch mask is overlaid onto the Bilateral painting to produce the final comic book effect.

---

## Part II: Road Lane Detection

The objective of this section is to detect road lanes using a custom implementation of the Hough Transform. **Note:** The use of built-in OpenCV Hough functions (`cv2.HoughLines`) was intentionally avoided to build the mathematical model from the ground up.

**Pipeline:**
1. **Pre-processing:** The road image is smoothed using a 2D median filter, followed by Canny edge detection with high thresholds to isolate strong lines and remove noise.
2. **Region of Interest (ROI) Masking:** A polygonal mask is applied to eliminate irrelevant edges outside the road boundaries.
3. **Custom Hough Transform:** * Implementation of the mathematical model: $x \cos \theta + y \sin \theta = \rho$.
   * Accumulation of "votes" in a 2D parameter space (accumulator array) for every edge point.
4. **Post-Processing:** Searching the parameter space for the highest peaks and applying non-maximum suppression to filter out inaccuracies and draw the final lane lines.

---

## Project Structure

```text
image-cartoonifying-and-road-lane-detection/
├── part1_cartoonifier/
│   ├── Part1_Cartoonifier.ipynb
│   └── assets/ 
├── part2_lane_detection/
│   ├── Part2_LaneDetection.ipynb
│   └── assets/
├── requirements.txt
└── README.md
