import cv2
import time
import os


IMAGE_DIR = "captured_images"  # Folder to save images in
os.makedirs(IMAGE_DIR, exist_ok=True)  # Create folder if it doesn't exist


counter = 1
while True:
    filename = os.path.join(IMAGE_DIR, f"image_{counter:03d}.jpg")
    if not os.path.exists(filename):
        break
    counter += 1

print(f"Next image will be saved as: {filename}")

# --- CAPTURE ---
cap = cv2.VideoCapture(0, cv2.CAP_DSHOW)

if not cap.isOpened():
    raise IOError("Cannot open webcam")

# Set resolution
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 1280)
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 720)

# Adjust brightness/exposure
cap.set(cv2.CAP_PROP_BRIGHTNESS, 150)
cap.set(cv2.CAP_PROP_EXPOSURE, -5)
cap.set(cv2.CAP_PROP_CONTRAST, 100)

# Warm up camera
time.sleep(2)

# Discard first frame (often black)
ret, _ = cap.read()
time.sleep(0.1)

ret, frame = cap.read()

if ret:
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    
    # Enhance contrast with CLAHE
    clahe = cv2.createCLAHE(clipLimit=3.0, tileGridSize=(8,8))
    enhanced = clahe.apply(gray)
    
    # Save with counter
    cv2.imwrite(filename, enhanced)
    print(f" Image saved as '{filename}'")
    
    # Optional: Show preview
    cv2.imshow("Captured Image", enhanced)
    cv2.waitKey(2000)
    cv2.destroyAllWindows()

else:
    print(" Failed to capture frame")

cap.release()