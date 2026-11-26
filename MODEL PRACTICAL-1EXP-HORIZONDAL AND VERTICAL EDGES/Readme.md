import cv2
import numpy as np
import matplotlib.pyplot as plt

# Install pillow-heif if not already present to add AVIF support to Pillow
try:
    import pillow_heif
    pillow_heif.register_heif_opener()
except ImportError:
    !pip install pillow-heif -q
    import pillow_heif
    pillow_heif.register_heif_opener()

from PIL import Image

# Read the AVIF image and convert to grayscale
pil_img = Image.open('/content/photo-1651787957245-3d760746a717.avif')
img = np.array(pil_img.convert('L'))

# Sobel X direction (detects vertical lines)
gx = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)

# Sobel Y direction (detects horizontal lines)
gy = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)

# Convert gradients into display format
gx = cv2.convertScaleAbs(gx)
gy = cv2.convertScaleAbs(gy)

# Calculate combined magnitude
magnitude = np.sqrt(gx.astype(float)**2 + gy.astype(float)**2)
result = cv2.convertScaleAbs(magnitude)

# Display the results inline
fig, axes = plt.subplots(2, 2, figsize=(12, 10))
axes[0, 0].imshow(img, cmap='gray')
axes[0, 0].set_title('Original Image (Grayscale)')
axes[0, 0].axis('off')

axes[0, 1].imshow(gy, cmap='gray')
axes[0, 1].set_title('Horizontal Edges (Sobel Y)')
axes[0, 1].axis('off')

axes[1, 0].imshow(gx, cmap='gray')
axes[1, 0].set_title('Vertical Edges (Sobel X)')
axes[1, 0].axis('off')

axes[1, 1].imshow(result, cmap='gray')
axes[1, 1].set_title('Combined Edges')
axes[1, 1].axis('off')

plt.tight_layout()
plt.show()

# Save outputs
cv2.imwrite('horizontal.jpg', gy)
cv2.imwrite('vertical.jpg', gx)
cv2.imwrite('result.jpg', result)
