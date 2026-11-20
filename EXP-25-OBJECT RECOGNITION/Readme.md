import cv2
import matplotlib.pyplot as plt

# 1. Read a fresh copy of the image to avoid cumulative boxes
image = cv2.imread('/content/images.jpg')
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Get image dimensions
img_h, img_w = gray.shape[:2]

# 2. Perform thresholding to segment distinct objects/regions
_, thresh = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY_INV + cv2.THRESH_OTSU)

# 3. Find contours of the segmented objects
contours, _ = cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

# ==========================================================
# SENSITIVITY TUNING:
# - Set min_area smaller (e.g., 20 or 50) to detect small leaf details/features.
# - Set min_area larger (e.g., 5000 or 10000) to isolate only the main tree.
# ==========================================================
min_area = 100

# Filter and draw bounding boxes around significant objects found
for contour in contours:
    area = cv2.contourArea(contour)
    if area > min_area:
        x, y, w, h = cv2.boundingRect(contour)
        
        # Skip the contour if it represents the outermost border of the entire image
        if w > img_w * 0.98 and h > img_h * 0.98:
            continue
