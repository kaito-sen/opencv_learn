Here is the complete guide to **writing video outputs (`cv2.VideoWriter`)** in OpenCV, directly continuing **Lesson 1.2** of your OpenCV curriculum.

---

**Core Concepts & Workflow**
Writing video with OpenCV requires initializing a `cv2.VideoWriter` object. Unlike saving single static images via `cv2.imwrite()`, saving video requires configuring 4 parameters upfront:

1. **Output Filename**: Path and file extension (e.g., `"output.mp4"` or `"output.avi"`).
2. **FourCC Code**: A 4-character code specifying the video codec (e.g., `'XVID'`, `'mp4v'`, `'MJPG'`).
3. **Frames Per Second (FPS)**: Desired playback speed (e.g., `20.0`, `30.0`).
4. **Frame Size**: Resolution as a `(width, height)` tuple. **Crucial:** OpenCV expects `(width, height)`, which is the reverse order of NumPy's `(height, width)` shape.

---

**Common FourCC Code Combinations**

* **MP4 Container**: `cv2.VideoWriter_fourcc(*'mp4v')` or `cv2.VideoWriter_fourcc(*'X264')`
* **AVI Container**: `cv2.VideoWriter_fourcc(*'XVID')` or `cv2.VideoWriter_fourcc(*'MJPG')`

---

**1. Recording a Live Webcam Stream to File**
This script captures frames from your webcam, displays them live, and writes them directly to an `.mp4` file.

```python
import cv2

# 1. Initialize Webcam
cap = cv2.VideoCapture(0)

if not cap.isOpened():
    print("Error: Could not open webcam.")
    exit()

# 2. Get webcam frame dimensions and FPS
frame_width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
frame_height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fps = cap.get(cv2.CAP_PROP_FPS)

# Fallback FPS if webcam doesn't report it properly
if fps == 0:
    fps = 20.0

frame_size = (frame_width, frame_height)

# 3. Define the Codec and create VideoWriter object
fourcc = cv2.VideoWriter_fourcc(*'mp4v')
out = cv2.VideoWriter('recorded_webcam.mp4', fourcc, fps, frame_size)

print("Recording started. Press 'q' to stop...")

while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        print("Error: Failed to grab frame.")
        break

    # Write frame to output file
    out.write(frame)

    # Show live feed
    cv2.imshow('Recording Live Stream', frame)

    # Stop recording when 'q' is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# 4. Release all resources (Failure to release VideoWriter leads to corrupted files)
cap.release()
out.release()
cv2.destroyAllWindows()
print("Video successfully saved!")

```

---

**2. Processing an Existing Video & Saving Output**
If you modify frames during processing (e.g., converting to grayscale, applying masks, or resizing), ensure the frame format matches what `VideoWriter` expects:

* **Grayscale Frames**: Must be converted back to 3-channel BGR (`cv2.cvtColor(gray, cv2.COLOR_GRAY2BGR)`) before passing to `out.write()`, OR initialize `VideoWriter` with `isColor=False`.

```python
import cv2

# Open existing video file
cap = cv2.VideoCapture("input_video.mp4")

if not cap.isOpened():
    print("Error: Could not open input video.")
    exit()

# Fetch properties from source video
width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
fps = cap.get(cv2.CAP_PROP_FPS)

# Setup writer for modified output
fourcc = cv2.VideoWriter_fourcc(*'XVID')
out = cv2.VideoWriter('processed_output.avi', fourcc, fps, (width, height))

while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break

    # Example Processing: Convert frame to Grayscale
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # Convert 1-channel Grayscale back to 3-channel BGR for writing
    processed_frame = cv2.cvtColor(gray, cv2.COLOR_GRAY2BGR)

    # Write processed frame
    out.write(processed_frame)

    cv2.imshow('Processing Stream', processed_frame)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
out.release()
cv2.destroyAllWindows()

```

---

**Key Troubleshooting Tips**

* **Corrupted or 0-KB Output File**: This almost always happens if `out.release()` is omitted before exiting the script, or if the `(width, height)` dimension in `cv2.VideoWriter` does not **exactly** match the dimension of the frames being passed to `out.write()`.
* **Dimension Swapping**: Remember that `frame.shape` in NumPy gives `(height, width, channels)`, but `VideoWriter` expects `(width, height)`.
