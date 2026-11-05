import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input image
image = cv2.imread("/content/images.jpg")

# Convert the image to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply Sobel filter in X and Y directions
sobel_x = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3) # Gradient in X direction
sobel_y = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3) # Gradient in Y direction

# Convert gradients to absolute scale
sobel_x_abs = cv2.convertScaleAbs(sobel_x)
sobel_y_abs = cv2.convertScaleAbs(sobel_y)

# Combine the two gradients to get the overall edge magnitude
sobel_combined = cv2.addWeighted(sobel_x_abs, 0.5, sobel_y_abs, 0.5, 0)

# Convert BGR to RGB for correct plotting
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Display the results
fig, axes = plt.subplots(1, 4, figsize=(20, 5))
axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(sobel_x_abs, cmap="gray")
axes[1].set_title("Sobel X (Vertical Edges)")
axes[1].axis("off")

axes[2].imshow(sobel_y_abs, cmap="gray")
axes[2].set_title("Sobel Y (Horizontal Edges)")
axes[2].axis("off")

axes[3].imshow(sobel_combined, cmap="gray")
axes[3].set_title("Sobel Combined")
axes[3].axis("off")

plt.tight_layout()
plt.show()
