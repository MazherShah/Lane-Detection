Here is a `README.md` file drafted based on your project documentation and repository details:

```markdown
# [cite_start]Advanced Lane Detection of the Road using Computer Vision Techniques [cite: 17]

## Project Overview
[cite_start]This project evaluates and implements a complete software pipeline for identifying road lane boundaries in real-time video streams[cite: 14, 15]. [cite_start]Based on the Udacity Self-Driving Car Engineer Nanodegree curriculum, the system applies classical image processing and computer vision techniques to detect and visualize road lane lines from dashcam video footage[cite: 15, 19]. 

[cite_start]Beyond simple detection, the pipeline calculates key metrics essential for autonomous driving systems, augmenting the output video with the road's radius of curvature and the vehicle's center offset[cite: 20].

## Repository Details
* [cite_start]**Repository:** [MazherShah/Lane-Detection](https://github.com/MazherShah/Lane-Detection) [cite: 102]
* **Main Code:** `Lane Detection.ipynb`

### Contributors
* [cite_start]**Mazher Ali Shah** (23108121) - GitHub: MazherShah [cite: 11, 102]
* [cite_start]**Jahanzaib Ibrahim Khan** (23108116) - GitHub: jahanzaibibra [cite: 10]

[cite_start]**Department:** Department of Robotics & Artificial Intelligence [cite: 12]
[cite_start]**Supervisor:** Mr. Muhammad Azhar [cite: 8]

---

## Core Pipeline Steps
The lane detection pipeline consists of the following image processing steps:

1. [cite_start]**Camera Calibration:** Uses chessboard images to compute and apply distortion coefficients[cite: 22].
2. [cite_start]**Distortion Correction:** Applied to raw input images to account for camera lens distortion[cite: 23].
3. [cite_start]**Thresholding:** Applies color space transforms (like HLS to isolate yellow/white) and gradient thresholding (Sobel) to create distinct binary images[cite: 24, 38].
4. [cite_start]**Perspective Transform:** Warps the image to a "Birds-Eye View" to rectify the binary images and accurately measure lane curvature[cite: 25, 38].
5. [cite_start]**Lane Detection:** Detects lane pixels column by column using a histogram-based sliding window search and isolates bright regions via Morphological Top-Hat[cite: 26, 38].
6. [cite_start]**Curve Fitting:** Applies polynomial curve fitting (2nd order) to identify the lane boundaries through the detected pixels[cite: 27, 38].
7. [cite_start]**Calculations:** Calculates the lane curvature (converted to real-world meters) and the vehicle's offset from the center of the lane[cite: 28, 38].
8. [cite_start]**Result Overlay:** Uses inverse perspective transforms to draw the detected lanes and data onto the original video frames[cite: 29].

---

## Technologies Used
[cite_start]The project utilizes an open-source technology stack[cite: 40]:
* [cite_start]**Python (3.x):** Primary programming language[cite: 31].
* [cite_start]**OpenCV (cv2):** Image processing and computer vision algorithms[cite: 31].
* [cite_start]**NumPy:** Numerical computation and array operations[cite: 31].
* [cite_start]**Matplotlib:** Visualization and image display[cite: 31].
* [cite_start]**MoviePy:** Video processing and output generation[cite: 31].
* [cite_start]**Jupyter Notebook / Anaconda:** Development, environment management, and experimentation[cite: 31].

---

## Datasets
[cite_start]The project uses the publicly available **Udacity Self-Driving Car Dataset**[cite: 43]. The footage tests the pipeline under various conditions, including:
* [cite_start]Standard road footage (straight and curved scenarios)[cite: 45].
* [cite_start]Challenge videos with varying lighting, shadows, and pavement colors[cite: 46].
* [cite_start]Harder challenge videos featuring sharp curves and rapid lighting changes[cite: 47].

---

## Known Limitations & Challenges
* **Environmental Variables:** High variations in lighting, heavy shadows, and differing weather conditions (rain, snow, night) can impact edge/color thresholds. [cite_start]Adaptive thresholding and Top-Hat morphological operations are used to mitigate shadows[cite: 49].
* **Road Topology:** The pipeline may struggle on very sharp road curves or lane merges/crossings. [cite_start]The current scope is optimized primarily for highway and freeway scenarios[cite: 49].
* **Processing Speed:** The current single-frame pipeline is computationally heavy. [cite_start]While highly feasible for academic demonstration, real-time processing speed is noted as an area for future optimization[cite: 49].

---

## References & Acknowledgments
1. [cite_start]Udacity Self-Driving Car Engineer Nanodegree — Advanced Lane Finding Project[cite: 106].
2. Bradski, G. (2000). [cite_start]The OpenCV Library[cite: 107].
3. Ayanzadeh, A. (2017). [cite_start]Udacity Advanced Lane Detection of the Road[cite: 105].
```
