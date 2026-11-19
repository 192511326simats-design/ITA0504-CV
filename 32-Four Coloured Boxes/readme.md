import numpy as np
import matplotlib.pyplot as plt

def create_colored_corners(image_size):
    height, width = image_size  # Extract height and width
    
    # Create a white image (3D array of ones scaled to 255 for RGB)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    
    # Calculate the size of the colored boxes (1/10th of image size)
    box_h, box_w = height // 10, width // 10
    
    # Define corner regions and their colors (RGB representation)
    image[:box_h, :box_w] = [0, 0, 0]         # Top-left (Black)
    image[:box_h, -box_w:] = [0, 0, 255]       # Top-right (Red in RGB)
    image[-box_h:, :box_w] = [0, 255, 0]       # Bottom-left (Green)
    image[-box_h:, -box_w:] = [255, 0, 0]      # Bottom-right (Blue in RGB)
    
    # Display the image using Matplotlib
    plt.figure(figsize=(6, 6))
    plt.imshow(image)
    plt.title("Colored Corners Image")
    plt.axis('off')
    plt.show()

# Configure dimensions directly to avoid blocking prompts in Colab
user_width = 500
user_height = 500
create_colored_corners((user_height, user_width))
