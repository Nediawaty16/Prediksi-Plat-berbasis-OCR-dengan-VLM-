
# OCR License Plate Recognition with Vision Language Models (VLM)

A Python application that performs Optical Character Recognition (OCR) on Indonesian license plates using Vision Language Models (VLMs) integrated with LMStudio. The system evaluates OCR accuracy using the Character Error Rate (CER) metric.

---

## Features

- **Vision Language Model Support**: Supports models like `google/gemma-3-4b` via LMStudio
- **LMStudio Integration**: Sends image-based queries through LMStudio's API
- **Batch Processing**: Automatically process all images in the test folder
- **Performance Evaluation**: Calculate CER for each prediction from the license plate image
- **CSV Output**: Save comparison results in CSV format
- **Robust Logging**: Prints errors and result summaries

---

## Requirements

### Software Dependencies

Install required Python packages:

```bash
pip install pandas tqdm python-Levenshtein
```

### System Requirements

- **LMStudio**: Must be installed and running locally
- **Python**: Version 3.7 or higher
- **VLM Model**: Load a model that supports vision input (e.g., `google/gemma-3-4b`)

---

## 🛠️ Installation

1. Clone or download the notebook file `Prediksi_Plate_With_VLM.ipynb`.
2. Install the required Python libraries (see above).
3. Install and start LMStudio with a supported model.

---

## 🔧 Configuration

In the notebook, configure the following variables:

```python
IMAGE_FOLDER = "test"                              # Path to folder containing images
GROUND_TRUTH_CSV = os.path.join(IMAGE_FOLDER, "ground_truth.csv")  # Path to ground truth labels
OUTPUT_CSV = "result.csv"                          # Path to save results
MODEL_NAME = "google/gemma-3-4b"                   # Model name loaded in LMStudio
```

---

## 📁 Dataset Structure

```
project/
├── Prediksi_Plate_With_VLM.ipynb
├── test/
│   ├── ground_truth.csv
│   ├── plate001.jpg
│   ├── plate002.png
│   └── ...
```

### `ground_truth.csv` Format:

```
image,ground_truth
plate001.jpg,B1234XYZ
plate002.png,D5678ABC
```

---

## ▶️ Usage

1. **Start LMStudio** with the selected VLM model (`gemma-3-4b`, etc.).
2. **Open the notebook** in Jupyter or VSCode.
3. **Run the cells sequentially**. The process includes:
   - Loading the model via LMStudio
   - Reading all test images
   - Sending OCR prompts to the model
   - Calculating CER
   - Saving results to `result.csv`
   - Printing performance summary

---

## 📤 Output

### CSV File: `result.csv`

```
image,ground_truth,prediction,CER_score
plate001.jpg,B1234XYZ,B1234XYZ,0.0
plate002.png,D5678ABC,D5678AC,0.125
```

### Console Output:

```
✅ Selesai memproses semua gambar.
📁 Hasil disimpan ke 'result.csv'

📊 Statistik Evaluasi:
- Jumlah Gambar       : 50
- Exact Match         : 22 (44.00%)
- Rata-rata CER Score : 0.1173
```

---

## 📏 CER Metric

Character Error Rate (CER) is calculated as:

```
CER = (Levenshtein Distance) / (Length of Ground Truth)
```

- `0.0` = perfect match
- `1.0` = completely incorrect

---

## 🧰 Troubleshooting

| Issue | Solution |
|-------|----------|
| **LMStudio not detected** | Make sure LMStudio is running and the model is loaded |
| **ground_truth.csv not found** | Ensure the path and format are correct |
| **Image not processed** | Check image format (jpg, png) and path |
| **Prediction = "ERROR"** | Could be API issue or image read failure |
| **Model timeout** | Increase timeout in the `respond()` function or optimize model settings |

---

## ✅ Tested Model

- **google/gemma-3-4b** (via LMStudio): Works well for Indonesian license plates

---

## 💡 Suggestions for Future Work

- Add support for image preprocessing (e.g., contrast enhancement)
- Extend evaluation with confidence scores
- Integrate GUI or command-line interface
- Adapt to other formats (motorcycles, foreign plates)
