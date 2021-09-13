# Sinhala Optical Character Recognition

### About
The purpose of this project is to create a basic optical character recognition (OCR) system that can take images of printed Sinhalese characters, the national language of Sri Lanka, and to convert them to machine readable text using a KNN classifier.

---

images of text are inputted and the system will identify regions of interest (ROIs) which it will attempt to classify.

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

### Evaluation Metrics
Levenshtein distance
Jaro–Winkler distance
