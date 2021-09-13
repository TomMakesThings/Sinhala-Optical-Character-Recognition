# Sinhala Optical Character Recognition

## About
The aim of this project was to experminet creating a basic optical character recognition (OCR) system that can take images of printed Sinhalese characters, Sinhala being the national language of Sri Lanka, and to convert them to machine readable text using a KNN classifier.

---

## Approach
#### Training Data
To generate training data, I created PDFs of Sinhalese characters with different font weights and matching text files to store the ground truth. After reading the PDFs into the notebook, they are converted to images.

For each image, padding is added to increase the margin of the page and a Gaussian blur applied to merge parts of characters that are close together. The image is then converted to grayscale and adaptive thresholding applied using Otsu's method to separate the background from the foreground.

Next the image is converted to boolean and regions of interest (ROIs) are identified. ROIs are first sorted by their y coordinates to find characters on the same line, and then by x to determine the order on the page. Finally, each ROI resized to 20 x 20 pixels as the classifier requires all input images to be the same size.

# Testing Data
Matching training labels are read from .txt files. If more labels are found than images, then unlabeled images are removed from the 
data set to prevent errors. Similarly, if more images are found, 
remaining labels are removed. Testing images and labels are gathered
using the same methods as for training.

<br>

#### K-Nearest Neighbors (KNN)
KNN works by majority voting as it assigns a class based on its k closest points.

#### Evaluation Metrics
Levenshtein distance
Jaro–Winkler distance
