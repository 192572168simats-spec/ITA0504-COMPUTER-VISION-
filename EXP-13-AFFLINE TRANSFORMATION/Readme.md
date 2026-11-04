mport cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the image using the correct path
image = cv2.imread("/content/images.jpg")
rows, cols, ch = image.shape

# Define points for affine transformation
pts1 = np.float32([[50, 50], [200, 50], [50, 200]])
pts2 = np.float32([[10, 100], [200, 50], [100, 250]])

# Calculate transformation matrix and apply warp
matrix = cv2.getAffineTransform(pts1, pts2)
transformed_image = cv2.warpAffine(image, matrix, (cols, rows))

# Save the result
cv2.imwrite("affine_transformed.jpg", transformed_image)

# Convert BGR to RGB for correct matplotlib plotting
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
transformed_image_rgb = cv2.cvtColor(transformed_image, cv2.COLOR_BGR2RGB)

# Display the results side-by-side
fig, axes = plt.subplots(1, 2, figsize=(10, 5))
axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(transformed_image_rgb)
axes[1].set_title("Affine Transformed Image")
axes[1].axis("off")

plt.tight_layout()
plt.show()
