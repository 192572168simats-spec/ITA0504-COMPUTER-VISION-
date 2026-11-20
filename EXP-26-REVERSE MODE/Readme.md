import cv2
import matplotlib.pyplot as plt

# Load the original image
img = cv2.imread('/content/images.jpg')

if img is not None:
    # Define the target resolution (width, height)
    target_width = 300
    target_height = 300
    target_dim = (target_width, target_height)
    
    # Resize the image using bilinear interpolation (standard for resizing)
    resized_img = cv2.resize(img, target_dim, interpolation=cv2.INTER_LINEAR)
    
    # Convert color spaces from BGR to RGB for correct display in matplotlib
    img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    resized_rgb = cv2.cvtColor(resized_img, cv2.COLOR_BGR2RGB)
    
    # Display both images side-by-side
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    
    # Original Image
    axes[0].imshow(img_rgb)
    axes[0].set_title(f"Original Image\nResolution: {img.shape[1]}x{img.shape[0]}")
    axes[0].axis('off')
    
    # Resized Image
    axes[1].imshow(resized_rgb)
    axes[1].set_title(f"Resized Image\nResolution: {target_width}x{target_height}")
    axes[1].axis('off')
    
    plt.tight_layout()
    plt.show()
else:
    print("Could not load the image. Please verify the file path.")
