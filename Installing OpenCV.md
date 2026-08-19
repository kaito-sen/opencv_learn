Here is a step-by-step guide to installing **OpenCV (`opencv-python`)** and **NumPy**.

---

## 1. Fast Installation Command

Both packages can be installed via `pip`. Open your terminal or command prompt and run:

```bash
pip install opencv-python numpy

```

> **Note:** Installing `opencv-python` will automatically pull `numpy` as a dependency, but explicitly listing both ensures both packages are up-to-date.

---

## 2. Choosing the Right Package Variant

Depending on your project needs, select the OpenCV package that fits your use case:

| Package Variant | Installation Command | Use Case |
| --- | --- | --- |
| **Standard** | `pip install opencv-python` | Core OpenCV modules + GUI display support (Most users) |
| **With Contrib** | `pip install opencv-contrib-python` | Includes standard modules **+ experimental/extra algorithms** |
| **Headless** | `pip install opencv-python-headless` | No GUI backend; optimized for **docker, cloud servers, or CI/CD pipelines** |

*(Only install **one** variant at a time to prevent package conflicts.)*

---

## 3. Step-by-Step Environment Setup

### Step 1: Create & Activate a Virtual Environment (Recommended)

Isolating dependencies per project prevents system-wide library mismatches.

* **Windows:**
```cmd
python -m venv venv
venv\Scripts\activate

```


* **macOS / Linux:**
```bash
python3 -m venv venv
source venv/bin/activate

```



### Step 2: Upgrade Pip & Install Packages

```bash
python -m pip install --upgrade pip
pip install opencv-python numpy

```

---

## 4. Verify the Installation

To confirm both libraries are installed properly and check their version numbers, run the following Python snippet in your terminal:

```bash
python -c "import cv2, numpy as np; print('OpenCV:', cv2.__version__); print('NumPy:', np.__version__)"

```

**Expected Output:**

```text
OpenCV: 4.x.x
NumPy: 1.x.x (or 2.x.x)

```
<img width="428" height="437" alt="image" src="https://github.com/user-attachments/assets/5587b949-af87-478a-8208-14dd85aba961" />
<img width="977" height="53" alt="image" src="https://github.com/user-attachments/assets/e2e37a41-e068-408f-8be4-51289ef40e77" />

---

## 5. Quick Test Script

Run this basic test script to ensure image creation and matrix manipulation work correctly:

```python
import cv2
import numpy as np

# Create a 300x300 black canvas (NumPy array)
canvas = np.zeros((300, 300, 3), dtype="uint8")

# Draw a blue circle in the center using OpenCV
cv2.circle(canvas, (150, 150), 50, (255, 0, 0), -1)

# Display the image window
cv2.imshow("OpenCV Test", canvas)
cv2.waitKey(0)
cv2.destroyAllWindows()

```

Run code command: `py main.py`

<img width="301" height="328" alt="image" src="https://github.com/user-attachments/assets/30c30390-3f32-4d85-a60a-a17be5e31ab0" />
