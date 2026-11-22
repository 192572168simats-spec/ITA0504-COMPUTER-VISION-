import numpy as np
import cv2
from google.colab.patches import cv2_imshow

def create_colored_corners(image_size):
    height, width = image_size # Extract height and width
    # Create a white image (3D array of ones scaled to 255 for RGB)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    # Calculate the size of the colored boxes (1/10th of image size)
    box_h, box_w = height // 10, width // 10
    # Define corner regions and their colors (OpenCV uses BGR layout)
    image[:box_h, :box_w] = [0, 0, 0] # Top-left (Black)
    image[:box_h, -box_w:] = [255, 0, 0] # Top-right (Blue in BGR)
    image[-box_h:, :box_w] = [0, 255, 0] # Bottom-left (Green)
    image[-box_h:, -box_w:] = [0, 0, 255] # Bottom-right (Red in BGR)
    
    # Display the image using Colab patch
    print("Generated Corner Colored Image:")
    cv2_imshow(image)

# Example usage with preset dimensions to avoid blocking the runtime
user_width = 400
user_height = 400
create_colored_corners((user_height, user_width))
