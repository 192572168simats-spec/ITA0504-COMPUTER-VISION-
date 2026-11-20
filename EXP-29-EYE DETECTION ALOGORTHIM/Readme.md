import cv2

def detect_eyes(image_path):
    # Load face and eye classifiers
    face_cascade = cv2.CascadeClassifier(
        cv2.data.haarcascades +
        'haarcascade_frontalface_default.xml'
    )
    eye_cascade = cv2.CascadeClassifier(
        cv2.data.haarcascades + 'haarcascade_eye.xml'
    )

    # Read the image
    image = cv2.imread(image_path)

    if image is None:
        print("Error: Image not found!")
        return

    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    # Detect faces
    faces = face_cascade.detectMultiScale(
        gray, scaleFactor=1.1,
        minNeighbors=5, minSize=(30, 30)
    )

    for (x, y, w, h) in faces:
        face_roi = gray[y:y+h, x:x+w]

        # Detect eyes inside each face
        eyes = eye_cascade.detectMultiScale(
            face_roi, scaleFactor=1.1,
            minNeighbors=10, minSize=(15, 15)
        )

        # Draw blue boxes around detected eyes
        for (ex, ey, ew, eh) in eyes:
            cv2.rectangle(
                image,
                (x + ex, y + ey),
                (x + ex + ew, y + ey + eh),
                (255, 0, 0), 2
            )

    # Display the result
    cv2.imshow("Eye Detection", image)
    cv2.waitKey(0)
    cv2.destroyAllWindows()


# Example usage
detect_eyes("face_image.jpg")
