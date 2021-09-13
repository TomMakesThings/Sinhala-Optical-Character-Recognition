# Sinhala-Optical-Character-Recognition

### Optical Character Recognition
An Optical Character Recognition (OCR) system is software that can take images of printed or handwritten characters and extract machine readable text.

### The Sinhalese Script
The Sinhalese script is used to write Sinhalese, the national language of Sri Lanka. It contains 58 letters of which 42 are consonants and 16 are vowels.

### K-Nearest Neighbors (KNN)
KNN works by majority voting as it assigns a class based on its k closest points.

Extract character images for training the OCR model:
* Convert each PDF to an image
* Add padding to the image to increase edge around the characters and apply a Gaussian blur
* Convert the image from colour to grayscale
* Apply an Otsu threshold
* Segment the characters in the image using bounding boxes
* Resize each character to 20 × 20 pixels
* Apply a binary threshold
