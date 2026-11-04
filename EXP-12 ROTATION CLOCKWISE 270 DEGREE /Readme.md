import cv2
import matplotlib.pyplot as plt

# Load the image using the correct path
image = cv2.imread("/content/images.jpg")

# Flip and rotate
flipped_image = cv2.flip(image, 1)
rotated_image = cv2.rotate(flipped_image, cv2.ROTATE_90_COUNTERCLOCKWISE)

# Save the result
cv2.imwrite("rotated_image_270.jpg", rotated_image)

# Convert BGR to RGB for correct matplotlib plotting
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
rotated_image_rgb = cv2.cvtColor(rotated_image, cv2.COLOR_BGR2RGB)

# Display the results
fig, axes = plt.subplots(1, 2, figsize=(10, 5))
axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(rotated_image_rgb)
axes[1].set_title("Rotated 270-degree Clockwise Along Y-axis")
axes[1].axis("off")

plt.tight_layout()
plt.show()
