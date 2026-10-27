import cv2
from google.colab.patches import cv2_imshow
image = cv2.imread('/content/images.jpg')

if image is not None:
    # Convert the image to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    
    # Detect edges using Canny
    edges = cv2.Canny(gray_image, 100, 200)
    
    # Display the images using Google Colab's patch
    print("Original Image:")
    cv2_imshow(image)
    
    print("Edge Detected Image:")
    cv2_imshow(edges)
else:
    print("Error: Could not load '/content/images.jpg'. Please make sure the file exists.")
