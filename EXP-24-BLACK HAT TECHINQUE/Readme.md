import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the correct image in grayscale
image = cv2.imread('/content/images.jpg', cv2.IMREAD_GRAYSCALE)

# Define a kernel (5x5 structuring element)
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))

# Apply the Black Hat transformation
blackhat = cv2.morphologyEx(image, cv2.MORPH_BLACKHAT, kernel)

# Display the results using matplotlib
fig, axes = plt.subplots(1, 2, figsize=(12, 6))
axes[0].imshow(image, cmap='gray')
axes[0].set_title('Original Grayscale Image')
axes[0].axis('off')

axes[1].imshow(blackhat, cmap='gray')
axes[1].set_title('Black Hat Image')
axes[1].axis('off')

plt.tight_layout()
plt.show()
