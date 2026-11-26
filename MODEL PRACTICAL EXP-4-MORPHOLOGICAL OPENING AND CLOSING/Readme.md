import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the image in grayscale
img = cv2.imread('/content/images.jpg', 0)

if img is None:
    print("Error: Could not open or find the image '/content/images.jpg'")
else:
    # Apply binary thresholding
    _, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

    # Define a 5x5 structuring element (kernel)
    kernel = np.ones((5, 5), np.uint8)

    # Perform opening (erosion followed by dilation)
    opening = cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)

    # Perform closing (dilation followed by erosion)
    closing = cv2.morphologyEx(binary, cv2.MORPH_CLOSE, kernel)

    # Save the output images
    cv2.imwrite('opening.jpg', opening)
    cv2.imwrite('closing.jpg', closing)

    # Display the results inline using Matplotlib
    plt.figure(figsize=(12, 4))

    plt.subplot(1, 3, 1)
    plt.imshow(binary, cmap='gray')
    plt.title('Binary Image')
    plt.axis('off')

    plt.subplot(1, 3, 2)
    plt.imshow(opening, cmap='gray')
    plt.title('Opening (Noise Removal)')
    plt.axis('off')

    plt.subplot(1, 3, 3)
    plt.imshow(closing, cmap='gray')
    plt.title('Closing (Hole Filling)')
    plt.axis('off')

    plt.tight_layout()
    plt.show()
