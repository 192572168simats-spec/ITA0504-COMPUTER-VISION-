import cv2
import matplotlib.pyplot as plt

# Load the selected image
image_path = "/content/images.jpg"
image = cv2.imread(image_path)

if image is not None:
    # Convert BGR to RGB for plotting with matplotlib
    image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    
    # Convert to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # Apply Gaussian blur to reduce noise (kernel size of 5x5)
    blurred_gray = cv2.GaussianBlur(gray_image, (5, 5), 0)
    
    # Define threshold values to refine edge detection
    low_threshold = 50
    high_threshold = 150
    
    # Apply Canny Edge Detection on the blurred image
    edges = cv2.Canny(blurred_gray, low_threshold, high_threshold)
    
    # Plot original and edge-detected images side-by-side
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    
    axes[0].imshow(image_rgb)
    axes[0].set_title("Original Image")
    axes[0].axis("off")
    
    axes[1].imshow(edges, cmap="gray")
    axes[1].set_title(f"Edges (Blurred + Canny: {low_threshold}, {high_threshold})")
    axes[1].axis("off")
    
    plt.tight_layout()
    plt.show()
else:
    print(f"Could not load image from {image_path}. Please check the file path.")
