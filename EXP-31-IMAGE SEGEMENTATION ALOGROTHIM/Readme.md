import cv2
from google.colab.patches import cv2_imshow

def segment_image(image_path, threshold_value=127):
    # Read the input image
    image = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE) # Convert to grayscale
    if image is None:
        print(f"Error: Could not read image at {image_path}")
        return
    # Apply thresholding for segmentation
    _, segmented_image = cv2.threshold(image, threshold_value, 255, cv2.THRESH_BINARY)
    # Display the results in Colab
    print("Original Image:")
    cv2_imshow(image)
    print("Segmented Image:")
    cv2_imshow(segmented_image)

# Example usage with selected file
segment_image("/content/images.jpg", 127)
