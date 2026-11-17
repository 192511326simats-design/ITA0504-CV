import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input image from the correct path
image = cv2.imread('/content/images.jpg')

# Convert BGR to RGB for correct displaying in matplotlib
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Define the structuring element (kernel)
kernel = np.ones((5,5), np.uint8)

# Apply morphological closing
closed_image = cv2.morphologyEx(gray_image, cv2.MORPH_CLOSE, kernel)

# Save the result
cv2.imwrite('closed_image.jpg', closed_image)

# Display the results side-by-side using matplotlib
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

axes[0].imshow(image_rgb)
axes[0].set_title('Original Image')
axes[0].axis('off')

axes[1].imshow(closed_image, cmap='gray')
axes[1].set_title('Closed Image')
axes[1].axis('off')

plt.tight_layout()
plt.show()
