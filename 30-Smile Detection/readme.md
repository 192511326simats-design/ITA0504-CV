!pip install -q face-recognition

import face_recognition
from PIL import Image, ImageDraw
import matplotlib.pyplot as plt

def detect_smile_landmarks(image_path):
    try:
        # Load the image
        image = face_recognition.load_image_file(image_path)
    except Exception as e:
        print(f"Error reading image: {e}")
        return

    # Find facial landmarks
    face_landmarks_list = face_recognition.face_landmarks(image)

    # Convert to PIL Image for drawing
    pil_image = Image.fromarray(image)
    draw = ImageDraw.Draw(pil_image)

    if len(face_landmarks_list) > 0:
        print(f"Detected {len(face_landmarks_list)} face(s) with landmarks.")
        for face_landmarks in face_landmarks_list:
            # A smile/mouth is composed of the top lip and bottom lip
            for mouth_part in ['top_lip', 'bottom_lip']:
                if mouth_part in face_landmarks:
                    mouth_pts = face_landmarks[mouth_part]
                    # Draw mouth outlines
                    draw.polygon(mouth_pts, outline=(0, 255, 0), width=3)
    else:
        print("No faces or smile/mouth landmarks detected in the image.")

    # Display the result safely in Colab
    plt.figure(figsize=(10, 10))
    plt.imshow(pil_image)
    plt.axis('off')
    plt.show()

# Run the smile/mouth detection on your selected file
detect_smile_landmarks("/content/3qZ09UE7lN6AtorfXFRYpEtSY93.webp")
