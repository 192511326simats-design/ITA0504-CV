import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the selected image
image = cv2.imread('/content/images.jpg')
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Convert to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Perform Harris Corner Detection
gray_float = np.float32(gray)
dst = cv2.cornerHarris(gray_float, 2, 3, 0.04)

# Dilate the results to mark the corners clearly
dst = cv2.dilate(dst, None)

# Threshold for an optimal value, marking corners in red on the original RGB image
threshold = 0.01 * dst.max()
image_rgb[dst > threshold] = [255, 0, 0]

# Display the detected features inline using matplotlib
plt.figure(figsize=(8, 8))
plt.imshow(image_rgb)
plt.title('Feature Detection (Harris Corners marked in Red)')
plt.axis('off')
plt.show()
