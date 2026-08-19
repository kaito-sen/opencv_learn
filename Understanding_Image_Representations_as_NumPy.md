In OpenCV, digital images are stored as multi-dimensional **NumPy arrays**. Understanding the `shape` and `dtype` properties allows you to correctly manipulate pixels, coordinates, and color channels.

---

**1. The `shape` Property**
The `shape` tuple describes the dimensions of the image matrix. OpenCV uses the structure `(Height, Width, Channels)`:

* **Color Images (3D Array):** Returns a tuple of 3 integers: `(height, width, channels)`.
* `height`: Number of pixel rows.
* `width`: Number of pixel columns.
* `channels`: Number of color planes. Standard color images loaded by OpenCV have `3` channels arranged in **BGR** (Blue, Green, Red) order.
* *Example:* `(1080, 1920, 3)` means an image 1080 pixels high, 1920 pixels wide, with 3 color channels.


* **Grayscale Images (2D Array):** Returns a tuple of 2 integers: `(height, width)`. Because there is only a single intensity channel, no third dimension is included.
* *Example:* `(1080, 1920)`.



---

**2. The `dtype` Property**
The `dtype` (data type) describes how pixel values are stored in memory:

* **Standard Images (`uint8`):** Unsigned 8-bit integers. Pixel values range strictly from **0** (pure black) to **255** (pure white or full channel intensity). This is the standard data type for standard loaded images.
* **Floating-Point Images (`float32` or `float64`):** Used primarily during mathematical operations (such as high dynamic range processing or filter convolutions), where pixel intensities are normalized between **0.0** and **1.0**.

---

**Python Code Example**

```python
import cv2

# Load a color image and a grayscale image
img_color = cv2.imread("example.jpg", cv2.IMREAD_COLOR)
img_gray = cv2.imread("example.jpg", cv2.IMREAD_GRAYSCALE)

# Inspecting Shape
print("Color Shape:", img_color.shape)  # Returns (Height, Width, 3)
print("Gray Shape:", img_gray.shape)    # Returns (Height, Width)

# Inspecting Data Type
print("Data Type:", img_color.dtype)    # Returns uint8

# Inspecting Total Values (Height x Width x Channels)
print("Total Elements:", img_color.size)

```
Result:  
```bash
Color Shape: (512, 512, 3)
Gray Shape: (512, 512)
Data Type: uint8
Total Elements: 786432
```
