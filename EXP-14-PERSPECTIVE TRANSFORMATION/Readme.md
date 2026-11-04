import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the image using the correct path
image = cv2.imread("/content/images.jpg")
rows, cols, ch = image.shape

# Define source and destination points for perspective transform
pts1 = np.float32([[50, 50], [400, 50], [50, 400], [400, 400]])
pts2 = np.float32([[10, 100], [300, 50], [100, 300], [350, 350]])

# Calculate transformation matrix and apply perspective warp
matrix = cv2.getPerspectiveTransform(pts1, pts2)
transformed_image = cv2.warpPerspective(image, matrix, (cols, rows))

# Save the result
cv2.imwrite("perspective_transformed.jpg", transformed_image)

# Convert BGR to RGB for correct matplotlib plotting
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
transformed_image_rgb = cv2.cvtColor(transformed_image, cv2.COLOR_BGR2RGB)

# Display the results side-by-side
fig, axes = plt.subplots(1, 2, figsize=(10, 5))
axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(transformed_image_rgb)
axes[1].set_title("Perspective Transformed Image")
axes[1].axis("off")

plt.tight_layout()
plt.show()
