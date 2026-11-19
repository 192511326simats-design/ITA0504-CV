import cv2
import numpy as np
import matplotlib.pyplot as plt

def subtract_background(image_path, lower_color, upper_color):
    # Read the image
    image = cv2.imread(image_path)
    if image is None:
        print(f"Error: Could not load image from {image_path}")
        return
    
    # Convert to HSV color space
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    
    # Define lower and upper range for background color
    lower_bound = np.array(lower_color, dtype=np.uint8)
    upper_bound = np.array(upper_color, dtype=np.uint8)
    
    # Create mask for background removal
    mask = cv2.inRange(hsv, lower_bound, upper_bound)
    
    # Invert mask to keep the foreground
    mask_inv = cv2.bitwise_not(mask)
    
    # Extract the foreground
    foreground = cv2.bitwise_and(image, image, mask=mask_inv)
    
    # Convert BGR to RGB for Matplotlib visualization
    image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    foreground_rgb = cv2.cvtColor(foreground, cv2.COLOR_BGR2RGB)
    
    # Display results side-by-side
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    axes[0].imshow(image_rgb)
    axes[0].set_title("Original Image")
    axes[0].axis('off')
    
    axes[1].imshow(foreground_rgb)
    axes[1].set_title("Background Subtracted Image")
    axes[1].axis('off')
    
    plt.tight_layout()
    plt.show()

# Configure parameters using selected file
image_path = "/content/images.jpg"
lower_color = [30, 30, 30] 
upper_color = [255, 255, 255]

subtract_background(image_path, lower_color, upper_color)
