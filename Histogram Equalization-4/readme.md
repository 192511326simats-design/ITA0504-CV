import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the selected image
image = cv2.imread('/content/images.jpg')

if image is None:
    print("Error: Could not load the image. Please make sure the file exists at /content/images.jpg")
else:
    # Convert to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # Apply Histogram Equalization
    equalized_image = cv2.equalizeHist(gray_image)
    
    # Display the results side-by-side using matplotlib
    plt.figure(figsize=(12, 6))
    
    plt.subplot(1, 2, 1)
    plt.imshow(gray_image, cmap='gray')
    plt.title('Original Grayscale Image')
    plt.axis('off')
    
    plt.subplot(1, 2, 2)
    plt.imshow(equalized_image, cmap='gray')
    plt.title('Histogram Equalized Image')
    plt.axis('off')
    
    plt.tight_layout()
    plt.show()
