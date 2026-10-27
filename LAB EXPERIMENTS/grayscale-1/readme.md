import cv2
import matplotlib.pyplot as plt

# Load the selected image
image_path = "/content/images.jpg"
image = cv2.imread(image_path)

if image is not None:
    # Convert BGR (OpenCV default) to RGB for correct plotting
    image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    
    # Convert to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    # Plot the images side-by-side
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    
    axes[0].imshow(image_rgb)
    axes[0].set_title("Original Image")
    axes[0].axis("off")
    
    axes[1].imshow(gray_image, cmap="gray")
    axes[1].set_title("Grayscale Image")
    axes[1].axis("off")
    
    plt.tight_layout()
    plt.show()
else:
    print(f"Could not load image from {image_path}. Please check the file path.")
