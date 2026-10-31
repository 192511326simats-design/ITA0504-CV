import cv2
import matplotlib.pyplot as plt

# Load the selected image from the environment
image_path = "/content/images.jpg"
image = cv2.imread(image_path)

# OpenCV loads images in BGR; convert to RGB for correct matplotlib colors
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Display both images side by side using matplotlib
fig, axes = plt.subplots(1, 2, figsize=(12, 6))

axes[0].imshow(image_rgb)
axes[0].set_title("Original Image")
axes[0].axis("off")

axes[1].imshow(gray_image, cmap="gray")
axes[1].set_title("Grayscale Image")
axes[1].axis("off")

plt.tight_layout()
plt.show()
