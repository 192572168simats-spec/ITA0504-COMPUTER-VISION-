import cv2
import numpy as np
import matplotlib.pyplot as plt

# Compute Laplacian edge detection (using a 64-bit float to capture negative gradients)
laplacian = cv2.Laplacian(gray, cv2.CV_64F, ksize=3)
laplacian = cv2.convertScaleAbs(laplacian)

# Save Laplacian result
cv2.imwrite("laplacian.jpg", laplacian)

# Compare Sobel Combined vs Laplacian side-by-side
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(image_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 3, 2)
plt.imshow(sobel_combined, cmap="gray")
plt.title("Sobel Combined (1st Derivative)")
plt.axis("off")

plt.subplot(1, 3, 3)
plt.imshow(laplacian, cmap="gray")
plt.title("Laplacian (2nd Derivative)")
plt.axis("off")

plt.tight_layout()
plt.show()
