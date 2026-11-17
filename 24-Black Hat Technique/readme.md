import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the image as grayscale from the correct path
image = cv2.imread('/content/images.jpg', cv2.IMREAD_GRAYSCALE)

# Define a kernel (5x5 structuring element)
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))

# Apply the Black Hat transformation
blackhat = cv2.morphologyEx(image, cv2.MORPH_BLACKHAT, kernel)

# Save the result
cv2.imwrite('black_hat_image.jpg', blackhat)

# Display the results inline using matplotlib
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

axes[0].imshow(image, cmap='gray')
axes[0].set_title('Original Gray Image')
axes[0].axis('off')

axes[1].imshow(blackhat, cmap='gray')
axes[1].set_title('Black Hat Image')
axes[1].axis('off')

plt.tight_layout()
plt.show()
