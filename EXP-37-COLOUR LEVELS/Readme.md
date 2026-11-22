import cv2
import numpy as np
from google.colab.patches import cv2_imshow

def subtract_foreground(image_path, lower_color, upper_color):
    # Read the image
    image = cv2.imread(image_path)
    if image is None:
        print(f"Could not load the image from {image_path}.")
        return

    # Convert to HSV color space
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)

    # Define lower and upper range for foreground color (adjust as needed)
    lower_bound = np.array(lower_color, dtype=np.uint8)
    upper_bound = np.array(upper_color, dtype=np.uint8)

    # Create mask to isolate the desired range
    mask = cv2.inRange(hsv, lower_bound, upper_bound)

    # Extract the background
    background = cv2.bitwise_and(image, image, mask=mask)

    # Display results
    print("Original Image:")
    cv2_imshow(image)
    print("Isolated Color Range:")
    cv2_imshow(background)
