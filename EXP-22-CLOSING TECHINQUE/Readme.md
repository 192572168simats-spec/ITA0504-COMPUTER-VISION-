import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the correct image path
image = cv2.imread('/content/images.jpg')
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Top-hat morphological operation
kernel = np.ones((5,5), np.uint8)
top_hat_image = cv2.morphologyEx(gray_image, cv2.MORPH_TOPHAT, kernel)

# Display the results using matplotlib instead of cv2.imshow
fig, axes = plt.subplots(1, 2, figsize=(12, 6))
axes[0].imshow(image_rgb)
axes[0].set_title('Original Image')
axes[0].axis('off')

axes[1].imshow(top_hat_image, cmap='gray')
axes[1].set_title('Top Hat Image')
axes[1].axis('off')

plt.tight_layout()
plt.show()
