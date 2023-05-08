# Face-Dectection-Project

An Easy way of detecting faces using Haar cascades in OpenCV and Python.😊😊😊

<br>

# Project Guide
This project requires python package "opencv".

You can install it using pip:
```
pip install opencv-python
```
+ Face detection using Haar cascades is a machine learning based approach where a cascade function is trained with a set of input data. 

+ OpenCV already contains many pre-trained classifiers for face, eyes, smiles, etc.. here we use face classifier. You can experiment with other classifiers as well.

You need to download the trained classifier XML file (haarcascade_frontalface_default.xml), which is available in OpenCv’s GitHub repository. Save it to your working location.

Download from here(OFFICIAL):

+ > Raw format - https://raw.githubusercontent.com/opencv/opencv/master/data/haarcascades/haarcascade_frontalface_default.xml

+ > xml file - https://github.com/opencv/opencv/tree/master/data/haarcascades

## To detect faces in images:
file name : detect_face.py

```
import cv2

## Load the cascade

face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')

## Read the input image

img = cv2.imread('test.jpg')

## Convert into grayscale

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

## Detect faces

faces = face_cascade.detectMultiScale(gray, 1.1, 4)

## Draw rectangle around the faces

for (x, y, w, h) in faces:
cv2.rectangle(img, (x, y), (x+w, y+h), (255, 0, 0), 2)


## Display the output

cv2.imshow('img', img)

cv2.waitKey()
```
# A few things to note:

+ The detection works only on grayscale images. So it is important to convert the color image to grayscale.

+ detectMultiScale function is used to detect the faces. It takes 3 arguments — the input image, scaleFactor and minNeighbours. scaleFactor specifies how much the image size is reduced with each scale. minNeighbours specifies how many neighbors each candidate rectangle should have to retain it. You can read about it in detail here. You may have to tweak these values to get the best results.

+ faces contains a list of coordinates for the rectangular regions where faces were found. We use these coordinates to draw the rectangles in our image.

we can also detect faces in videos. As you know videos are basically made up of frames, which are still images. So we perform the face detection for each frame in a video. Here is the code:
file name : detect_face_vid.py
```
import cv2

#Load the cascade

face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')



#To capture video from webcam. 

cap = cv2.VideoCapture(0)

#To use a video file as input 

#cap = cv2.VideoCapture('filename.mp4')

while True:

#Read the frame

_, img = cap.read()

#Convert to grayscale

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

#Detect the faces

faces = face_cascade.detectMultiScale(gray, 1.1, 4)

#Draw the rectangle around each face

for (x, y, w, h) in faces:

cv2.rectangle(img, (x, y), (x+w, y+h), (255, 0, 0), 2)

#Display

cv2.imshow('img', img)

#Stop if escape key is pressed

k = cv2.waitKey(30) & 0xff

if k==27:

break

#Release the VideoCapture object

cap.release()
```

The only difference here is that we use an infinite loop to loop through each frame in the video. We use cap.read() to read each frame. 

The 
first value returned is a flag that indicates if the frame was read correctly or not. We don’t need it. The second value returned is the still 
frame on which we will be performing the detection.
