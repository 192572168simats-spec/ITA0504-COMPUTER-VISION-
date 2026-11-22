import numpy as np
import cv2
from google.colab.patches import cv2_imshow

def create_circle_image(image_size, save_path=None):
    height, width = image_size # Extract height and width
    # Create a white image (3D array of ones scaled to 255 for RGB)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    # Define the circle properties
    center = (width // 2, height // 2) # Center of the image
    radius = min(width, height) // 4 # Radius is 1/4th of the smallest dimension
    # Draw the circle (color: Red in BGR, thickness: 2)
    cv2.circle(image, center, radius, (0, 0, 255), 2)
    
    # Save the image if a path is provided
    if save_path:
        cv2.imwrite(save_path, image)
        print(f"Image successfully saved to {save_path}")
        
    # Display the image
    cv2_imshow(image)

# Execute the function to display and save the circle
create_circle_image((400, 400), save_path="/content/circle_output.jpg")
