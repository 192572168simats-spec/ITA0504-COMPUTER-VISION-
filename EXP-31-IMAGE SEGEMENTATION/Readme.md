
import cv2

def segment_image(image_path, threshold_value=127):
    # Read the input image in grayscale
    image = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)

    if image is None:
        print("Error: Image not found!")
        return

    # Apply thresholding for image segmentation
    _, segmented_image = cv2.threshold(
        image, threshold_value, 255, cv2.THRESH_BINARY
    )

    # Display original and segmented images
    cv2.imshow("Original Grayscale Image", image)
    cv2.imshow("Segmented Image", segmented_image)

    cv2.waitKey(0)
    cv2.destroyAllWindows()

# Example usage with your uploaded image
segment_image(r"/mnt/data/images(1).jpg", 127)
