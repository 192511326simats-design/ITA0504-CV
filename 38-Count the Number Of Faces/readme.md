!pip install face-recognition

import face_recognition
from PIL import Image, ImageDraw
import matplotlib.pyplot as plt

def count_faces(image_path):
    # Load the image using face_recognition (which uses PIL/numpy internally)
    try:
        image = face_recognition.load_image_file(image_path)
    except Exception as e:
        print(f"Error loading image: {e}")
        return 0
    
    # Find all the faces in the image
    face_locations = face_recognition.face_locations(image)
    face_count = len(face_locations)
    print(f"Number of faces detected: {face_count}")
    
    # Convert to PIL Image to draw bounding boxes
    pil_image = Image.fromarray(image)
    draw = ImageDraw.Draw(pil_image)
    
    # Draw a green box around each face detected
    for top, right, bottom, left in face_locations:
        # Draw a rectangle with a thickness of 3 pixels
        draw.rectangle(((left, top), (right, bottom)), outline="green", width=3)
    
    # Display the result using matplotlib
    plt.figure(figsize=(10, 10))
    plt.imshow(pil_image)
    plt.axis('off')
    plt.title('Face Detection Result (Bypassing cv2)')
    plt.show()
    
    return face_count

# Run the face detection on your image
image_path = "/content/images (2).jpg"
count_faces(image_path)
