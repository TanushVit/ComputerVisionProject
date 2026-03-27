# 🔍 Blur Detection using OpenCV

A Computer Vision project that automatically detects whether an image is **blurred or sharp** using the **Laplacian Variance Method** — a well-established technique in image processing used in autofocus systems, quality control pipelines, and medical imaging.

---

## 📌 Problem Statement

In real-world applications such as surveillance, document scanning, and medical imaging, blurry images can lead to incorrect analysis or poor user experience. This project provides a lightweight, fast, and accurate solution to **automatically classify images as blurred or sharp** without requiring any machine learning model — using only classical Computer Vision techniques.

---

## 💡 How It Works

The project uses the **Laplacian operator** to measure image sharpness:

1. The input image is converted to **grayscale**
2. The **Laplacian** of the grayscale image is computed — this highlights edges and regions of rapid intensity change
3. The **variance** of the Laplacian is calculated:
   - A **sharp image** → high variance (many well-defined edges)
   - A **blurred image** → low variance (few defined edges)
4. A **threshold of 120** is applied:
   - Variance **< 120** → `Image is Blurred`
   - Variance **≥ 120** → `Image is not Blurred`

The script tests two images:
- The **original input image** (`images/input.jpg`)
- An **artificially blurred version** (blurred using a 10×10 averaging kernel internally)

---

## 🧠 Computer Vision Concepts Demonstrated

| Concept | Function Used | Purpose |
|--------|--------------|---------|
| Color Space Conversion | `cv2.cvtColor()` | Convert BGR → Grayscale |
| Image Smoothing / Blurring | `cv2.blur()` | Apply averaging kernel blur |
| Laplacian Edge Detection | `cv2.Laplacian()` | Detect edges and sharpness |
| Statistical Variance | `.var()` | Quantify sharpness level |
| Thresholding Logic | Custom `variance_fn()` | Classify blurred vs sharp |

---

## 🗂️ Project Structure

```
project/
│
├── images/
│   └── input.jpg            # Place your input image here
│
├── blur_detection.py        # Main Python script
└── README.md                # Project documentation
```

---

## ⚙️ Requirements

| Requirement | Version |
|------------|---------|
| Python | 3.7 or above |
| opencv-python | Latest |

---

## 📦 Installation & Setup

### Step 1 — Clone the Repository

```bash
git clone https://github.com/{your-username}/{repo-name}.git
cd {repo-name}
```

### Step 2 — (Recommended) Create a Virtual Environment

```bash
# On Linux / Mac
python -m venv venv
source venv/bin/activate

# On Windows
python -m venv venv
venv\Scripts\activate
```

### Step 3 — Install Dependencies

```bash
pip install opencv-python
```

### Step 4 — Add Your Input Image

Place your image inside the `images/` folder and name it `input.jpg`:

```
images/input.jpg
```

> ⚠️ Make sure the `images/` folder exists. If not, create it manually:
> ```bash
> mkdir images
> ```

---

## 🚀 How to Run

```bash
python blur_detection.py
```

> The script runs entirely from the **command line** — no GUI required.

---

## 📤 Expected Output

```
1st image:  Image is not Blurred
2nd image:  Image is Blurred
```

- **1st image** → Result for the original `images/input.jpg`
- **2nd image** → Result for the internally blurred version of the same image

---

## 🖼️ Sample Results

| Image | Laplacian Variance | Result |
|-------|--------------------|--------|
| Original (sharp) | High (≥ 120) | ✅ Not Blurred |
| Blurred (10×10 kernel) | Low (< 120) | ❌ Blurred |

---

## 🔧 Customization

| Parameter | Location in Code | Description |
|-----------|-----------------|-------------|
| Threshold (`120`) | `variance_fn()` | Increase for stricter detection, decrease for more lenient |
| Blur kernel size (`(10,10)`) | `cv2.blur(img, (10,10))` | Controls how strongly the test image is blurred |
| Input image path | `cv2.imread('images/input.jpg')` | Change to use a different image path |

---

## 🧪 Full Source Code

```python
import cv2

# If variance is less than the set threshold, image is blurred
def variance_fn(var):
    if var < 120:
        s = 'Image is Blurred'
    else:
        s = 'Image is not Blurred'
    return s

# Read the image
img = cv2.imread('images/input.jpg')

# Convert to greyscale
grey_1 = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Apply blur with a 10x10 kernel
blurImg = cv2.blur(img, (10, 10))
grey_2 = cv2.cvtColor(blurImg, cv2.COLOR_BGR2GRAY)

# Calculate Laplacian variance for both images
var_1 = cv2.Laplacian(grey_1, cv2.CV_64F).var()
var_2 = cv2.Laplacian(grey_2, cv2.CV_64F).var()

print("1st image: ", variance_fn(var_1))
print("2nd image: ", variance_fn(var_2))
```

---

## 🧰 Troubleshooting

| Problem | Solution |
|---------|----------|
| `ModuleNotFoundError: cv2` | Run `pip install opencv-python` |
| `NoneType` error on imread | Check that `images/input.jpg` exists |
| Wrong results | Try adjusting the threshold value in `variance_fn()` |
| `images/` folder missing | Run `mkdir images` and add your image |

---

## 📄 License

This project is open-source and free to use for educational purposes.
