Here is a practical guide to **reading, displaying, and writing images** using OpenCV and Python, building directly on **Lesson 1.1** of the curriculum.

---

## Core IO Operations

OpenCV handles images as **NumPy arrays** with **BGR** (Blue, Green, Red) channel ordering.

### 1. Reading an Image (`cv2.imread`)

`cv2.imread()` loads an image from a specified file path.

```python
import cv2

# Read an image in full color (default flag: cv2.IMREAD_COLOR)
image = cv2.imread("example.png")

# Check if the image was successfully loaded
if image is None:
    print("Error: Could not load image. Check the file path.")
else:
    print("Upload photo successfully!")
```
Image Existing:  
<img width="701" height="188" alt="image" src="https://github.com/user-attachments/assets/bb2c6d76-38d6-4f38-9f66-a1093fba0120" />  
Image not found:  
<img width="1153" height="905" alt="image" src="https://github.com/user-attachments/assets/85e64427-a394-410b-9922-784c8a91cd8b" />  


#### Read Modes / Flags:

* `cv2.IMREAD_COLOR` (or `1`): Loads a 3-channel BGR color image.
* `cv2.IMREAD_GRAYSCALE` (or `0`): Loads the image in grayscale (single channel).
* `cv2.IMREAD_UNCHANGED` (or `-1`): Loads the image including the alpha (transparency) channel if present.

---

### 2. Displaying an Image (`cv2.imshow`)

`cv2.imshow()` displays the image in a GUI window.

```python
# Create a window and display the image
cv2.imshow("Displayed Image", image)

# Keep the window open until any key is pressed (0 = wait indefinitely)
cv2.waitKey(0)

# Destroy all created GUI windows to free up memory
cv2.destroyAllWindows()

```

> **Key Functions:**
> * `cv2.waitKey(delay)`: Waits for a keyboard event for `delay` milliseconds. If `0`, it waits indefinitely.
> * `cv2.destroyAllWindows()`: Closes all active OpenCV image windows.

Result:  
<img width="1342" height="728" alt="image" src="https://github.com/user-attachments/assets/b46f2c9b-f05c-4cac-879d-fb0872821818" />  

---

### 3. Writing / Saving an Image (`cv2.imwrite`)

`cv2.imwrite()` saves an image array to a file on your disk. The image format is determined by the file extension provided (e.g., `.png`, `.jpg`).

```python
# Save the loaded image to a new file
success = cv2.imwrite("output_image.png", image)

if success:
    print("Image saved successfully!")

```
<img width="1763" height="771" alt="image" src="https://github.com/user-attachments/assets/2dc9780d-8cc8-491c-8ef6-510cf0fc406b" />

---

## Understanding Image Data (NumPy Properties)

Because OpenCV represents images as **NumPy arrays**, you can inspect their structure using standard NumPy attributes:

```python
import cv2

image = cv2.imread("example.jpg")

# 1. Dimensions (Height, Width, Channels)
print("Shape:", image.shape) 
# Example output for color image: (1080, 1920, 3)
# Example output for grayscale image: (1080, 1920)

# 2. Data Type (Pixel values typically range from 0 to 255)
print("Data Type:", image.dtype) 
# Output: uint8 (Unsigned 8-bit integer)

# 3. Total number of pixels / values
print("Total Size:", image.size)

```
Result:  
```bash
Shape: (512, 512, 3)
Data Type: uint8
Total Size: 786432
```
---

## Complete Example Script

Here is a full Python snippet that reads an image, converts it to grayscale using a read flag, displays both versions, and saves the result:

```python
import cv2

# 1. Load original image and grayscale version
img_color = cv2.imread("sample.jpg", cv2.IMREAD_COLOR)
img_gray = cv2.imread("sample.jpg", cv2.IMREAD_GRAYSCALE)

if img_color is not None:
    # 2. Display both images
    cv2.imshow("Color Window", img_color)
    cv2.imshow("Grayscale Window", img_gray)

    # 3. Save the grayscale output
    cv2.imwrite("sample_gray.png", img_gray)

    # 4. Wait for key press to close windows
    cv2.waitKey(0)
    cv2.destroyAllWindows()
else:
    print("Failed to find 'sample.jpg'")

```
