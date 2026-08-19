This guide covers **Lesson 1.2: Video Input & Processing** from the OpenCV curriculum, focusing on using `cv2.VideoCapture` to read live webcam streams and existing video files.

---

### Key Concepts & Syntax

`cv2.VideoCapture` creates a video capture object used to sequentially fetch frames.

* **Webcam Feed:** Pass an integer index (`0` for the default internal camera, `1` for external).
* **Video File:** Pass the path string to the video file (e.g., `"video.mp4"`).

#### Essential Methods:

* `cap.isOpened()`: Returns `True` if video initialization was successful.
* `cap.read()`: Grabs, decodes, and returns the next frame. Returns `(ret, frame)` where `ret` is a boolean (`True` if frame read correctly) and `frame` is the image NumPy array.
* `cap.release()`: Releases hardware resources or file locks when finished.

---

### Code Examples

#### 1. Reading a Live Webcam Stream

```python
import cv2

# Initialize webcam (0 is typically the default camera)
cap = cv2.VideoCapture(0)

# Verify camera opened
if not cap.isOpened():
    print("Error: Could not access the webcam.")
    exit()

while True:
    # Capture frame-by-frame
    ret, frame = cap.read()

    # If frame reading failed, break loop
    if not ret:
        print("Error: Failed to grab frame.")
        break

    # Display real-time frame
    cv2.imshow("Webcam Stream", frame)

    # Press 'q' on the keyboard to exit loop
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Release the camera and close windows
cap.release()
cv2.destroyAllWindows()

```

#### 2. Reading a Video File

Reading a video file follows the exact same pattern, but you check when the video reaches its end (`ret` becomes `False`).

```python
import cv2

# Pass path to the video file
cap = cv2.VideoCapture("input_video.mp4")

if not cap.isOpened():
    print("Error: Could not open video file.")
    exit()

# Extract properties (e.g., Frame Rate)
fps = cap.get(cv2.CAP_PROP_FPS)
print(f"Video FPS: {fps}")

while cap.isOpened():
    ret, frame = cap.read()

    if not ret:
        print("End of video stream or error reading frame.")
        break

    # Optional: Convert frame to Grayscale in real-time
    gray_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    cv2.imshow("Video Playback", gray_frame)

    # Adjust waitKey to match video FPS (e.g., ~30 ms delay for 30 FPS)
    if cv2.waitKey(25) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()

```

---
