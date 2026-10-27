# edge-detection-opencv

## Aim

To perform edge detection using Sobel, Roberts, Prewitt, Laplacian, and Canny edge detectors.

---

## Software Required

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

## ⚙️ Algorithm

### Step 1:

Import all the necessary modules for the program.

### Step 2:

Load an image using `cv2.imread()`.

### Step 3:

Convert the image to grayscale.

### Step 4:

Apply **Sobel operator** using OpenCV to detect edges.

### Step 5:

Apply **Prewitt operator** using custom kernels.

### Step 6:

Apply **Roberts operator** using custom kernels.

### Step 7:

Apply **Laplacian operator** using OpenCV.

### Step 8:

Apply **Canny edge detector** using OpenCV.

### Step 9:

Display all edge-detected images for comparison.

---

## Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Load an image using cv2.imread()
image = cv2.imread('your_image.jpg')

# Step 3: Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Step 4: Apply Sobel operator using OpenCV
sobel_x = cv2.Sobel(gray_image, cv2.CV_64F, 1, 0, ksize=3) 
sobel_y = cv2.Sobel(gray_image, cv2.CV_64F, 0, 1, ksize=3) 

sobel_x = cv2.convertScaleAbs(sobel_x)
sobel_y = cv2.convertScaleAbs(sobel_y)
sobel_combined = cv2.bitwise_or(sobel_x, sobel_y)

# Step 5: Apply Prewitt operator using custom kernels
kernel_prewitt_x = np.array([[-1, 0, 1], 
                             [-1, 0, 1], 
                             [-1, 0, 1]])
kernel_prewitt_y = np.array([[ 1,  1,  1], 
                             [ 0,  0,  0], 
                             [-1, -1, -1]])

prewitt_x = cv2.filter2D(gray_image, -1, kernel_prewitt_x)
prewitt_y = cv2.filter2D(gray_image, -1, kernel_prewitt_y)
prewitt_combined = cv2.bitwise_or(prewitt_x, prewitt_y)

# Step 6: Apply Roberts operator using custom kernels
kernel_roberts_x = np.array([[1, 0], 
                             [0, -1]])
kernel_roberts_y = np.array([[0, 1], 
                             [-1, 0]])

roberts_x = cv2.filter2D(gray_image, -1, kernel_roberts_x)
roberts_y = cv2.filter2D(gray_image, -1, kernel_roberts_y)
roberts_combined = cv2.bitwise_or(roberts_x, roberts_y)

# Step 7: Apply Laplacian operator using OpenCV
laplacian = cv2.Laplacian(gray_image, cv2.CV_64F)
laplacian = cv2.convertScaleAbs(laplacian)

# Step 8: Apply Canny edge detector using OpenCV
canny = cv2.Canny(gray_image, 100, 200)

# Step 9: Display all edge-detected images for comparison
images = [gray_image, sobel_combined, prewitt_combined, roberts_combined, laplacian, canny]
titles = ['Original Grayscale', 'Sobel Edge', 'Prewitt Edge', 'Roberts Edge', 'Laplacian Edge', 'Canny Edge']

plt.figure(figsize=(15, 10))
for i in range(6):
    plt.subplot(2, 3, i+1)
    plt.imshow(images[i], cmap='gray') 
    plt.title(titles[i])
    plt.axis('off') 

plt.tight_layout()
plt.show()

```

---

## Developed By

* **Name:** Varun Aravamudhan
* **Register No:** 212224240178

---

## Output
![alt text](image.png)

### Sobel Edge Detector

* Detects edges in horizontal and vertical directions
* Produces gradient-based edge map

### Prewitt Edge Detector

* Similar to Sobel but simpler kernel
* Detects directional edges

### Roberts Edge Detector

* Detects edges using diagonal gradients
* Sensitive to noise

### Laplacian Edge Detector

* Detects edges using second-order derivatives
* Highlights rapid intensity changes

### Canny Edge Detector

* Multi-stage edge detection
* Produces clean and thin edges

---

## Result

Thus, edges are successfully detected using Sobel, Prewitt, Roberts, Laplacian, and Canny edge detection techniques. Each method highlights edges differently based on gradient and intensity variations, improving feature extraction and analysis.