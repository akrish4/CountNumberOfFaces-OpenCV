<h1><p align="center">  CountNumberOfFaces-OpenCV  <p/></h1>

In this project, I will use image processing to detect and count the number of faces. We are not supposed to get all the features of the face. Instead, the objective is to obtain the bounding box through some methods i.e. coordinates of the face in the image, depending on different areas covered by the number of the coordinates, number faces that will be computed.


## Required libraries:
### opencv 
- library in python is a computer vision library, mostly used for image processing, video processing, and analysis, facial recognition and detection, etc.
### Dlib library 
- Dlib library in python contains the pre-trained facial landmark detector, that is used to detect the (x, y) coordinates that map to facial structures on the face.
### Numpy 
- Numpy is a general-purpose array-processing package. It provides a high-performance multidimensional array object and tools for working with these arrays.

## Procedure : 
Step 1: Import required libraries. 
```
import cv2
import dlib
import numpy as np
```

Step 2: Open the default camera to capture faces and use the dlib library to get coordinates.
```
# (0) in VideoCapture is used to
# connect to your computer's default camera
cap = cv2.VideoCapture(0)
# Get the coordinates
detector = dlib.get_frontal_face_detector()

```

Step 3: Count the number of faces.
 - Capture the frames continuously.
 - Convert the frames to grayscale(not necessary).
 - Take an iterator i and initialize it to zero.
 - Each time you get the coordinates to the face structure in the frame, increment the iterator by 1.
 - Plot the box around each detected face along with its face count.
```
while True:

	# Capture frame-by-frame
	ret, frame = cap.read()
	frame = cv2.flip(frame, 1)

	# Our operations on the frame come here
	gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
	faces = detector(gray)

	# Counter to count number of faces
	i = 0
	for face in faces:
		x, y = face.left(), face.top()
		x1, y1 = face.right(), face.bottom()
		cv2.rectangle(frame, (x, y), (x1, y1), (0, 255, 0), 2)

		# Incrment the iterartor each time you get the coordinates
		i = i+1

		# Adding face number to the box detecting faces
		cv2.putText(frame, 'face num'+str(i), (x-10, y-10),
					cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0, 0, 255), 2)
		print(face, i)

	# Display the resulting frame
	cv2.imshow('frame', frame)
```

Step 4: Terminate the loop.
``` 
# Enter key 'q' to break the loop
if cv2.waitKey(1) & 0xFF == ord('q'):
	break
```
Step 5: Clear windows.
```
# When everything done, release
# the capture and destroy the windows
cap.release()
cv2.destroyAllWindows()
```

## Output 


  
  <img src="https://github.com/akrish4/CountNumberOfFaces-OpenCV/blob/main/image/image1.png" width="425"/>  
