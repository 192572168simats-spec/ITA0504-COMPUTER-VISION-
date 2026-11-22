
import cv2
import pytesseract

def extract_text_from_video(video_path):
    # Open the video
    cap = cv2.VideoCapture(video_path)

    if not cap.isOpened():
        print("Error: Cannot open video!")
        return

    while cap.isOpened():
        # Read each frame
        ret, frame = cap.read()

        if not ret:
            break

        # Convert frame to grayscale
        gray_frame = cv2.cvtColor(
            frame, cv2.COLOR_BGR2GRAY
        )

        # Extract text using Tesseract OCR
        text = pytesseract.image_to_string(gray_frame)

        if text.strip():
            print("Extracted Text:")
            print(text)

        # Display the video frame
        cv2.imshow("Video Text Extraction", frame)

        if cv2.waitKey(1) & 0xFF == ord('q'):
            break

    cap.release()
    cv2.destroyAllWindows()

# Example usage
extract_text_from_video("video.mp4")
