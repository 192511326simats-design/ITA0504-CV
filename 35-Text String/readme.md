import numpy as np
import cv2
import matplotlib.pyplot as plt

def add_text_to_image(image_size, text):
    height, width = image_size  # Extract height and width
    
    # Create a white image (3D array of ones scaled to 255 for RGB)
    image = np.ones((height, width, 3), dtype=np.uint8) * 255
    
    # Define text properties
    font = cv2.FONT_HERSHEY_SIMPLEX
    font_scale = 1
    font_thickness = 2
    text_color = (255, 0, 0)  # Red color in RGB representation for Matplotlib
    text_size = cv2.getTextSize(text, font, font_scale, font_thickness)[0]
    
    # Calculate text position (centered)
    text_x = (width - text_size[0]) // 2
    text_y = (height + text_size[1]) // 2
    
    # Draw text on the image
    cv2.putText(image, text, (text_x, text_y), font, font_scale, text_color, font_thickness)
    
    # Display the image inline using Matplotlib
    plt.figure(figsize=(6, 6))
    plt.imshow(image)
    plt.title("Image with Text")
    plt.axis('off')
    plt.show()

# Configure dimensions directly to avoid blocking execution
user_width = 500
user_height = 500
user_text = "Hello, Colab!"
add_text_to_image((user_height, user_width), user_text)
