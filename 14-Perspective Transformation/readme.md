import cv2
import numpy as np
from google.colab.patches import cv2_imshow

# Read the selected image
image = cv2.imread("/content/images.jpg")

rows, cols, ch = image.shape
pts1 = np.float32([[50, 50], [400, 50], [50, 400], [400, 400]])
pts2 = np.float32([[10, 100], [300, 50], [100, 300], [350, 350]])
matrix = cv2.getPerspectiveTransform(pts1, pts2)
transformed_image = cv2.warpPerspective(image, matrix, (cols, rows))

print("Original Image:")
cv2_imshow(image)

print("Perspective Transformed Image:")
cv2_imshow(transformed_image)

cv2.imwrite("perspective_transformed.jpg", transformed_image)
