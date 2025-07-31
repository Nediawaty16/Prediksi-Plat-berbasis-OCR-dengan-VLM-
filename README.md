
# OCR License Plate Recognition with Vision Language Models (VLM)

A Python application that performs Optical Character Recognition (OCR) on Indonesian license plates using Vision Language Models (VLMs) integrated with LMStudio. The system evaluates OCR accuracy using the Character Error Rate (CER) metric.

---

## Features

- **Vision Language Model Support**: Supports models like `google/gemma-3-4b` via LMStudio
- **LMStudio Integration**: Communicates with LMStudio's local API to send images and receive predictions
- **Batch Processing**: Automatically processes all images in the test folder
- **Performance Evaluation**: Calculates Character Error Rate (CER) for each license plate prediction
- **CSV Output**: Saves prediction results and comparisons to a CSV file
- **Robust Logging**: Logs errors and provides summary statistics

---

## Requirements

### Software Dependencies

Install required Python packages:

```bash
pip install pandas tqdm python-Levenshtein
```

### System Requirements

- **LMStudio**: Installed and running locally
- **Python**: Version 3.7 or higher
- **VLM Model**: Load a vision-capable model (e.g., `google/gemma-3-4b`) in LMStudio

---

## Installation

1. Clone or download the notebook file `Prediksi_Plate_With_VLM.ipynb`.
2. Install the required Python libraries (see above).
3. Install LMStudio and load a compatible vision-language model.
4. Start LMStudio with API access enabled.

---

## Configuration

In the notebook, configure the following variables according to your folder structure:

```python
IMAGE_FOLDER = "test"                              # Folder containing input images
GROUND_TRUTH_CSV = os.path.join(IMAGE_FOLDER, "ground_truth.csv")  # Ground truth label CSV
OUTPUT_CSV = "result.csv"                          # File path to store results
MODEL_NAME = "google/gemma-3-4b"                   # Model name loaded in LMStudio
```

---

## Dataset Structure

```
Indonesian License Plate Recognition Dataset/
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

## Usage

1. **Start LMStudio** with the selected VLM model (e.g., `google/gemma-3-4b`).
2. **Open the notebook** `Prediksi_Plate_With_VLM.ipynb` using Jupyter Notebook or VSCode.
3. **Run all code cells sequentially**. The notebook will:
   - Connect to LMStudio using the `lmstudio` Python library
   - Read images from the dataset
   - Send each image to the VLM model with an OCR prompt
   - Receive predictions and compare with ground truth
   - Calculate Character Error Rate (CER)
   - Save results to `result.csv`
   - Print summary statistics to the console

---

## LMStudio Integration

This application integrates directly with LMStudio, which acts as a local inference server for Vision Language Models (VLMs).

- The integration is handled using the `lmstudio` Python package:
  ```python
  import lmstudio as lms
  ```
- The library provides a high-level interface to:
  - Load a local vision-language model
  - Encode and send image prompts
  - Receive text predictions from LMStudio’s local API

> 📌 Ensure that LMStudio is running, and the selected model is properly loaded and supports image inputs.

---

## Output

### CSV File: `result.csv`

The following fields will be saved:

```
image,ground_truth,prediction,CER_score
plate001.jpg,B1234XYZ,B1234XYZ,0.0
plate002.png,D5678ABC,D5678AC,0.125
```

### Console Output Example:

```
✅ Selesai memproses semua gambar.
📁 Hasil disimpan ke 'result.csv'

📊 Statistik Evaluasi:
- Jumlah Gambar       : 50
- Exact Match         : 22 (44.00%)
- Rata-rata CER Score : 0.1173
```

---

## Character Error Rate (CER)

CER is used to evaluate how close the predicted license plate is to the ground truth. It is calculated as:

```
CER = (Levenshtein Distance) / (Length of Ground Truth)
```

- `0.0` = perfect match
- `0.1` = 10% character error rate
- `1.0` = completely incorrect

---

## Tested Model

- `google/gemma-3-4b` — confirmed working in LMStudio for Indonesian license plate OCR.

---

## Troubleshooting

| Issue | Possible Cause / Solution |
|-------|---------------------------|
| **LMStudio not detected** | Ensure LMStudio is running and API access is enabled |
| **Model not responding** | Check if the correct model is loaded and supports vision |
| **ground_truth.csv not found** | Verify the path and format of your CSV file |
| **Image not processed** | Check file format (JPG/PNG), permissions, and naming |
| **Prediction = "ERROR"** | May be caused by API issues or invalid input |
| **Model timeout** | Consider increasing the timeout or using a lighter model |

---

## Suggestions for Future Work

- Add image preprocessing (e.g., grayscale, resizing)
- Support more license plate formats (e.g., motorcycles)
- Add confidence score parsing
- Provide web or command-line interface for batch processing
