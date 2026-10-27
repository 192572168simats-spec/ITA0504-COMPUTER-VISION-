import cv2
import matplotlib.pyplot as plt

# Load the selected image
image_path = "/content/images.jpg"
image = cv2.imread(image_path)

if image is not None:
    # Convert BGR (OpenCV default) to RGB for correct matplotlib plotting
    image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    
    # Apply Gaussian blur
    blurred_image = cv2.GaussianBlur(image_rgb, (15, 15), 0)
    
    # Plot the original and blurred images side-by-side
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    
    axes[0].imshow(image_rgb)
    axes[0].set_title("Original Image")
    axes[0].axis("off")
    
    axes[1].imshow(blurred_image)
    axes[1].set_title("Blurred Image")
    axes[1].axis("off")
    
    plt.tight_layout()
    plt.show()
else:
    print(f"Could not load image from {image_path}. Please check the file path.")
