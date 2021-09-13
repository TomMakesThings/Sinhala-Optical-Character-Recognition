# Sinhala Optical Character Recognition

## About
The aim of this project was to experminet creating a basic optical character recognition (OCR) system that can take images of printed Sinhalese characters, Sinhala being the national language of Sri Lanka, and to convert them to machine readable text using a KNN classifier.

---

## Approach
#### Training and Testing Data
To generate training and testing data, I created PDFs of Sinhalese characters with differnt font weights and matching text files to store the ground truth. After reading the PDFs into the notebook, they are converted to images.

For each image, padding is added to increase the margin of the page and a Gaussian blur applied to merge parts of characters that are close together. The image is then converted to grayscale and adaptive thresholding applied using Otsu's method to separate the background from the foreground.

Finally the image is converted into boolean values and regions of interest (ROIs) are identified. These are sorted by x coordinate and resized as 20 x 20 images as the classifier requires a standard size.

#### K-Nearest Neighbors (KNN)
KNN works by majority voting as it assigns a class based on its k closest points.

#### Evaluation Metrics
Levenshtein distance
Jaro–Winkler distance
