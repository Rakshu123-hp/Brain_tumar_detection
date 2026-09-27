# 🧠 Brain MRI Tumor Classification

A deep learning-based web application for classifying brain MRI scans using multiple convolutional neural network architectures.

The project compares three deep learning approaches:

- Custom CNN
- VGG16 Transfer Learning
- ResNet50 Fine-Tuning

The models support both binary and multi-class brain MRI classification and are integrated into an interactive Streamlit application.

---

## 📌 Project Overview

Brain MRI analysis is an important application of medical image processing and deep learning.

This project explores how different deep learning architectures perform on brain MRI image classification.

The system provides two classification tasks:

### 1. Binary Classification

Classifies MRI scans into:

- No Tumor
- Tumor

### 2. Multi-Class Classification

Classifies MRI scans into four categories:

- Healthy
- Glioma
- Meningioma
- Pituitary

Three different architectures are evaluated for both tasks.

---

## 🤖 Models Used

### Custom CNN

A convolutional neural network developed from scratch for brain MRI image classification.

### VGG16

VGG16 is used with transfer learning from ImageNet weights.

### ResNet50

ResNet50 is used with fine-tuning of the final layers to adapt the pretrained architecture to the MRI classification task.

---

## 📊 Model Performance

The validation results from the project are:

| Model | Binary Classification | Multi-Class Classification |
|---|---:|---:|
| Custom CNN | 96.43% | 71.04% |
| VGG16 | 97.83% | 83.19% |
| ResNet50 | 99.07% | 96.18% |

### Binary Classification

- Custom CNN: 96.43%
- VGG16: 97.83%
- ResNet50: 99.07%

### Multi-Class Classification

- Custom CNN: 71.04%
- VGG16: 83.19%
- ResNet50: 96.18%

The project also includes accuracy/loss curves and confusion matrices for model evaluation.

---

## 🏗️ System Architecture

```text
                    Brain MRI Image
                           │
                           ▼
                  Image Preprocessing
                           │
                           ▼
                    Select Model
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
      Custom CNN         VGG16          ResNet50
          │                │                │
          └────────────────┼────────────────┘
                           │
                           ▼
                     Classification
                           │
                           ▼
                Prediction + Confidence
````

---

## 🔄 Image Processing Pipeline

The uploaded MRI image goes through the following stages:

```text
MRI Image
   │
   ▼
Image Upload
   │
   ▼
RGB Conversion
   │
   ▼
Brain Region Preprocessing
   │
   ▼
Image Resizing
   │
   ▼
Normalization
   │
   ▼
Deep Learning Model
   │
   ▼
Prediction
   │
   ▼
Class + Confidence
```

The application automatically resizes the uploaded image according to the selected model.

---

## 🖥️ Streamlit Application

The project includes an interactive Streamlit interface.

### Detection

Users can:

1. Upload an MRI image.
2. Select a classification model.
3. Run the prediction.
4. View the predicted class.
5. View the prediction confidence.

### Model Comparison

The application also provides:

* Model accuracy comparison
* Validation loss
* Training curves
* Confusion matrices
* Model architecture information

---

## 📂 Project Structure

```text
Brain_tumar_detection/
│
├── app.py
├── brain_tumor_detection.ipynb
├── requirements.txt
├── .python-version
├── LICENSE
├── README.md
│
└── assets/
    ├── Training curves
    ├── Confusion matrices
    └── Model comparison images
```

---

## 🛠️ Technologies Used

### Programming Language

* Python

### Deep Learning

* TensorFlow
* Keras
* CNN
* VGG16
* ResNet50

### Image Processing

* OpenCV
* Pillow
* NumPy
* imutils

### Machine Learning

* Scikit-learn

### Visualization

* Matplotlib
* Seaborn
* Pandas

### Web Application

* Streamlit

### Model Hosting

* Hugging Face Hub

---

## 📦 Installation

> ⚠️ **Requires Python 3.11 - 3.13.** `tensorflow==2.20.0` publishes wheels for
> CPython 3.9 - 3.13 only, so `pip install -r requirements.txt` fails on
> Python 3.14+ with
> `ERROR: No matching distribution found for tensorflow==2.20.0`.
> The intended version is recorded in `.python-version` (`3.12`).

### 1. Clone the repository

```bash
git clone https://github.com/Rakshu123-hp/Brain_tumar_detection.git
```

### 2. Navigate to the project

```bash
cd Brain_tumar_detection
```

### 3. Create a virtual environment

```bash
python -m venv venv
```

### 4. Activate the environment

#### Windows

```bash
venv\Scripts\activate
```

### 5. Install dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ Run the Application

Start the Streamlit application:

```bash
python -m streamlit run app.py
```

The application will open in your browser at:

```text
http://localhost:8501
```

---

## ☁️ Deployment

> ⚠️ **Python 3.11 - 3.13 only.** `tensorflow==2.20.0` publishes wheels for
> **Python 3.9 - 3.13** and nothing newer, so any host that builds on 3.14+
> aborts with:
>
> ```text
> ERROR: Could not find a version that satisfies the requirement tensorflow==2.20.0
> ERROR: No matching distribution found for tensorflow==2.20.0
> [..] installer returned a non-zero exit code
> ```
>
> How the interpreter gets pinned depends on the platform — see below.

### Render (current deployment)

The app is live at:

```text
https://brain-tumar-detection-rvja.onrender.com
```

Render **does** honour `.python-version`, so the `3.12` pinned in this repo is
what keeps the build on a TensorFlow-compatible interpreter — no dashboard
setting is needed.

To redeploy:

1. Push to `main`; Render rebuilds automatically.
2. Watch the build log and confirm it reaches `Your service is live`.

Operational notes:

* The `Could not find cuda drivers` and `AVX2 FMA` lines in the log are
  informational, not errors — TensorFlow falls back to CPU, which is expected
  on Render's CPU instances.
* The six `.h5` models are downloaded from Hugging Face on first use
  (~401 MB in total), so the first prediction after a cold start can take a
  while. Render's free tier also spins the service down after inactivity.

#### Resource requirements

The free tier is **not** sufficient for this app. It provides 512 MB of RAM,
while TensorFlow plus one loaded model needs considerably more — the two
ResNet50 `.h5` files alone are ~130 MB each. When the container exceeds its
memory limit it is killed and restarted, which shows up in the browser as
intermittent `Failed to fetch dynamically imported module` errors and `502`
responses, even though the health endpoint passed moments earlier.

* Use a **`starter` (1 GB)** instance at minimum; **`standard` (2 GB)** is safer.
* Restrict the app to a single session so a second browser tab cannot start a
  second Python process holding its own copy of TensorFlow and the model. Set
  the Render start command to:

  ```bash
  streamlit run app.py --server.port $PORT --server.address 0.0.0.0 --server.maxSessions 1
  ```

### Streamlit Community Cloud

> ⚠️ **The Python version must be selected by hand in the dashboard.**
> Community Cloud ignores `runtime.txt`, `.python-version` and every other
> file, and the Python version of an existing app **cannot be changed in
> place** — the app has to be deleted and redeployed.

#### Steps

1. Push the repository to GitHub.
2. On [share.streamlit.io](https://share.streamlit.io), open the app and choose
   **Delete app**. (The Python version can only be chosen on a fresh deploy.)
3. Click **Create app** → **Yup, I have an app**.
4. Fill in the GitHub coordinates:
   * Repository: `Rakshu123-hp/Brain_tumar_detection`
   * Branch: `main`
   * Main file path: `app.py`
5. Click **Advanced settings** and set **Python version** to **3.12**.
6. Click **Save**, then **Deploy**.
7. Verify the build log contains `Using Python 3.12.x environment`.

If the log still reports a different interpreter, the version was not applied —
delete the app and repeat from step 3.

---

## 📓 Training the Models

The complete training workflow is available in:

```text
brain_tumor_detection.ipynb
```

The notebook contains the workflow for:

* Dataset loading
* Image preprocessing
* Data augmentation
* Model construction
* Model training
* Validation
* Accuracy and loss evaluation
* Confusion matrix generation
* Classification reports
* Model saving

The project contains training workflows for both binary and multi-class classification.

---

## ☁️ Running on Kaggle

For GPU-based model training, the notebook can be executed using Kaggle.

### Steps

1. Open Kaggle.
2. Create a new notebook.
3. Import `brain_tumor_detection.ipynb`.
4. Enable a GPU accelerator.
5. Add the Brain Tumor MRI Dataset for the multi-class task.
6. Run the notebook cells sequentially.

GPU acceleration can significantly reduce model training time.

---

## 📁 Dataset

### Binary Classification Dataset

The binary classification task uses the:

`akar49/MRI_Classification`

Dataset categories:

```text
No Tumor
Tumor
```

### Multi-Class Dataset

The multi-class task uses the:

`brain-tumor-mri-dataset`

Dataset categories:

```text
Healthy
Glioma
Meningioma
Pituitary
```

---

## 📈 Evaluation

The models are evaluated using:

* Accuracy
* Validation Loss
* Confusion Matrix
* Precision
* Recall
* F1-Score

Training and validation curves are also used to observe model learning behaviour.

---

## 🔍 Model Comparison

The application provides a direct comparison between:

```text
                    Model Comparison
                           │
           ┌───────────────┼───────────────┐
           │               │               │
           ▼               ▼               ▼
       Custom CNN        VGG16         ResNet50
           │               │               │
           └───────────────┼───────────────┘
                           ▼
                    Performance Analysis
```

This makes it possible to study how different CNN architectures perform on the same classification tasks.

---

## ⚙️ Input Processing

The application accepts:

```text
.jpg
.jpeg
.png
```

MRI images can be uploaded directly through the Streamlit interface.

The application performs the required preprocessing before passing the image to the selected model.

---

## ⚠️ Important Note

This project is developed for **educational and research purposes**.

The predictions generated by this application should not be considered a medical diagnosis or used for clinical decision-making.

Always consult a qualified medical professional for medical diagnosis and treatment decisions.

---

## 🚀 Future Improvements

Possible future enhancements include:

* Larger and more diverse datasets
* External test-set evaluation
* Cross-validation
* Explainable AI using Grad-CAM
* Improved image preprocessing
* Additional CNN architectures
* Model ensemble techniques
* Cloud deployment
* Improved user interface
* More extensive performance analysis

---

## 👩‍💻 Author

**Rakshitha H P**

Computer Science and Engineering – Data Science

---

## 📜 License

This project is available under the MIT License.

````


