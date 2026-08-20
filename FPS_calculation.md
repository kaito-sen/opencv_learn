This guide covers **Lesson 1.2** of your OpenCV curriculum, focusing on calculating **Frames Per Second (FPS)** and setting up **real-time frame manipulation loops**.

---

### Core Concepts

1. **FPS Calculation**: To measure real-time processing performance, calculate the time elapsed between frame iterations using `time.time()` or OpenCV's high-precision timing function `cv2.getTickCount()`.

$$\text{FPS} = \frac{1}{\text{Time to process one frame}}$$


2. **Exponential Moving Average (EMA)**: Frame times fluctuate wildly due to system tasks. Applying an EMA smooths the displayed FPS readout:

$$\text{FPS}_{\text{smoothed}} = \alpha \cdot \text{FPS}_{\text{current}} + (1 - \alpha) \cdot \text{FPS}_{\text{previous}}$$


3. **Real-time Loop**: Every frame captured from a webcam or video stream is modified (e.g., drawing overlays, color conversions, spatial transformations) inside the read loop before rendering with `cv2.imshow()`.

---

### Complete Python Implementation

The following script reads a video stream, applies real-time frame manipulation (grayscale conversion + edge detection overlay), calculates smoothed FPS, and overlays performance metrics directly onto the frame.

```python
import cv2
import time

# Initialize video stream (0 for default webcam or path string to video file)
cap = cv2.VideoCapture(0)

if not cap.isOpened():
    print("Error: Could not open video source.")
    exit()

# Variables for FPS calculation
prev_frame_time = 0
curr_frame_time = 0
fps_smoothed = 0
alpha = 0.1  # Smoothing factor for EMA (0 < alpha <= 1)

while cap.isOpened():
    # 1. Capture frame-by-frame
    ret, frame = cap.read()
    if not ret:
        print("End of stream or failed to fetch frame.")
        break

    # 2. Start frame timer
    curr_frame_time = time.time()

    # -------------------------------------------------------------
    # 3. Real-Time Frame Manipulation Loop
    # -------------------------------------------------------------
    # Example A: Convert to Grayscale
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    # Example B: Canny Edge Detection (Lesson 3.1 preview)
    edges = cv2.Canny(gray, threshold1=100, threshold2=200)

    # Example C: Convert single-channel edge mask back to BGR for color overlay
    edges_bgr = cv2.cvtColor(edges, cv2.COLOR_GRAY2BGR)

    # Example D: Combine original color frame with edge detection side-by-side
    combined_frame = cv2.hconcat([frame, edges_bgr])
    # -------------------------------------------------------------

    # 4. Calculate FPS
    time_diff = curr_frame_time - prev_frame_time
    if time_diff > 0:
        fps_instant = 1.0 / time_diff
        # Smooth FPS reading to prevent rapid jumping on screen
        fps_smoothed = (alpha * fps_instant) + ((1 - alpha) * fps_smoothed)

    prev_frame_time = curr_frame_time

    # 5. Overlay FPS counter on top of processed frame
    fps_text = f"FPS: {fps_smoothed:.1f}"
    cv2.putText(
        img=combined_frame,
        text=fps_text,
        org=(20, 50),
        fontFace=cv2.FONT_HERSHEY_SIMPLEX,
        fontScale=1.0,
        color=(0, 255, 0),  # Green text
        thickness=2,
        lineType=cv2.LINE_AA
    )

    # 6. Display output window
    cv2.imshow("Real-Time Processing & FPS Counter", combined_frame)

    # Exit when 'q' key is pressed
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Clean up resources
cap.release()
cv2.destroyAllWindows()

```

---

### High-Precision Alternative (`cv2.getTickCount`)

For microsecond precision when profiling heavy processing loops, use OpenCV's built-in timing functions:

```python
# Before frame processing block
t1 = cv2.getTickCount()

# --- Frame processing operations here ---

# After frame processing block
t2 = cv2.getTickCount()

# Calculate time spent processing in seconds
elapsed_sec = (t2 - t1) / cv2.getTickFrequency()
processing_fps = 1.0 / elapsed_sec if elapsed_sec > 0 else 0

```
