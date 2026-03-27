# 🔍 Blur Detection using OpenCV

A Computer Vision project that detects whether an image is blurred or sharp using the **Laplacian Variance Method**.

---

## 📌 How It Works

The project uses the **Laplacian operator** to measure the sharpness of an image:

1. The image is converted to **grayscale**.
2. The **Laplacian** of the grayscale image is computed — this highlights edges and regions of rapid intensity change.
3. The **variance** of the Laplacian is calculated. A sharp image has high variance (lots of edges), while a blurred image has low variance (fewer defined edges).
4. A **threshold of 120** is used:
   - Variance **< 120** → Image is **Blurred**
   - Variance **≥ 120** → Image is **Not Blurred**

The script tests two images:
- The **original image** (`images/input.jpg`)
- A **blurred version** of the same image (blurred using a 10×10 averaging kernel)

---

## 🗂️ Project Structure

```
project/
│
├── images/
│   └── input.jpg        # Your input image goes here
│
└── blur_detection.py    # Main Python script
```

---

## ⚙️ Requirements

- Python 3.x
- OpenCV

---

## 📦 Installation

### 1. Clone or download the project

```bash
git clone https://github.com/your-username/blur-detection.git
cd blur-detection
```

### 2. Install dependencies

```bash
pip install opencv-python
```

> **Note:** If you're using a virtual environment (recommended):
> ```bash
> python -m venv venv
> source venv/bin/activate        # On Linux/Mac
> venv\Scripts\activate           # On Windows
> pip install opencv-python
> ```

---

## 🚀 How to Run

### Step 1 — Add your image

Place your input image inside the `images/` folder and name it `input.jpg`.

```
images/input.jpg
```

### Step 2 — Run the script

```bash
python blur_detection.py
```

---

## 📤 Expected Output

```
1st image:  Image is not Blurred
2nd image:  Image is Blurred
```

- **1st image** → Result for the original `input.jpg`
- **2nd image** → Result for the artificially blurred version (blurred using a 10×10 kernel internally)

---

## 🔧 Customization

| Parameter | Location in Code | Description |
|-----------|-----------------|-------------|
| Threshold value (`120`) | `variance_fn()` | Increase for stricter sharpness detection, decrease for more lenient |
| Blur kernel size (`(10,10)`) | `cv2.blur(img, (10,10))` | Controls how aggressively the test image is blurred |
| Input image path | `cv2.imread('images/input.jpg')` | Change to use a different image file |

---

## 🧠 Concepts Used

- **Grayscale Conversion** — `cv2.cvtColor()`
- **Image Blurring** — `cv2.blur()` with an averaging kernel
- **Laplacian Operator** — `cv2.Laplacian()` for edge detection / sharpness measurement
- **Variance** — Statistical measure to quantify the spread of edge intensity values

---

## 📝 Notes

- Make sure the `images/` folder exists and contains `input.jpg` before running the script.
- You can adjust the **threshold (120)** based on your specific use case or dataset.
- This method works best for detecting out-of-focus or motion blur in standard photographs.

---

## 📄 License

This project is open-source and free to use for educational purposes.
