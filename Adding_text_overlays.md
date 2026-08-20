Here is the next logical step in your OpenCV tutorial: **Adding Text Overlays** using `cv2.putText`.

---

## 5. Adding Text (`cv2.putText`)

To place text on an image canvas, use the `cv2.putText()` function. It requires specifying the text string, bottom-left origin coordinate, font type, scale factor, color, and thickness.

### Core Syntax

```python
cv2.putText(img, text, org, fontFace, fontScale, color, thickness, lineType)

```

### Parameter Breakdown

* 
**`img`**: The target image/canvas array.


* 
**`text`**: The string to display.


* 
**`org`**: `(x, y)` tuple representing the **bottom-left corner** of the text string.


* 
**`fontFace`**: Built-in OpenCV font style (e.g., `cv2.FONT_HERSHEY_SIMPLEX`).


* 
**`fontScale`**: Multiplier for the font size.


* 
**`color`**: `(B, G, R)` tuple.


* 
**`thickness`**: Thickness of the rendered font.


* 
**`lineType`**: *(Optional)* Line anti-aliasing (using `cv2.LINE_AA` gives smoother edges).



---

### Basic Example

```python
import cv2
import numpy as np

# Create a black canvas (500x500 pixels)
canvas = np.zeros((500, 500, 3), dtype="uint8")

# Add text to the canvas
text = "OpenCV Text Overlay"
position = (50, 250)  # Bottom-left corner of the text
font = cv2.FONT_HERSHEY_SIMPLEX
scale = 1.0
color = (0, 255, 0)  # Green in BGR
thickness = 2

cv2.putText(
    canvas, text, position, font, scale, color, thickness, cv2.LINE_AA
)

cv2.imshow("Text Overlay Example", canvas)
cv2.waitKey(0)
cv2.destroyAllWindows()

```

---

## Common OpenCV Fonts (`fontFace`)

OpenCV includes built-in Hershey fonts:

| Font Constant | Description |
| --- | --- |
| `cv2.FONT_HERSHEY_SIMPLEX` | Normal size sans-serif font |
| `cv2.FONT_HERSHEY_PLAIN` | Small size sans-serif font |
| `cv2.FONT_HERSHEY_DUPLEX` | More complex sans-serif font |
| `cv2.FONT_HERSHEY_COMPLEX` | Normal size serif font |
| `cv2.FONT_HERSHEY_TRIPLEX` | Complex serif font |
| `cv2.FONT_HERSHEY_SCRIPT_SIMPLEX` | Handwriting script style |
| `cv2.FONT_HERSHEY_SCRIPT_COMPLEX` | Complex handwriting script style |

---

## Updated Complete Executable Script

Combining shape drawing with text annotations:

```python
import cv2
import numpy as np

# 1. Create a black canvas
canvas = np.zeros((500, 500, 3), dtype="uint8")

# 2. Draw shapes
cv2.line(canvas, (50, 50), (450, 50), (0, 0, 255), 3)  # Red line
cv2.rectangle(
    canvas, (50, 100), (200, 250), (0, 255, 0), 2
)  # Green rectangle
cv2.circle(canvas, (350, 375), 50, (255, 255, 0), -1)  # Cyan filled circle

# 3. Add text labels to the shapes
cv2.putText(
    canvas,
    "Line",
    (50, 40),
    cv2.FONT_HERSHEY_SIMPLEX,
    0.6,
    (255, 255, 255),
    1,
    cv2.LINE_AA,
)
cv2.putText(
    canvas,
    "Rectangle",
    (50, 90),
    cv2.FONT_HERSHEY_SIMPLEX,
    0.6,
    (255, 255, 255),
    1,
    cv2.LINE_AA,
)
cv2.putText(
    canvas,
    "Circle",
    (310, 315),
    cv2.FONT_HERSHEY_SIMPLEX,
    0.6,
    (255, 255, 255),
    1,
    cv2.LINE_AA,
)

# 4. Display canvas
cv2.imshow("Shapes and Text Overlay", canvas)
cv2.waitKey(0)
cv2.destroyAllWindows()

```
