import cv2
from google.colab.patches import cv2_imshow

# Read the user selected image
image = cv2.imread("/content/images.jpg")

if image is None:
    print("Error: Could not load the image. Please verify the file path.")
else:
    # Convert to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # Display the images using Colab's patches
    print("Original Image:")
    cv2_imshow(image)
    
    print("Grayscale Image:")
    cv2_imshow(gray_image)
