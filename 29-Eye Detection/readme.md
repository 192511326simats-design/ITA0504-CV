!pip install -q face-recognition

import face_recognition
from PIL import Image, ImageDraw
import matplotlib.pyplot as plt

def detect_eyes_and_face(image_path):
    try:
        # Load the image using face_recognition
        image = face_recognition.load_image_file(image_path)
    except Exception as e:
        print(f"Error reading image: {e}")
        return

    # Find all facial features (including eyes)
    face_landmarks_list = face_recognition.face_landmarks(image)

    # Convert to PIL Image for drawing
    pil_image = Image.fromarray(image)
    draw = ImageDraw.Draw(pil_image)

    if len(face_landmarks_list) > 0:
        print(f"Detected {len(face_landmarks_list)} face(s) with landmarks.")
        for face_landmarks in face_landmarks_list:
            # Draw left and right eyes using the keypoints detected
            for eye in ['left_eye', 'right_eye']:
                if eye in face_landmarks:
                    eye_pts = face_landmarks[eye]
                    # Draw a closed polygon around the eye outline
                    draw.polygon(eye_pts, outline=(255, 0, 0), width=3)
    else:
        print("No faces or eye landmarks detected in the image.")

    # Display the result using Matplotlib
    plt.figure(figsize=(10, 10))
    plt.imshow(pil_image)
    plt.axis('off')
    plt.show()

# Run the detection on your selected file
detect_eyes_and_face("/content/3qZ09UE7lN6AtorfXFRYpEtSY93.webp")
