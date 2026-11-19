import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the selected image
image_path = '/content/360_F_909111022_5zQGE6DHPqglss1so5IpJQqoQ0Pr38mC.jpg'
image = cv2.imread(image_path)

# Convert to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply morphological CLOSE operation
kernel = np.ones((5,5), np.uint8)
closed_image = cv2.morphologyEx(gray_image, cv2.MORPH_CLOSE, kernel)

# Display the results side-by-side using matplotlib
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

# Original image (convert BGR to RGB for correct colors in matplotlib)
axes[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
axes[0].set_title('Original Image')
axes[0].axis('off')
