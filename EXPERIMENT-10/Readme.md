import cv2
import matplotlib.pyplot as plt

# Load the image
image_path = "/content/images.jpg"
img = cv2.imread(image_path)

# Convert BGR (OpenCV default) to RGB (Matplotlib default)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Rotate 90 degrees clockwise
rotated_img = cv2.rotate(img_rgb, cv2.ROTATE_90_CLOCKWISE)

# Display the rotated image using matplotlib
plt.figure(figsize=(6, 6))
plt.imshow(rotated_img)
plt.title("Rotated Image (90° Clockwise)")
plt.axis("off")
plt.show()
