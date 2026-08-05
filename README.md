# Color Recognition using OpenCV

This project detects the **red color** in an image using **OpenCV** and **NumPy**. It converts the image from the BGR color space to HSV, creates a mask for the red color, detects the red object, and draws a bounding box around it.

The example below demonstrates the detection of the **red light** in a traffic signal.

## Features

- Read an image from a file.
- Convert the image from BGR to HSV.
- Detect the red color using HSV thresholds.
- Create a binary mask for the red color.
- Find the detected object's contours.
- Draw a green bounding box around the detected object.
- Display the detected object with the label **"Red"**.

## Technologies Used

- Python
- OpenCV
- NumPy

## How It Works

1. Load the image.
2. Convert the image to the HSV color space.
3. Define the HSV range for the red color.
4. Create a mask containing only red pixels.
5. Detect the contours of the red object.
6. Draw a rectangle and label around the detected object.
7. Display the final result.

## Code

```python
import cv2
import numpy as np

img = cv2.imread("img.webp")

hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

lower_red = np.array([0, 120, 70])
upper_red = np.array([10, 255, 255])

mask = cv2.inRange(hsv, lower_red, upper_red)

contours, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

for c in contours:
    if cv2.contourArea(c) > 500:
        x, y, w, h = cv2.boundingRect(c)
        cv2.rectangle(img, (x, y), (x + w, y + h), (0, 255, 0), 2)
        cv2.putText(img, "Red", (x, y - 10),
                    cv2.FONT_HERSHEY_SIMPLEX, 0.8, (0, 255, 0), 2)

cv2.imshow("Result", img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## Result

The program successfully detects the **red traffic light** and highlights it with a green bounding box and the label **"Red"**.

<img width="1206" height="800" alt="Screenshot 2026-07-25 224732" src="https://github.com/user-attachments/assets/a16e5896-6866-4231-862b-14605dc118b2" />
