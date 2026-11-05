# 🤟 Vietnamese Sign Language (VSL) Translator

![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)
![Mediapipe](https://img.shields.io/badge/Mediapipe-Enabled-green)
![OpenCV](https://img.shields.io/badge/OpenCV-Supported-red)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Model-orange)

A real-time Desktop Application that translates Vietnamese Sign Language (VSL) into text and speech. Built with **Computer Vision (OpenCV & MediaPipe)** for hand-tracking and **Scikit-Learn** for gesture classification, this project provides a complete pipeline from dataset collection to model training and GUI deployment.

## ✨ Key Features
*   **Real-time Recognition:** Captures webcam feed to detect and translate VSL hand gestures instantly.
*   **Tkinter GUI:** A lightweight, user-friendly graphical interface (`src/gui.py`).
*   **Word Suggester:** An integrated NLP module (`src/word_suggester.py`) that predicts and suggests complete Vietnamese words based on recognized characters.
*   **Text-to-Speech (TTS):** Speaks out the translated Vietnamese text automatically using `pyttsx3`.
*   **Custom Training Pipeline:** Includes built-in scripts (`data/collect_images.py`, `data/create_dataset.py`) to easily collect new hand gestures and train your own custom model.

## 📁 Repository Structure

```text
VSL-translator/
│
├── data/                   # Dataset generation pipeline
│   ├── collect_images.py   # Script to capture hand images via webcam
│   ├── create_dataset.py   # Script to extract MediaPipe landmarks and save to CSV/Pickle
│   ├── words.csv           # Vocabulary dictionary
│   └── download_dataset.txt# Link to download the full raw dataset
│
├── docs/                   # Documentation & Logs
│   ├── CHANGES.md          # Version history
│   ├── LAYOUT_CHANGE_V2.3.md # UI update notes
│   └── UPDATE_PLAN.md      # Future development plans
│
├── models/                 # Pre-trained models
│   ├── model.p             # Trained classifier
│   └── download_model.txt  # Google Drive link for VSL.pickle
│
├── notebooks/              
│   └── model_testing.ipynb # Jupyter notebook for training and evaluating models
│
├── src/                    # Core application logic
│   ├── __init__.py
│   ├── backend.py          # Inference engine & MediaPipe wrapper
│   ├── config.py           # App configurations (colors, thresholds, etc.)
│   ├── gui.py              # Tkinter UI components
│   └── word_suggester.py   # Autocomplete & word suggestion algorithm
│
├── requirements.txt        # Dependencies (OpenCV, MediaPipe, sklearn, etc.)
└── main.py                 # Main entry point to launch the app

```

## ⚙️ Installation

**1. Clone the repository:**

```bash
git clone [https://github.com/NguyenVanThuong2112/VSL-translator.git](https://github.com/NguyenVanThuong2112/VSL-translator.git)
cd VSL-translator

```

**2. Install dependencies:**

```bash
pip install -r requirements.txt

```

**3. Download Pre-trained Models:**
Due to file size limits, the main model (`VSL.pickle`) is hosted on Google Drive.

* Open `models/download_model.txt` and navigate to the provided Google Drive link.
* Download `VSL.pickle` and place it inside the `models/` directory.

## 🚀 Usage

### 1. Run the Application

To launch the Translator GUI with the pre-trained model:

```bash
python main.py

```

*Note: Make sure your webcam is connected.*

### 2. Train Your Own Gestures (Custom Dataset)

This repository includes a full pipeline to train new signs:

1. **Collect Data:** Run `python data/collect_images.py` to open the webcam and capture images for new classes.
2. **Process Data:** Run `python data/create_dataset.py` to extract hand landmarks using MediaPipe and save them into a structured format.
3. **Train Model:** Open `notebooks/model_testing.ipynb` to train a new Scikit-Learn classifier (e.g., Random Forest) on your custom data and export the new `model.p` or `VSL.pickle`.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

## 📝 License

This project is open-source and available under the [MIT License](https://www.google.com/search?q=LICENSE).

```
