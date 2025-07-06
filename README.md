# 📝 Bengali Handwriting Word Segmentation

This project performs **word-level segmentation** on handwritten Bengali text images using OpenCV. It processes the input image to extract and visualize individual words for further tasks like OCR or handwriting analysis.

---

## 🧠 Objective

To **detect and segment words** from a handwritten Bengali text image using image processing techniques such as adaptive thresholding, morphological dilation, and contour detection.

---

## 📦 Requirements

```bash
pip install opencv-python matplotlib numpy
```

---

## 📂 Input

A scanned or photographed image of **handwritten Bengali text** in `.jpg`, `.png`, or `.webp` format.

---

## 🔁 Processing Pipeline

### Step 1: Load and Resize Image
- Reads the input image using OpenCV.
- Converts BGR to RGB for display.
- Resizes image if its width > 1000px (to normalize processing).

### Step 2: Adaptive Thresholding
- Converts image to grayscale.
- Applies **adaptive Gaussian thresholding** with `cv2.THRESH_BINARY_INV` to handle uneven lighting and varied writing.

### Step 3: Line Segmentation
- Applies morphological **dilation** with a horizontal kernel (1×90) to merge characters into lines.
- Finds contours of lines.
- Sorts them top to bottom.
- Draws green bounding boxes for each line.

### Step 4: Word Segmentation
- Uses a smaller horizontal kernel (1×20) to group characters within each line into words.
- For each line ROI:
  - Finds word contours.
  - Filters out small noise contours (area < 300).
  - Draws blue bounding boxes for words.

### Step 5: Crop Specific Word
- Crops and displays the **5th word** from the detected words (if available).

---

## 📊 Outputs

- Original image with:
  - ✅ Green line boxes
  - ✅ Blue word boxes
- The 5th word image cropped and displayed separately.
- Can be extended to export bounding boxes or feed into OCR engines (like `tesserocr` or `easyocr`).

---

## 📁 Output Format Example

```python
words_list = [
    [x1, y1, x2, y2],  # Word 1 bounding box
    [x1, y1, x2, y2],  # Word 2
    ...
]
```

---

## 📌 Notes

- Adjust the **kernel sizes** (`(1, 90)` and `(1, 20)`) based on handwriting density.
- `adaptiveThreshold()` is used instead of fixed thresholding to better handle variation in lighting or ink density.
- Minimum contour area (`< 300`) filters noise—can be tuned based on dataset.

---

## 🔧 Future Improvements

- Character-level segmentation within words.
- Integration with OCR (e.g., EasyOCR or Tesseract).
- Exporting bounding boxes to JSON or XML for dataset creation.
- Web/GUI interface for real-time use.
# OCR-
