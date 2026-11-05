import cv2
import numpy as np
from google.colab.patches import cv2_imshow

# Read the input image from the correct path
image = cv2.imread("/content/images.jpg")

# Create a copy to keep the original clean for display
original_image = image.copy()

# Convert the image to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Convert to float32 for Harris Corner Detection
gray = np.float32(gray)

# Apply Harris Corner Detection
harris_corners = cv2.cornerHarris(gray, blockSize=2, ksize=3, k=0.04)

# Dilate corner points for better visibility
harris_corners = cv2.dilate(harris_corners, None)

# Mark detected corners in red on the image copy
image[harris_corners > 0.01 * harris_corners.max()] = [0, 0, 255]

# Display images using Colab's cv2_imshow patch
print("Original Image:")
cv2_imshow(original_image)

print("Harris Corner Detection:")
cv2_imshow(image)

# Save the result
cv2.imwrite("harris_corners.jpg", image)
