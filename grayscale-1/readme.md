import cv2
from google.colab.patches import cv2_imshow
image = cv2.imread("/content/images.jpg")
if image is not None:
    print("Original Image:")
    cv2_imshow(image)
    print("Grayscale Image:")
    cv2_imshow(gray_image)
else:
    print("Error: Could not load image. Please verify the file path.")
