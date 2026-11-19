import numpy as np
import cv2
import matplotlib.pyplot as plt

def create_rectangle_image(image_size):
    height, width = image_size  # Extract height and width
    
    # Create a white image (3D array of ones scaled to 255 for RGB)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    
    # Define rectangle coordinates (centered in the image)
    top_left = (width // 4, height // 4)
    bottom_right = (3 * width // 4, 3 * height // 4)
    
    # Draw the rectangle (color: Blue in RGB representation: (0, 0, 255), thickness: 2)
    cv2.rectangle(image, top_left, bottom_right, (0, 0, 255), 2)
    
    # Display the image using Matplotlib
    plt.figure(figsize=(6, 6))
    plt.imshow(image)
    plt.title("Rectangle Image")
    plt.axis('off')
    plt.show()

# Configure dimensions directly to prevent blocking execution prompts
user_width = 500
user_height = 500
create_rectangle_image((user_height, user_width))
