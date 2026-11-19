import numpy as np
import cv2
import matplotlib.pyplot as plt

def create_circle_image(image_size):
    height, width = image_size  # Extract height and width
    
    # Create a white image (3D array of ones scaled to 255 for RGB)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    
    # Define the circle properties
    center = (width // 2, height // 2)  # Center of the image
    radius = min(width, height) // 4     # Radius is 1/4th of the smallest dimension
    
    # Draw the circle (color: Red in RGB representation: (255, 0, 0), thickness: 2)
    cv2.circle(image, center, radius, (255, 0, 0), 2)
    
    # Display the image inline using Matplotlib
    plt.figure(figsize=(6, 6))
    plt.imshow(image)
    plt.title("Circle Image")
    plt.axis('off')
    plt.show()

# Configure dimensions directly to prevent blocking execution prompts
user_width = 500
user_height = 500
create_circle_image((user_height, user_width))
