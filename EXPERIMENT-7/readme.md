import cv2
from google.colab.patches import cv2_imshow

# Load the image using the correct path
image = cv2.imread("/content/images.jpg")

if image is None:
    print("Error: Could not load the image from /content/images.jpg. Please make sure the file exists.")
else:
    # Convert the image to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # Display the original image
    print("Original Image:")
    cv2_imshow(image)
    
    # Display the grayscale image
    print("Grayscale Image:")
    cv2_imshow(gray_image)
