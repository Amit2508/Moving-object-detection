1. Importing the necessary libraries

2. Initializing the camera capture

3: Giving some time for the camera to warm up

4: Initializing variables for frame comparison and area threshold

5: Starting an infinite loop for video processing

6: Reading the current frame from the camera:

_, img = cam.read()

7: Setting the initial text to "Normal" (assuming no moving objects)

8: Resizing the frame to a width of 500 pixels using imutils library

9: Converting the resized frame to grayscale:

grayImg = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

10: Applying Gaussian blur to the grayscale image to reduce noise:

gaussianImg = cv2.GaussianBlur(grayImg, (21, 21), 0)

11:Checking if it is the first frame:

if firstFrame is None:
    firstFrame = gaussianImg
    continue
    
 12 : Calculating the absolute difference between the current frame and the first frame
 
 imgDiff = cv2.absdiff(firstFrame, gaussianImg)

13: Thresholding the difference image to create a binary image:


threshImg = cv2.threshold(imgDiff, 25, 255, cv2.THRESH_BINARY)[1]

14  : Dilating the thresholded image to fill in gaps:


threshImg = cv2.dilate(threshImg, None, iterations=2)

15 : Finding contours in the thresholded image:


cnts = cv2.findContours(threshImg.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
cnts = imutils.grab_contours(cnts)

16 : Iterating over the contours and checking their area
  
  for c in cnts:
    if cv2.contourArea(c) < area:
        continue
    (x, y, w, h) = cv2.boundingRect(c)
    cv2.rectangle(img, (x, y), (x + w, y + h), (0, 255, 0), 2)
    text = "Moving Object detected"


17 Printing the detected object status:


print(text)
18 : 
Drawing the status text on the image:


cv2.putText(img, text, (10, 20), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 255), 2)

19 : 
Displaying the image with object detection:


cv2.imshow("cameraFeed", img)

20: 
Checking for the 'q' key to break the loop and exit the program:


key = cv2.waitKey(


