# Sinhala Script Optical Character Recognition

## About
The aim of this project was to experiment creating a basic optical character recognition (OCR) system that can take images of printed Sinhalese characters, Sinhala being the national language of Sri Lanka, and to convert them to machine readable text using a KNN classifier.

---

## Training Data
To generate training and testing data, I created PDFs of Sinhalese characters with different font weights and matching text files to store the ground truth. After reading the PDFs into the notebook, they are converted to images.

For each image, padding is added to increase the margin of the page and a Gaussian blur applied to merge parts of characters that are close together. The image is then converted to grayscale and adaptive thresholding applied using Otsu's method to separate the background from the foreground.

Next the image is converted to boolean and regions of interest (ROIs) are identified. ROIs are first sorted by their y coordinates to find characters on the same line, and then by x to determine the order on the page. Finally, each ROI resized to 20 x 20 pixels as the classifier requires all input images to be the same size.

---

## K-Nearest Neighbors (KNN)
KNN is a type of classifier that uses majority voting to assigns a class to each data point based on its k closest points. After the extracted ROIs are matched to their labels, the KNN classifier is fit to the training data. Then the KNN is used to make a prediction on the test data and the predicted and expected text compared.

To quantify the performance, both the Levenshtein distance and Jaro–Winkler distance are calculated.
```
Prediction: ථළභඦඹශඝඖරඨෆඦඤදධඣඏඋඏධටඝෆඵයවෂෂඉඅටකචඤ
Actual:     ථළභඦඹශඝඖරඨෆඦඤදධඣඏඋඏධටඝෆඵයවෂෂඉආකචඤඏ
```

```
Levenshtein distance: 3
Jaro–Winkler distance: 0.961
```
