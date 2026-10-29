import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the selected image
image = cv2.imread('/content/images.jpg')

# Convert to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply histogram equalization
equalized_image = cv2.equalizeHist(gray_image)

# Display the results
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

axes[0].imshow(gray_image, cmap='gray')
axes[0].set_title('Original Grayscale Image')
axes[0].axis('off')

axes[1].imshow(equalized_image, cmap='gray')
axes[1].set_title('Histogram Equalized Image')
axes[1].axis('off')

plt.tight_layout()
plt.show()
