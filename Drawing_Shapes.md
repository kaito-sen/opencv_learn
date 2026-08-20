Here is the complete guide to **Lesson 1.3: Drawing Shapes (Lines, Rectangles, Circles, Polygons)** using OpenCV and Python.

---

### Key Concepts

When drawing with OpenCV:

* **Image Canvas:** Drawings modify the NumPy array directly in-place.
* **Color:** Defined as a tuple in **BGR** format `(Blue, Green, Red)`, where each value ranges from `0` to `255`.
* **Thickness:** Specified in pixels. A positive integer (e.g., `2`) sets the line width. Passing `-1` (or `cv2.FILLED`) fills the shape completely.
* **Coordinate System:** Origin `(0, 0)` is at the **top-left** corner. $X$ increases moving right, and $Y$ increases moving down.

---

### 1. Lines (`cv2.line`)

To draw a line, specify the starting point `pt1` and ending point `pt2` as `(x, y)` tuples.

```python
import cv2
import numpy as np

# Create a blank black canvas (500x500 pixels, 3 channels)
canvas = np.zeros((500, 500, 3), dtype="uint8")

# cv2.line(img, pt1, pt2, color, thickness)
cv2.line(canvas, (50, 50), (450, 50), (0, 0, 255), 3)  # Red horizontal line

```

---

### 2. Rectangles (`cv2.rectangle`)

To draw a rectangle, specify the top-left corner `pt1` and bottom-right corner `pt2`.

```python
# Outlined Green Rectangle
# cv2.rectangle(img, pt1, pt2, color, thickness)
cv2.rectangle(canvas, (50, 100), (200, 250), (0, 255, 0), 2)

# Filled Blue Rectangle
cv2.rectangle(canvas, (250, 100), (450, 250), (255, 0, 0), -1)

```

---

### 3. Circles (`cv2.circle`)

To draw a circle, specify the center coordinate `(x, y)` and the `radius` in pixels.

```python
# Outlined Yellow Circle
# cv2.circle(img, center, radius, color, thickness)
cv2.circle(canvas, (125, 375), 50, (0, 255, 255), 3)

# Filled Cyan Circle
cv2.circle(canvas, (350, 375), 50, (255, 255, 0), cv2.FILLED)

```

---

### 4. Polygons (`cv2.polylines` & `cv2.fillPoly`)

Polygons require an array of vertex points reshaped into `(-1, 1, 2)`.

```python
# Define vertices for a triangle
pts = np.array([[250, 300], [200, 400], [300, 400]], np.int32)
pts = pts.reshape((-1, 1, 2))

# Option A: Outlined Polygon
# cv2.polylines(img, [pts], isClosed, color, thickness)
cv2.polylines(canvas, [pts], True, (255, 0, 255), 2)

# Option B: Filled Polygon
# cv2.fillPoly(img, [pts], color)
# cv2.fillPoly(canvas, [pts], (255, 0, 255))

```

---

### Complete Executable Script

Here is a full code snippet combining all four shapes on a single canvas:

```python
import cv2
import numpy as np

# 1. Create a black canvas (height=500, width=500, channels=3)
canvas = np.zeros((500, 500, 3), dtype="uint8")

# 2. Draw a Red Line
cv2.line(canvas, (50, 50), (450, 50), (0, 0, 255), 3)

# 3. Draw Rectangles (Green outlined, Blue filled)
cv2.rectangle(canvas, (50, 100), (200, 250), (0, 255, 0), 2)
cv2.rectangle(canvas, (250, 100), (450, 250), (255, 0, 0), -1)

# 4. Draw Circles (Yellow outlined, Cyan filled)
cv2.circle(canvas, (125, 375), 50, (0, 255, 255), 3)
cv2.circle(canvas, (350, 375), 50, (255, 255, 0), -1)

# 5. Draw a White Polygon (Triangle) in the center
pts = np.array([[250, 260], [210, 320], [290, 320]], np.int32)
pts = pts.reshape((-1, 1, 2))
cv2.polylines(canvas, [pts], isClosed=True, color=(255, 255, 255), thickness=2)

# 6. Display the result
cv2.imshow("Drawing Shapes in OpenCV", canvas)
cv2.waitKey(0)
cv2.destroyAllWindows()

```
