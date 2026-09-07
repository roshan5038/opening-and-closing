# EX 10 Opening and Closing Operations Using OpenCV

## Aim

To write a Python program using OpenCV to perform morphological **Opening** and **Closing** operations on an image.

The program performs the following operations:

* Creation of a blank image
* Adding text to the image
* Morphological Opening
* Morphological Closing

---

## Experiment Details

* **Experiment No.:** 10
* **Experiment Name:** Opening and Closing Operations Using OpenCV
* **Name:** Roshan V
* **Register No.:** 212225240124

---

## Learning Objective

The objectives of this experiment are:

* To understand morphological Opening and Closing operations.
* To learn how structuring elements are used in morphological processing.
* To implement Opening using OpenCV.
* To implement Closing using OpenCV.
* To understand the difference between Opening and Closing operations.
* To observe the effect of morphological operations on an image.

---

## Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (`cv2`)
* NumPy
* Matplotlib

---

## Libraries Used

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### OpenCV

OpenCV is used to:

* Create and manipulate the image.
* Add text using `cv2.putText()`.
* Perform morphological Opening.
* Perform morphological Closing.
* Convert BGR images to RGB for display.

### NumPy

NumPy is used to:

* Create the blank image.
* Create the 3×3 structuring element.

### Matplotlib

Matplotlib is used to display the original image and the result of the Opening operation.

---

# Algorithm

## Step 1: Import Required Libraries

Import OpenCV, NumPy, and Matplotlib.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

## Step 2: Create a Blank Image

A blank image of size **500 × 500 pixels** with three color channels is created using NumPy.

```python
image = np.zeros((500, 500, 3), dtype=np.uint8)
```

The image is initialized with zeros, producing a black background.

---

## Step 3: Add Text to the Image

The text **"Open and Close"** is added to the blank image using OpenCV's `cv2.putText()` function.

```python
font = cv2.FONT_HERSHEY_SIMPLEX

cv2.putText(
    image,
    'Open and Close',
    (100, 250),
    font,
    1,
    (255, 255, 255),
    2,
    cv2.LINE_AA
)
```

The text is displayed in white on the black background.

### Text Parameters

| Parameter  |                  Value | Description               |
| ---------- | ---------------------: | ------------------------- |
| Text       |       `Open and Close` | Text written on image     |
| Position   |           `(100, 250)` | Starting position of text |
| Font       | `FONT_HERSHEY_SIMPLEX` | Font type                 |
| Font Scale |                    `1` | Text size                 |
| Color      |        `(255,255,255)` | White                     |
| Thickness  |                    `2` | Text thickness            |
| Line Type  |              `LINE_AA` | Anti-aliased text         |

---

## Step 4: Create Structuring Element

A **3 × 3 square kernel** is created using NumPy.

```python
kernel = np.ones((3, 3), np.uint8)
```

The kernel is:

```text
1 1 1
1 1 1
1 1 1
```

This kernel is used for both Opening and Closing operations.

---

## Step 5: Display the Input Image

The original image containing the text is displayed using Matplotlib.

```python
plt.imshow(
    cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
)

plt.title("Input Image with Text")
plt.axis('off')
```

The BGR image is converted to RGB before displaying because OpenCV uses BGR channel ordering.

---

# Step 6: Opening Operation

Morphological Opening consists of:

**Erosion followed by Dilation**

The operation is performed using:

```python
opened_image = cv2.morphologyEx(
    image,
    cv2.MORPH_OPEN,
    kernel
)
```

The `cv2.MORPH_OPEN` operation applies morphological Opening using the specified 3×3 kernel.

### Purpose of Opening

Opening is commonly used to:

* Remove small foreground regions.
* Reduce small noise.
* Remove thin protrusions.
* Smooth object boundaries.

---

## Step 7: Display Opening Result

The Opening result is displayed using Matplotlib.

```python
plt.imshow(
    cv2.cvtColor(opened_image, cv2.COLOR_BGR2RGB)
)

plt.title("Opening Operation")
plt.axis('off')
```

The output is displayed with the title:

**Opening Operation**

---

# Step 8: Closing Operation

Morphological Closing consists of:

**Dilation followed by Erosion**

The operation is performed using:

```python
closed_image = cv2.morphologyEx(
    image,
    cv2.MORPH_CLOSE,
    kernel
)
```

The `cv2.MORPH_CLOSE` operation applies morphological Closing using the same 3×3 kernel.

### Purpose of Closing

Closing is commonly used to:

* Fill small holes.
* Close small gaps.
* Connect nearby foreground regions.
* Produce more continuous object boundaries.

---

# Complete Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Create a blank image
image = np.zeros((500, 500, 3), dtype=np.uint8)

# Add text on the image using cv2.putText
font = cv2.FONT_HERSHEY_SIMPLEX
cv2.putText(
    image,
    'Open and Close',
    (100, 250),
    font,
    1,
    (255, 255, 255),
    2,
    cv2.LINE_AA
)

# Create a simple square kernel (3x3)
kernel = np.ones((3, 3), np.uint8)

# Display the input image
plt.imshow(
    cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
)
plt.title("Input Image with Text")
plt.axis('off')

# Opening is erosion followed by dilation
opened_image = cv2.morphologyEx(
    image,
    cv2.MORPH_OPEN,
    kernel
)

# Display the result of Opening
plt.imshow(
    cv2.cvtColor(opened_image, cv2.COLOR_BGR2RGB)
)
plt.title("Opening Operation")
plt.axis('off')

# Closing is dilation followed by erosion
closed_image = cv2.morphologyEx(
    image,
    cv2.MORPH_CLOSE,
    kernel
)
```

---

# Working Principle

The complete processing flow is:

```text
Blank Image
     ↓
Add "Open and Close" Text
     ↓
Create 3×3 Kernel
     ↓
Display Input Image
     ↓
 ┌─────────────────────┐
 │                     │
 ↓                     ↓
Opening               Closing
 ↓                     ↓
Erosion               Dilation
 ↓                     ↓
Dilation              Erosion
 ↓                     ↓
Opened Image          Closed Image
```

---

# Opening Operation

Opening is performed using **erosion followed by dilation**.

```text
Opening = Erosion → Dilation
```

It generally removes small foreground details while preserving larger structures.

### Effects

* Removes small foreground noise.
* Removes thin protrusions.
* Smooths object boundaries.
* Can separate objects that are connected by thin regions.

---

# Closing Operation

Closing is performed using **dilation followed by erosion**.

```text
Closing = Dilation → Erosion
```

It generally fills small holes and closes small gaps in foreground objects.

### Effects

* Fills small holes.
* Closes small gaps.
* Connects nearby foreground regions.
* Smooths and strengthens object boundaries.

---

# Comparison

| Operation | Process            | Main Effect                      |
| --------- | ------------------ | -------------------------------- |
| Original  | No operation       | Original text                    |
| Opening   | Erosion → Dilation | Removes small foreground details |
| Closing   | Dilation → Erosion | Fills small gaps and holes       |

---

# Expected Output

## Original Image

A black **500 × 500** image containing the white text:


**Open and Close**

The output is displayed with the title:

**Input Image with Text**
<img width="646" height="628" alt="image" src="https://github.com/user-attachments/assets/5f5ff432-34b4-4bb8-b822-34f949e399f9" />

---

## Opening Operation

The input image is processed using morphological Opening with a **3×3 kernel**.

The resulting image is displayed with the title:

**Opening Operation**

Opening performs erosion followed by dilation.

---

## Closing Operation

The input image is processed using morphological Closing with the same **3×3 kernel**.

The resulting image is stored in the variable:

```python
closed_image
```

The attached notebook calculates the Closing result but does **not currently contain a separate Matplotlib display command for `closed_image`**.

---

# Applications

## Opening

Opening can be used for:

* Noise removal.
* Removing small foreground objects.
* Image preprocessing.
* Object segmentation.
* Smoothing object boundaries.

## Closing

Closing can be used for:

* Filling small holes.
* Closing gaps.
* Connecting nearby objects.
* Improving segmented regions.
* Smoothing object boundaries.

---

# Advantages

## Opening

* Removes small unwanted foreground regions.
* Reduces small noise.
* Preserves larger object structures.
* Helps improve image segmentation.

## Closing

* Fills small holes and gaps.
* Connects nearby foreground regions.
* Helps preserve larger object structures.
* Improves continuity of segmented objects.

---

# Limitations

* The result depends on the size and shape of the structuring element.
* A large kernel may remove important image details during Opening.
* A large kernel may merge objects during Closing.
* The experiment uses only a 3×3 square kernel.
* The experiment performs the morphological operations with the default iteration setting.

---

# Difference Between Opening and Closing

| Feature                        | Opening                      | Closing                      |
| ------------------------------ | ---------------------------- | ---------------------------- |
| Basic operation                | Erosion followed by Dilation | Dilation followed by Erosion |
| Removes small foreground noise | Yes                          | No                           |
| Fills small holes              | No                           | Yes                          |
| Closes small gaps              | No                           | Yes                          |
| Removes thin protrusions       | Yes                          | Generally no                 |
| Expands foreground regions     | No                           | Initially, during dilation   |
| Main purpose                   | Noise/detail removal         | Gap/hole filling             |

---

# Result

Thus, the morphological **Opening and Closing operations** were successfully implemented using OpenCV.

A blank 500×500 image was created using NumPy, the text **"Open and Close"** was added using `cv2.putText()`, and a **3×3 square structuring element** was created. Morphological Opening was performed using `cv2.MORPH_OPEN`, while Morphological Closing was performed using `cv2.MORPH_CLOSE`.

The experiment demonstrates the basic difference between Opening and Closing operations in morphological image processing.

---

## Developed By

**Name:** Roshan V

**Register No:** 212225240124
