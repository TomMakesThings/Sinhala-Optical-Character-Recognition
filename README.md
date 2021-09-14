# Sinhala Script Optical Character Recognition

## About
The aim of this project was to experiment creating a basic optical character recognition (OCR) system that can take images of printed Sinhalese characters, Sinhala being the national language of Sri Lanka, and to convert them to machine readable text using a KNN classifier.

---

## Training and Testing Data
To generate training and testing data, I created PDFs of Sinhalese characters with different font weights and matching text files to store the ground truth. After reading the PDFs into the [notebook](https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/SinhalaOCR.ipynb), they are converted to images.

For each image, padding is added to increase the margin of the page and a Gaussian blur applied to merge parts of characters that are close together. The image is then converted to grayscale and adaptive thresholding applied using Otsu's method to separate the background from the foreground (see example with training data below).

<a href="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/SinhalaOCR.ipynb"><img src="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/Images/Training-Image-Extraction.png" width=780></a>

Next the image is converted to binary and regions of interest (ROIs) are identified. ROIs are first sorted by their y coordinates to find characters on the same line, and then by x to determine the order on the page.

<a href="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/SinhalaOCR.ipynb"><img src="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/Images/Training-ROI-Threshold.png" width=400></a>

Finally, each ROI resized to 20 x 20 pixels. This is because the classifier requires all input images to be the same size.

<a href="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/SinhalaOCR.ipynb"><img src="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/Images/Training-ROIs.png"></a>

####

---

## K-Nearest Neighbors (KNN)
KNN is a type of classifier that uses majority voting to assigns a class to each data point based on its k closest points. After the extracted ROIs are matched to their labels, the KNN classifier is fit to the training data. Then the KNN is used to make a prediction on the test data and the predicted and expected text compared.

<a href="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/SinhalaOCR.ipynb"><img src="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/Images/Testing-Boxes.png" width=400></a>

```
Prediction: ථළභඦඹශඝඖරඨෆඦඤදධඣඏඋඏධටඝෆඵයවෂෂඉඅටකචඤ
Actual:     ථළභඦඹශඝඖරඨෆඦඤදධඣඏඋඏධටඝෆඵයවෂෂඉආකචඤඏ
```

With OCR, image-label shifts are a common occurrence. For example, at the end `අ ට ක ච ඤ` was predicted when the expected text was `ආ ක ච ඤ ඏ`. In this case the label at index 1 would not match image 1, label 2 would match image 2 etc. This means a measure such as accuracy is not suitable to measure performance.

Instead the Levenshtein distance and Jaro distance are calculated. The Levenshtein distance counts the number of edits (insertions, deletions and substitutions) required to convert the prediction to the actual text, while the Jaro distance is a string-edit distance between [0,1], where 0 represents dissimilar strings and 1 represents identical strings.

```
Levenshtein distance: 3
Jaro distance: 0.961
```

To evaluate the quality of the classifier's output, a confusion matrix is plotted. This reveals how good the classifier is at predicting each character (true positives are plotted on the diagonal line) and for those it get incorrect, which ones it predicts instead.

<a href="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/SinhalaOCR.ipynb"><img src="https://github.com/TomMakesThings/Sinhala-Optical-Character-Recognition/blob/main/Images/Confusion-Matrix.png" width=800></a>
