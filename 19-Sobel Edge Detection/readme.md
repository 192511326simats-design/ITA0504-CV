import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input image from the correct path
image = cv2.imread("/content/images.jpg")

# Convert BGR to RGB for matplotlib display
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

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

# Save the results
cv2.imwrite("sobel_x.jpg", sobel_x)
cv2.imwrite("sobel_y.jpg", sobel_y)
cv2.imwrite("sobel_combined.jpg", sobel_combined)

# Display the results inline using matplotlib
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

axes[0, 0].imshow(image_rgb)
axes[0, 0].set_title("Original Image")
axes[0, 0].axis("off")

axes[0, 1].imshow(sobel_x, cmap="gray")
axes[0, 1].set_title("Sobel X")
axes[0, 1].axis("off")

axes[1, 0].imshow(sobel_y, cmap="gray")
axes[1, 0].set_title("Sobel Y")
axes[1, 0].axis("off")

axes[1, 1].imshow(sobel_combined, cmap="gray")
axes[1, 1].set_title("Sobel Combined")
axes[1, 1].axis("off")

plt.tight_layout()
plt.show()
