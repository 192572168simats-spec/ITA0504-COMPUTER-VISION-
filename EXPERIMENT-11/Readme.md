import cv2
import matplotlib.pyplot as plt

# Load the image from the correct path
image_path = "/content/images.jpg"
image_bgr = cv2.imread(image_path)

# Convert BGR (OpenCV default) to RGB for correct displaying with matplotlib
image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)

# Flip the image horizontally (around y-axis)
flipped_image = cv2.flip(image_rgb, 1)

# Rotate the flipped image 180 degrees
rotated_image = cv2.rotate(flipped_image, cv2.ROTATE_180)

# Save the final transformed image (converting back to BGR for saving)
cv2.imwrite("rotated_image.jpg", cv2.cvtColor(rotated_image, cv2.COLOR_RGB2BGR))

# Display the results inline using matplotlib
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(rotated_image)
axes[1].set_title("Rotated 180-degree Clockwise Along Y-axis")
axes[1].axis("off")

plt.tight_layout()
plt.show()
