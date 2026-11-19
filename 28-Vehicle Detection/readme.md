!pip install -q face-recognition

import face_recognition
from PIL import Image, ImageDraw
import matplotlib.pyplot as plt

def detect_faces(image_path):
    try:
        # Load the image using face_recognition
        image = face_recognition.load_image_file(image_path)
    except Exception as e:
        print(f"Error reading image: {e}")
        return

    # Detect face locations
    face_locations = face_recognition.face_locations(image)

    # Load as PIL Image for rendering bounding boxes
    pil_image = Image.fromarray(image)
    draw = ImageDraw.Draw(pil_image)

    if len(face_locations) > 0:
        print(f"Detected {len(face_locations)} face(s).")
        for top, right, bottom, left in face_locations:
            draw.rectangle(((left, top), (right, bottom)), outline=(0, 255, 0), width=4)
    else:
        print("No faces detected in the image.")

    # Display the result using Matplotlib
    plt.figure(figsize=(10, 10))
    plt.imshow(pil_image)
    plt.axis('off')
    plt.show()

# Run the face detection on your selected file
detect_faces("/content/images (1).jpg")
