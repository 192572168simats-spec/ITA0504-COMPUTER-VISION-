import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the image using the correct path
image = cv2.imread("/content/images.jpg")
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Convert to float32 as required by cornerHarris
gray = np.float32(gray)

# Apply Harris Corner Detection
# Parameters: src image, neighborhood size (blockSize), aperture parameter for Sobel (ksize), Harris detector free parameter (k)
dest = cv2.cornerHarris(gray, blockSize=2, ksize=3, k=0.04)

# Dilate the results to mark the corners clearly
dest = cv2.dilate(dest, None)

# Create an image copy to overlay detected corners in red
corner_img = image.copy()
corner_img[dest > 0.01 * dest.max()] = [0, 0, 255] # Red color in BGR

# Save the corner-detected image
cv2.imwrite("harris_corners.jpg", corner_img)

# Convert BGR to RGB for correct matplotlib plotting
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
corner_img_rgb = cv2.cvtColor(corner_img, cv2.COLOR_BGR2RGB)

# Display original and corner-detected images side-by-side
fig, axes = plt.subplots(1, 2, figsize=(12, 6))
axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(corner_img_rgb)
axes[1].set_title("Harris Corners Detected")
axes[1].axis("off")

plt.tight_layout()
plt.show()
