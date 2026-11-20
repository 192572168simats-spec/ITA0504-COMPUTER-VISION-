import cv2
from pathlib import Path

input_path = "/mnt/data/WIN_20261103_12_18_18_Pro.mp4"
output_path = "/mnt/data/output_reversed.mp4"

cap = cv2.VideoCapture(input_path)
if not cap.isOpened():
    raise RuntimeError("Could not open the uploaded video.")

width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fps = cap.get(cv2.CAP_PROP_FPS)
if not fps or fps <= 0:
    fps = 30.0

frames = []
while True:
    ret, frame = cap.read()
    if not ret:
        break
    frames.append(frame)
cap.release()

if not frames:
    raise RuntimeError("No frames could be read from the uploaded video.")

frames.reverse()
fourcc = cv2.VideoWriter_fourcc(*"mp4v")
writer = cv2.VideoWriter(output_path, fourcc, fps, (width, height))
if not writer.isOpened():
    raise RuntimeError("Could not create the reversed video file.")

for frame in frames:
    writer.write(frame)
writer.release()

print(f"Reversed video saved as: {output_path}")
print(f"Frames: {len(frames)} | Resolution: {width}x{height} | FPS: {fps:.2f}")
