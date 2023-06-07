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


