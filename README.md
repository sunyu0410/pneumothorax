# Pneumothorax segmentation
This document is a work solution to the Kaggle competition on pneumothorax segmentation from X-ray images. 

There are two stages with corresponding Jupyter Notebook.
1. Explorative data analysis
2. Model development

## Pneumothorax
Pneumothorax is a medical condition where the lung is collapsed. Severe pneumothorax can lead to emergency. A normal lung will fill the thorax leaving no extra space in between. Pneumothorax is visually identified on X-ray images by looking for spaces between the lung boundary and the thorax. 

## Data
X-ray images are provided from the competition in DICOM (`.dcm`) format, which can be manipulated using the `pydicom` or `SimpleITK` library. The competition released a dataset containing a total of 12089 training images and 3205 test images. The training image comes with a unique identifier (`ImageID`) and the ground truth annotations as binary mask, with the pixel coordinates stored in the run-length encoding (`EncodedPixels`). For example, '1 3 10 5' contains two runs: pixels 1,2,3 and pixels 14,15,16,17,18. Images without pneumothorax are labelled with `-1`. An example of such correspondence is shown below.

```
ImageId,                 EncodedPixels
0004d4463b50_01,        -1
0004d4463b50_02,         1 10
0004d4463b50_03,         1 30 3 5
...
```

At the end, the contours will be converted to a mask, with the same size as the corresponding X-ray images.

## Task
The goal is to train a segmentation model that takes a X-ray image and output the binary mask for pneumothorax. Mean Dice will be used to evaluate the performance on the held out test data. 

More details can be found on the [competition page](https://www.kaggle.com/c/siim-acr-pneumothorax-segmentation).
