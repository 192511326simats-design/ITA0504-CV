import cv2
from google.colab.patches import cv2_imshow

# Read the correct selected image file
image = cv2.imread("/content/images.jpg")

# Perform transformations
flipped_image = cv2.flip(image, 1)
rotated_image = cv2.rotate(flipped_image, cv2.ROTATE_180)

# Display images in Colab
print("Original Image:")
cv2_imshow(image)

print("Rotated 180-degree Clockwise Along Y-axis:")
cv2_imshow(rotated_image)

# Save the result
cv2.imwrite("rotated_image.jpg", rotated_image)
