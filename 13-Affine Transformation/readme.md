import cv2
import numpy as np
from google.colab.patches import cv2_imshow

# Read the correct selected image
image = cv2.imread("/content/images.jpg")

rows, cols, ch = image.shape
pts1 = np.float32([[50, 50], [200, 50], [50, 200]])
pts2 = np.float32([[10, 100], [200, 50], [100, 250]])
matrix = cv2.getAffineTransform(pts1, pts2)
transformed_image = cv2.warpAffine(image, matrix, (cols, rows))

print("Original Image:")
cv2_imshow(image)

print("Affine Transformed Image:")
cv2_imshow(transformed_image)

cv2.imwrite("affine_transformed.jpg", transformed_image)
