import cv2
import matplotlib.pyplot as plt

# Read the image
image_path = "/content/images.jpg"
image = cv2.imread(image_path)

# Convert BGR (OpenCV default) to RGB (Matplotlib default)
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Resize to a bigger size (2x scaling)
bigger_image = cv2.resize(image_rgb, None, fx=2, fy=2, interpolation=cv2.INTER_LINEAR)

# Resize to a smaller size (0.5x scaling)
smaller_image = cv2.resize(image_rgb, None, fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA)

# Display images using matplotlib
fig, axes = plt.subplots(1, 3, figsize=(15, 5))

axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(bigger_image)
axes[1].set_title("Bigger Image (2x)")
axes[1].axis("off")

axes[2].imshow(smaller_image)
axes[2].set_title("Smaller Image (0.5x)")
axes[2].axis("off")

plt.tight_layout()
plt.show()
