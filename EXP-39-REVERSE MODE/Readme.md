
import cv2

def play_video_reverse_slow(video_path):
    # Open the video
    cap = cv2.VideoCapture(video_path)

    if not cap.isOpened():
        print("Error: Cannot open video!")
        return

    frames = []

    # Read and store all video frames
    while cap.isOpened():
        ret, frame = cap.read()

        if not ret:
            break

        frames.append(frame)

    cap.release()

    # Play frames in reverse order
    for frame in reversed(frames):
        cv2.imshow("Reverse Slow Motion Video", frame)

        # Press 'q' to quit
        if cv2.waitKey(100) & 0xFF == ord('q'):
            break

    cv2.destroyAllWindows()

# Example usage
play_video_reverse_slow("video.mp4")
