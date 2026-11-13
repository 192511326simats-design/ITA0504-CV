import cv2
import numpy as np
from google.colab.patches import cv2_imshow

# Read the input image from the correct path
image = cv2.imread("/content/images.jpg")

if image is None:
    print("Error: Could not load the image. Please verify that '/content/images.jpg' exists.")
else:
    # Convert the image to grayscale
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    # Apply Sobel filter in X and Y directions
    sobel_x = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3) # Gradient in X direction
    sobel_y = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3) # Gradient in Y direction

    # Convert gradients to absolute scale
    sobel_x = cv2.convertScaleAbs(sobel_x)
    sobel_y = cv2.convertScaleAbs(sobel_y)

    # Combine the gradients
    sobel_combined = cv2.addWeighted(sobel_x, 0.5, sobel_y, 0.5, 0)

    # Display images in Colab
    print("Original Image:")
    cv2_imshow(image)
    print("Sobel X:")
    cv2_imshow(sobel_x)
    print("Sobel Y:")
    cv2_imshow(sobel_y)
    print("Sobel Combined:")
    cv2_imshow(sobel_combined)

    # Save the results
    cv2.imwrite("sobel_x.jpg", sobel_x)
    cv2.imwrite("sobel_y.jpg", sobel_y)
    cv2.imwrite("sobel_combined.jpg", sobel_combined)
