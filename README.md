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
├── runtime.txt
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


