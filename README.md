# IoT Device Fingerprinting (Network-Traffic Based)

This project demonstrates a **supervised IoT device fingerprinting pipeline** using network-traffic/connection-log features to **classify the originating IoT device**.  
The implementation is provided as a single Jupyter notebook: **`IOT_fingerprinting.ipynb`**.

---

### 1) Data loading
- Loads a CSV dataset (as used in the notebook):
  - `master_data - Copy.csv`

### 2) Data cleaning
- Removes unwanted columns 
- Drops rows with nulls 
- Confirms duplicates and removes it.
- Removes null columns 

### 3) Feature + label preparation
- Target label: `device_name`
- Time column handled separately: `time` (renamed from `ts`)
- Splits into train/test using `train_test_split.

### 4) Encoding (categorical → numeric)
The notebook performs label encoding for multiple categorical columns, and **groups rare categories into `others`** using thresholds before encoding (helps reduce high cardinality).

Examples of columns handled (based on the notebook):
- `id.orig_h` → encoded → `orig_h_enc`
- `orig_p` → `orig_p_enc` (renamed from `id.orig_p`)
- `resp_h` → `resp_h_enc` (renamed from `id.resp_h`)
- `resp_p` → `resp_p_enc` (renamed from `id.resp_p`)
- `proto` → `proto_enc`
- `service` → `service_enc`
- Similar handling for other categorical/log-style fields (e.g., byte-count bins / states / histories depending on dataset)

The notebook uses a helper:
- `del_or_col(col, train, test)` to drop raw categorical columns after encoding.

### 5) Modeling + evaluation
Models used in the notebook:
- **SVC** (`sklearn.svm.SVC`)
- **RandomForestClassifier**
- **KNN** (`KNeighborsClassifier`) (fit shown; scoring may be extended)




