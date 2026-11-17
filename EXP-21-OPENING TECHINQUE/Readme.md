import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input image
image = cv2.imread('/content/images.jpg')
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Define a structuring element (5x5 kernel)
kernel = np.ones((5,5), np.uint8)

# Perform morphological opening (erosion followed by dilation)
opened_image = cv2.morphologyEx(gray_image, cv2.MORPH_OPEN, kernel)

# Save result
cv2.imwrite('opened_image.jpg', opened_image)

# Display the results inline using matplotlib
plt.figure(figsize=(12, 6))

plt.subplot(1, 2, 1)
plt.imshow(image_rgb)
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(opened_image, cmap='gray')
plt.title('Opened Image (Grayscale)')
plt.axis('off')

plt.tight_layout()
plt.show()
