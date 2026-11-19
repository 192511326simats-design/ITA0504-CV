import cv2
import numpy as np
import matplotlib.pyplot as plt

def subtract_foreground(image_path, lower_color, upper_color):
    # Read the image
    image = cv2.imread(image_path)
    if image is None:
        print(f"Error: Could not load image from {image_path}")
        return
    
    # Convert to HSV color space
    hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
    
    # Define lower and upper range for foreground color (adjust as needed)
    lower_bound = np.array(lower_color, dtype=np.uint8)
    upper_bound = np.array(upper_color, dtype=np.uint8)
    
    # Create mask to remove foreground
    mask = cv2.inRange(hsv, lower_bound, upper_bound)
    
    # Extract the background
    background = cv2.bitwise_and(image, image, mask=mask)
    
    # Convert BGR to RGB for Matplotlib visualization
    image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
    background_rgb = cv2.cvtColor(background, cv2.COLOR_BGR2RGB)
    
    # Display results side-by-side
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    axes[0].imshow(image_rgb)
    axes[0].set_title("Original Image")
    axes[0].axis("off")
    
    axes[1].imshow(background_rgb)
    axes[1].set_title("Foreground Subtracted Image (Only Background)")
    axes[1].axis("off")
    
    plt.tight_layout()
    plt.show()

# Configure parameters using selected file
image_path = "/content/images.jpg"
lower_color = [0, 50, 50]  # Example lower bound for foreground color
upper_color = [120, 255, 255]  # Example upper bound for foreground color
subtract_foreground(image_path, lower_color, upper_color)
