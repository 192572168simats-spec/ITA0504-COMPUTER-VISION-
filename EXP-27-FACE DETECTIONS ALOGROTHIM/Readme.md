import cv2
from pathlib import Path

input_path = "/mnt/data/WIN_20261120_13_22_55_Pro.jpg"
output_path = "/mnt/data/face_detection_output.jpg"

image = cv2.imread(input_path)
if image is None:
    raise FileNotFoundError("Could not load the uploaded image.")

gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
cascade_path = cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
face_cascade = cv2.CascadeClassifier(cascade_path)

faces = face_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5,
    minSize=(30, 30)
)

for (x, y, w, h) in faces:
    cv2.rectangle(image, (x, y), (x + w, y + h), (0, 255, 0), 3)

cv2.imwrite(output_path, image)
print(f"Detected faces: {len(faces)}")
print(f"Output saved to: {output_path}")
