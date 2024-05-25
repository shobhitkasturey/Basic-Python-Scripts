# Photo Capture Program#

Introduction

This program captures a photo whenever a specified key is pressed. The captured photos are saved in a defined directory with unique filenames based on the current date and time.
Dependencies

Before running the program, ensure you have the following dependencies installed:

    OpenCV: for capturing and displaying video.
    datetime: for generating unique filenames.

Installation

To install the necessary dependencies, run the following commands:

sh

    pip install opencv-python
    pip install datetime

How to Use the Program
Step 1: Define the Key and Directory

The program defines a key (p by default) which, when pressed, will capture a photo. It also defines a directory where the photos will be saved.

python

    key = 'p'
    directory = 'M:\\photocap'

Step 2: Open the Camera

The program uses OpenCV to open the camera of the device.

python

     capture = cv2.VideoCapture(0)

    if not capture.isOpened():
       print("Error opening camera")
       exit()

Step 3: Capture Photos

The program enters an infinite loop where it continuously captures frames from the camera and displays them in a window.

python

    while True:    
        ret, frame = capture.read()
          if ret:
          cv2.imshow('Camera', frame)

Step 4: Save Photos on Key Press

Inside the loop, the program checks if the specified key (p) is pressed. If pressed, it saves the current frame as an image in the specified directory with a unique filename.

python

        if cv2.waitKey(1) & 0xFF == ord(key):
            filename = f"photo_{datetime.now().strftime('%Y%m%d_%H%M%S')}_{count}.jpg"
            filepath = os.path.join(directory, filename)
            cv2.imwrite(filepath, frame)
            count += 1

Step 5: Exit the Program

The program also checks if the 'q' key is pressed to exit the loop and close the camera.

python

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

Step 6: Release Resources

After exiting the loop, the program releases the camera and closes all OpenCV windows.

python

    capture.release()
    cv2.destroyAllWindows()

Full Code

python

     import os
    import cv2
    from datetime import datetime

    key = 'p'
    directory = 'M:\\photocap'  

    capture = cv2.VideoCapture(0)

    if not capture.isOpened():
      print("Error opening camera")
      exit()
    
    count = 0  

    while True:    
        ret, frame = capture.read()
          if ret:
            cv2.imshow('Camera', frame)
              if cv2.waitKey(1) & 0xFF == ord(key):
                 filename = f"photo_{datetime.now().strftime('%Y%m%d_%H%M%S')}_{count}.jpg"
                 filepath = os.path.join(directory, filename)
                 cv2.imwrite(filepath, frame)
                 count += 1
          if cv2.waitKey(1) & 0xFF == ord('q'):  
           break
    capture.release()
    cv2.destroyAllWindows()

Conclusion

This program allows users to capture multiple images using their device's camera by pressing a defined key. Each image is saved with a unique filename to avoid overwriting previous images. The program continues to run until the user presses the 'q' key to exit.
