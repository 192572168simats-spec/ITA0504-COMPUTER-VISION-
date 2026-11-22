import cv2
from PIL import Image
from IPython.display import display
import os

input_path = "/mnt/data/images.jpg"
image = cv2.imread(input_path, cv2.IMREAD_GRAYSCALE)

if image is None:
    raise FileNotFoundError(f"Could not read image: {input_path}")

threshold_value = 127
_, segmented_image = cv2.threshold(image, threshold_value, 255, cv2.THRESH_BINARY)

output_path = "/mnt/data/segmented_image.png"
cv2.imwrite(output_path, segmented_image)

print("Threshold segmentation completed.")
print(f"Threshold value: {threshold_value}")
display(Image.open(output_path))
