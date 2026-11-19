import cv2
import matplotlib.pyplot as plt

def segment_image(image_path, threshold_value=127):
    # Read the input image in grayscale
    image = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
    if image is None:
        print(f"Error: Unable to load image at {image_path}")
        return
        
    # Apply binary thresholding for segmentation
    _, segmented_image = cv2.threshold(image, threshold_value, 255, cv2.THRESH_BINARY)
    
    # Display the original and segmented results side-by-side using Matplotlib
    fig, axes = plt.subplots(1, 2, figsize=(12, 6))
    
    axes[0].imshow(image, cmap='gray')
    axes[0].set_title("Original Grayscale Image")
    axes[0].axis('off')
    
    axes[1].imshow(segmented_image, cmap='gray')
    axes[1].set_title(f"Segmented Image (Threshold={threshold_value})")
    axes[1].axis('off')
    
    plt.tight_layout()
    plt.show()

# Run the segmentation on your selected image
segment_image("/content/images.jpg", 127)
