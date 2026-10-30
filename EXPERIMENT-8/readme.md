import cv2
from google.colab.patches import cv2_imshow

# Load the image from the specified path
image = cv2.imread('/content/images.jpg')

# Check if the image loaded successfully
if image is None:
    print("Error: Could not load the image. Please verify the file path.")
else:
    # Convert the image to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # Display the images using Colab's cv2_imshow patch
    print("Original Image:")
    cv2_imshow(image)
    
    print("Grayscale Image:")
    cv2_imshow(gray_image)
